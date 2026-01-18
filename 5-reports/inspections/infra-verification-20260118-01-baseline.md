# 基线核查报告

## 核查对象
- 服务：Mattermost
- 部署方式：Docker Compose + Nginx

## 核查项
- 服务可访问，HTTPS
- 容器状态正常
- 数据卷存在
- 端口暴露符合预期
- 日志无明显报错
- 重启后服务可恢复

## 关键证据
- docker compose ps
- ss -lntp
![[X241.png]]
![[X242.png]]

## 结论
当前系统处于最低可用状态。