# Change Record｜IAM v1.0 Bootstrap

## 变更目的

- 建立最小可治理权限体系
- 移除隐式 root 权限
- 明确 ops / app 权限边界

---

## 变更内容

- 创建 ops / app 角色组
- ratio 纳入 ops
- 创建 app-mm 应用用户
- 移除 docker / 隐式 sudo 高权
- 建立 sudo 白名单（runtime + governance）
- 禁止 root SSH 登录
- 禁止 SSH 密码登录
- 应用目录 ACL 只读授权

---

## 执行摘要

- 所有 sudo 权限通过组提供
- root 仅通过云控制面访问
- 应用用户无法访问系统权限

---

## 验证点

```bash
id ratio
sudo -l
sudo docker compose ps
sudo su -

id app-mm
sudo -l
ls /home/ratio/mattermost
```
## 回滚方案
使用云控制面 root

删除 sudoers.d 新增文件

恢复 SSH 配置

重启 sshd

## 风险与缓解
风险	                 缓解
sudo 自锁	    云控制面 root
SSH 错误	        systemctl reload sshd
ACL 错误      	setfacl 回滚
## 状态
变更状态：完成

验证：通过