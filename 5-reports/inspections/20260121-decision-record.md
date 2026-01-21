# Decision Record

## 决策主题
Staging 是否启用 HTTPS

---

## 结论

**不启用 HTTPS，仅使用 HTTP**

---

## 事实依据

* 使用 prod TLS 配置与证书
* staging 使用 localhost / 非匹配域名
* TLS 握手阶段失败（SNI / CN 不匹配）

---

## 排除项

已明确排除：

* Docker 网络
* 端口映射
* 防火墙

---

## 不采取的方案

* 不签发新证书
* 不修改 prod TLS
* 不引入新组件

---

## 决策理由

* 目标是验证变更路径
* TLS 修复不影响目标成立
* 风险收益不匹配
