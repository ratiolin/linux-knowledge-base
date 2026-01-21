# Access Model

本文档描述当前服务器 **真实生效** 的账号、登录方式与权限边界。
任何权限调整，必须同步更新本文件。

---

## 一、账号清单

| 用户 | UID/GID | 登录方式 | sudo | 说明 |
|----|----|----|----|----|
| root | 0 | SSH 禁止 | N/A | 仅 break-glass |
| ratio | >=1000 | SSH Key | 受限 | 日常运维入口 |
| app-mm | >=1000 | SSH Key | 禁止 | 应用身份 |
| ops | 组 | N/A | 权限载体 | sudo 绑定组 |
| app | 组 | N/A | 无 | 应用只读访问 |

---

## 二、登录策略

* 禁止密码登录
* 禁止 root SSH 登录
* 所有用户仅允许 SSH key
* 不允许横向 su / sudo 提权

---

## 三、sudo 原则

* 禁止 `ALL=(ALL) ALL`
* 所有 sudo 权限必须：
  * 明确命令
  * 明确执行用户
  * 可审计

---

## 四、ACL 使用声明

以下路径使用 ACL，而非属主控制：

```text
/home/ratio/mattermost/environments/prod/data/mm
```
原因：

容器运行用户为 UID=2000

属主不等于运行用户

ACL 为长期正确解

## 五、变更规则
新用户 = 必须补充本文件

sudo 调整 = 必须补充本文件

ACL 调整 = 必须补充本文件