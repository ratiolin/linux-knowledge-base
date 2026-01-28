# Runtime Topology｜运行态结构说明

> 本文描述的是**当前系统的实际运行形态**，  
> 目标是帮助理解：服务跑在哪里、请求怎么走。

---

## 1. 系统定位

- 单机 Mattermost 服务
- 使用 Docker Compose 编排
- 对外通过 Nginx 提供访问
- 本环境用于**技能执行与结构理解**

---

## 2. 主机与资源

- OS：Linux
- 资源规模：
  - 内存：~4G
  - 磁盘：~40G

---

## 3. 服务组成

| 组件 | 作用 |
|----|----|
| Nginx | HTTP / HTTPS 入口 |
| Mattermost | 应用服务 |
| PostgreSQL | 数据存储 |

---

## 4. 请求链路

```text
Client
  ↓
Nginx (80 / 443)
  ↓
Mattermost (8065)
  ↓
PostgreSQL
```

---

## 5. 目录与数据布局

```text
environments/prod/
├── docker-compose.yml
├── data/
│   ├── db/
│   └── mm/
└── nginx/
```

staging 结构与 prod 类似，但数据独立。

---

## 6. 使用边界说明

- 允许直接修改 prod 配置
- 不存在强发布治理
- 本拓扑用于理解与练习，不承载真实 SLA

---

## 7. 阅读本文件后你应当理解

- 服务之间如何连接
- 请求从哪里进入
- 数据存在哪里
- 修改哪里会影响什么
