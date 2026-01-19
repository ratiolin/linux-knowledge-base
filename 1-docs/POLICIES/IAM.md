# IAM v1.0｜最小可治理权限体系

## 1. 目标与原则

### 1.1 目标

- 从“单一用户 + 隐式 root”升级为：
  - 可审计
  - 可交接
  - 最小权限
  - 不自锁
- 明确区分：
  - 日常运维权限
  - 治理/救援权限
  - 应用访问权限

### 1.2 核心原则

- 权限绑定在**角色（组）**上，而不是用户
- 禁止用户级 sudo
- root 不参与日常操作
- 保留明确、受控的治理通道（break-glass）

### 1.3 非目标

- 不引入 LDAP / SSO
- 不实现多主机集中 IAM
- 不实现细粒度 RBAC
- 不覆盖设备级密钥管理

---

## 2. 权限层级模型

### Layer 0｜云控制面 / Out-of-Band Root

- 形式：
  - 云控制台免密登录
  - 救援模式 / 单用户模式
- 权限：
  - root
- 用途：
  - 修复 sudo / SSH / 系统级配置
- 特点：
  - 不可脚本化
  - 不参与日常运维

---

### Layer 1｜治理权限（Governance / Break-glass）

- 角色：ops
- 能力（通过 sudo 白名单）：
  - visudo
  - systemctl reload sshd
- 用途：
  - 修复权限配置
  - 修复 SSH 错误
- 禁止：
  - sudo su -
  - shell 级 root

---

### Layer 2｜运维权限（Runtime Ops）

- 角色：ops
- 能力：
  - Docker Compose 运维（受控）
  - Docker 状态查看
  - Docker 服务重启
  - 日志查看
  - 防火墙状态查看
- 禁止：
  - docker 组
  - 编辑 /etc
  - 提权 shell

---

### Layer 3｜应用权限（App）

- 角色：app
- 能力：
  - SSH key 登录
  - 只读访问应用目录
- 禁止：
  - sudo
  - docker
  - systemctl

---

## 3. 角色与用户映射

### 3.1 角色定义

| 角色 | 用途 |
|----|----|
| ops | 运维与治理 |
| app | 应用访问 |
| root | 仅控制面 |

### 3.2 当前用户映射

| 用户 | 所属组 | 说明 |
|----|----|----|
| ratio | ops | 主运维用户 |
| app-mm | app | 应用只读用户 |
| lighthouse | cloud-managed | 云厂商账户（不参与 IAM） |

---

## 4. sudo 策略（组级）

### 4.1 ops runtime sudo

文件：`/etc/sudoers.d/10-ops-runtime`

- Docker：
  - docker ps
  - docker compose ps / logs / restart
- systemd：
  - status / restart docker
- 日志：
  - journalctl -u docker / firewalld
- 防火墙：
  - firewalld --list-all

### 4.2 ops governance sudo

文件：`/etc/sudoers.d/20-ops-governance`

- visudo
- systemctl reload sshd

---

## 5. SSH 策略

- 禁止 root SSH 登录
- 禁止密码登录
- 仅允许 SSH key
- ops / app 可共用同一公钥（单人环境）

---

## 6. Docker 组安全说明

docker 组成员等价于 root 权限。  
IAM v1.0 中，所有非 root 用户均不加入 docker 组，  
通过 sudo 白名单受控执行 docker 命令。

---

## 7. 云厂商账户说明

系统存在云厂商预置账户（如 lighthouse）：

- 不赋 sudo
- 不加入 ops / app
- 仅用于控制面访问

---

## 8. 状态

- IAM 版本：v1.0
- 状态：已完成 / 可交付
