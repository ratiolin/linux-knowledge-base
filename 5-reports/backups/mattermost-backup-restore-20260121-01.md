# Day 4｜Mattermost 备份与恢复演练报告  
**日期**：2026-01-21  
**系统**：Mattermost（Docker Compose）  
**环境**：Prod  
**目标**：验证真实生产数据的备份可用性与恢复路径

---

## 0️⃣ 前置声明（审计免责线）

> 本次备份与恢复演练在 **低风险时间窗口** 执行，  
> 已确认无高频并发写入，  
> 允许在 prod 数据卷上进行一次可控破坏与恢复验证。

---

## 一、备份对象定义（以真实生效路径为准）

### 1️⃣ PostgreSQL 数据库（一级核心）

- 容器：`mm-db`
- 数据库：`mattermost`
- 角色：**唯一权威业务数据源**
- 备份方式：`pg_dump -F c`

---

### 2️⃣ Mattermost 文件数据（一级核心）

**真实生效路径（prod）：**

```text
/home/ratio/mattermost/environments/prod/data/mm
```
证据链：

```
chown -R 2000:2000 /home/ratio/mattermost/environments/prod/data/mm
```
风险说明：

数据库恢复 ≠ 文件恢复

文件路径错误将导致：

消息正常

附件 / 图片全部丢失

属于高概率、强感知生产事故

### 3️⃣ 配置文件（二级保护）
3.1 Docker Compose（prod）
```
/home/ratio/mattermost/environments/prod/docker-compose.yml
```
3.2 Nginx 配置与证书（共享路径）
```
/home/ratio/mattermost/nginx/conf.d
/home/ratio/mattermost/nginx/ssl
```
关键说明：

当前实例中，Nginx 配置与证书不随 environments 拆分，
staging / prod 共用同一配置源，因此备份路径位于 environments 之外。

## 二、备份目录与命名规范
```
/data/backups/20260121/
```
约定：

按日期分目录

不覆盖、不复用

仅存不可变备份

## 三、备份执行过程
### 1 PostgreSQL 备份
```
sudo docker exec -t mm-db pg_dump \
  -U mmuser \
  -F c \
  -f /tmp/mattermost-20260121.dump \
  mattermost
```
拷贝到宿主机：

```
sudo docker cp \
  mm-db:/tmp/mattermost-20260121.dump \
  /data/backups/20260121/
```
### 2 备份可用性验证（关键）
```
sudo docker exec -t mm-db \
  pg_restore -l /tmp/mattermost-20260121.dump | head
```
验证点：

Dump 非 0 字节

TOC Entries 正常

Dump / DB 版本匹配

### 3 Mattermost 文件数据备份
```
cd /home/ratio/mattermost/environments/prod

tar -czf /data/backups/20260121/mm-data-20260121.tar.gz \
  data/mm
```
### 4 配置文件备份
```
tar -czf /data/backups/20260121/mm-config-20260121.tar.gz \
  environments/prod/docker-compose.yml \
  nginx/conf.d \
  nginx/ssl
```
### 5 完整性校验（硬证据）
```
cd /data/backups/20260121
sha256sum * > SHA256SUMS
```
结果示例：

```
e6db2547c1a99a16d9ff1a33bb839580d4fe79230f9835620fad3191ba7bd226  mattermost-20260121.dump
e01f67340f68d9d8ffe2d25f48aed30181fb15f9d9280f17a2e6ed737b9bdea4  mm-config-20260121.tar.gz
f88873f5a54a70eb499fc7c939e50be2121582799cad67984934e7ea78fd136f  mm-data-20260121.tar.gz
```
## 四、破坏与恢复演练
### 1 破坏动作（可控）
删除一条明确可识别的历史消息

记录频道、内容、时间

确认前端不可见

### 2 恢复流程（prod）
停止服务
```
cd /home/ratio/mattermost/environments/prod
sudo docker compose down
```
模拟 DB 灾难
```
sudo rm -rf data/db/*
```
启动数据库
```
sudo docker compose up -d db
sleep 15
```
恢复数据库
```
sudo docker cp \
  /data/backups/20260121/mattermost-20260121.dump \
  mm-db:/tmp/restore.dump
sudo docker exec -t mm-db pg_restore \
  -U mmuser \
  -d mattermost \
  --clean \
  /tmp/restore.dump
```
启动完整服务
```
sudo docker compose up -d
sudo docker compose ps
```
## 五、恢复验证
### 1 业务验证
登录 Mattermost

被删除消息成功恢复

内容一致

### 2 文件系统验证
```
sudo docker exec -it mattermost \
  ls /mattermost/data | head
```
验证点：

目录存在

非空

无权限错误