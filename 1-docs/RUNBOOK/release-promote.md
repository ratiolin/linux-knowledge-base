# Release Promote Runbook（Staging → Prod）

## 1. Promote 原则

- Prod 不允许实验性修改
- 所有变更必须先在 staging 验证
- Promote 必须附带 change-record

## 2. 发布入口

唯一命令：

sudo /home/ratio/mattermost/scripts/promote-prod.sh

## 3. 回滚入口

sudo /home/ratio/mattermost/scripts/rollback.sh <backup-dir>

## 4. Prod 配置锁

Prod docker-compose.yml 默认 immutable：

lsattr environments/prod/docker-compose.yml

必须包含 i 标志。
