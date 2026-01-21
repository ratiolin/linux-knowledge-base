# Nginx Layout Decision

---

## 一、当前结构

```text
environments/
  ├── prod/
  └── staging/

nginx/
  ├── conf.d/
  └── ssl/
```
## 二、设计结论
Nginx 配置 不随 environments 拆分

prod / staging 共用一套配置与证书

## 三、原因
当前仅验证变更路径

不引入额外复杂度

TLS 不属于 Day 3 范围

## 四、已知风险
staging 修改 nginx = 影响 prod

需人工纪律保证

## 五、未来演进条件
当满足以下任一条件时，必须拆分：

staging 对外暴露

多域名 / 多证书

自动化部署引入