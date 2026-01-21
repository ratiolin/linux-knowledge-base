# Mattermost 权限检查清单

每次部署 / 迁移 / 故障排查前，必须逐项确认。

---

## 一、容器身份

- [ ] `docker inspect mattermost --format '{{.Config.User}}'`
- [ ] 记录 UID

---

## 二、Volume 实际路径

- [ ] `docker inspect mattermost | grep Mounts`
- [ ] 确认宿主机路径

---

## 三、写权限验证

- [ ] 宿主机路径可写
- [ ] UID/GID 匹配
- [ ] ACL 覆盖当前 + default

---

## 四、Nginx vs 应用限制

- [ ] nginx client_max_body_size
- [ ] Mattermost FileSettings
- [ ] 明确哪一层在拒绝

---

## 五、典型误判

- [ ] 413 ≠ 应用拒绝
- [ ] DB 正常 ≠ 文件系统正常