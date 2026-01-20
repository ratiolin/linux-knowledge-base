# Change Record｜Staging 验证后推广至 Prod

## 1. 变更背景

为验证“生产变更必须先经过非生产环境”的流程有效性，
本次执行一次低风险、可验证的配置变更。

---

## 2. 变更内容

- 修改 Nginx 请求体大小限制
- 参数：`client_max_body_size 5M;`

---

## 3. 基线状态（变更前）

- Prod 服务正常运行
- 权威配置路径：
  - `/home/ratio/mattermost/environments/prod`
- 对外访问方式：HTTPS

---

## 4. Staging 实施

### 4.1 实施位置

```text
/home/ratio/mattermost/environments/staging
```
### 4.2 实施内容
修改 Nginx 配置

使用 HTTP 访问（不涉及 TLS）

### 4.3 应用变更
sudo staging-compose-up
## 5. Staging 验证
验证方式
访问 http://localhost:8080

登录 Mattermost

上传超过 5MB 的文件

验证结果
请求被拒绝

行为符合预期

## 6. 推广至 Prod
推广方式
将已验证的配置复制至 Prod 环境

不在 Prod 中重新设计或试验

应用命令
sudo docker compose restart nginx
## 7. Prod 验证
访问生产域名

执行同样的上传操作

行为与 Staging 一致

## 8. 回滚方案
如出现异常：

git checkout nginx/conf.d/*.conf
sudo docker compose restart nginx
## 9. 结论
变更路径已验证

Staging → Prod 流程可执行

本次变更未引发异常

## 10. 状态
记录类型：计划内变更

结果：成功