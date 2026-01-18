# Incident L1 起手检查单（3–5 分钟收敛假设）

> 来源：`训练方案.md` + `故障排查肌肉记忆.md` 中的“起手动作”，统一成可重复的 L1 顺序。

## 使用规则
- 先观察后修改；一次只验证一个假设；全程留痕。
- 每一步都要写一句“我在否定的假设”。

## L1 顺序（建议默认顺序）
1. 用户路径快速验证（curl/健康检查）
2. 服务状态（systemd）
3. 资源态（CPU/内存/磁盘/IO）
4. 网络态（监听/连接/队列）
5. 日志入口（journal + 应用日志）
6. 近期变更线索（发布/配置/计划任务/证书）

## 常用命令候选池（按需取用，逐步收敛为你自己的固定集）
```bash
uptime
htop
free -m
df -h
vmstat 1
sudo apt update
sudo apt install -y nginx
sudo sed -i 's/listen 80;/listen 8080;/' /etc/nginx/sites-available/default
sudo systemctl restart nginx
time curl http://127.0.0.1:8080/ > /dev/null
yes > /dev/null &
top
free -h
pkill yes
curl http://127.0.0.1:8080/
sudo systemctl stop nginx
systemctl status nginx
ps aux | grep nginx
ss -lnt
sudo systemctl start nginx
curl -i http://127.0.0.1:8080/
sudo sed -i 's/root /proxy_pass http:\/\/127.0.0.1:9999; #root /' /etc/nginx/sites-available/default
sudo nginx -t && sudo systemctl reload nginx
tail -n 50 /var/log/nginx/error.log
sudo sed -i 's/proxy_pass/#proxy_pass/' /etc/nginx/sites-available/default
sudo sed -i 's/#root /root /' /etc/nginx/sites-available/default
curl --max-time 3 http://127.0.0.1:8080/
sudo nft add rule inet filter input tcp dport 8080 drop
sudo nft delete rule inet filter input tcp dport 8080 drop
for i in {1..5}; do curl http://127.0.0.1:8080/; done
sleep 3
for i in {1..5}; do curl -i http://127.0.0.1:8080/; done
curl -i http://127.0.0.1:8080/submit
sudo sed -i 's/try_files \$uri \$uri\/ =404;/return 403;/' /etc/nginx/sites-available/default
sudo sed -i 's/return 403;/try_files \$uri \$uri\/ =404;/' /etc/nginx/sites-available/default
watch -n 2 curl http://127.0.0.1:8080/
echo '* * * * * yes > /dev/null' | crontab -
date
crontab -l
crontab -r
```

## L1 输出（必须写出来）
- 一句话系统结论：资源/状态/队列/边界的落位
- 3–5 个假设（按优先级）
- 下一步验证清单（命令+预期）
