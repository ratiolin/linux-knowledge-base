# Sudo Governance Design

本文档说明 sudoers 的 **治理意图**，而非命令清单。

---

## 一、设计目标

* 最小权限
* 显式授权
* 防误操作
* 可审计

---

## 二、角色划分

| 角色 | 能做什么 | 不能做什么 |
|----|----|----|
| ops | 运维执行 | 任意 root shell |
| ratio | ops 成员 | 越权操作 |
| app-mm | 应用 | 所有 sudo |

---

## 三、受控脚本机制

### 示例

```text
/usr/bin/staging-compose-up
```
原则：

sudo 只允许执行脚本

脚本内部固定目录、固定行为

不允许参数注入

## 四、禁止项
明确禁止：

```
sudo su -
sudo bash
sudo sh
```
理由：

无审计边界

无回滚路径