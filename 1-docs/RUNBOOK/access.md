# Access Runbook｜用户与权限操作手册

## 1. 新增 ops 用户（示例）

```bash
useradd -m -s /bin/bash <user>
usermod -aG ops <user>
```
配置 SSH key

不加入 docker 组

不赋用户级 sudo

## 2. 新增 app 用户
```
useradd -m -s /bin/bash <user>
usermod -aG app <user>
```
必须配置 SSH key

禁止 sudo

通过 ACL 授权只读目录

## 3. 撤销用户权限
移出角色组：

```
gpasswd -d <user> ops
gpasswd -d <user> app
```
或删除用户：

```
userdel -r <user>
```
## 4. 治理 / Break-glass 操作
触发条件
sudoers 错误

SSH 配置错误

权限自锁

操作方式
使用云控制面 root 登录

修复 sudoers / sshd_config

完成后退出 root

## 5. 禁止事项
不使用 root 日常操作

不赋用户级 sudo

不将 ops / app 加入 docker 组

