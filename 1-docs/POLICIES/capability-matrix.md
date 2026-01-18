# Linux 运维与自动化运维能力清单

---
	参考材料:《Unix/Linux系统管理技术手册》第四版
	使用者：初级运维
	学习深度：
	
	-① 了解（Know）
	知道是什么、为什么存在、能看懂配置/输出
    
	- ② 会用（Operate）  
    能在指导/文档下完成操作，不追求优化
    
	- ③ 能独立执行（Own）  
    能独立完成常规操作，遇到问题能定位到方向

## 一
• Linux 系统安装、初始化与基线配置（分区、网络初配、时间同步等）；  
材料：第3章：系统引导与关机。
学习深度：③

---

## 二
• 用户、组、权限与 sudo 管控；基础身份与访问控制；SSH 与远程管理（密钥、跳板、安全策略、远程执行）；  
材料：第4章：访问控制与超级用户权限 + 第7章：新增用户。
学习深度：③

---

## 三
• 文件系统与存储管理（挂载、配额、LVM/RAID 基础、磁盘巡检）；  
• 备份/恢复与演练（备份策略、恢复验证、关键数据保护）；  
材料：第6章：文件系统 + 第8章：存储管理 + 第10章：备份。
学习深度：②

---

## 四
• 软件包/补丁管理与版本升级（rpm/deb、依赖、回滚常识）；  
材料：第12章：软件安装与管理。
学习深度：③

---

## 五
• 服务/进程管理（systemd、启动项、资源占用、僵尸进程处理）；  
材料：第3章：系统引导与关机 + 第5章：进程控制。
学习深度：③

---

## 六
• 网络配置与常见故障排查（路由、端口、连通性、抓包基础）；  
• 常见基础服务运维（DNS/HTTP/邮件等的基本运行与排障）；  
材料：第14章：TCP/IP 网络 + 第15章：路由 + 第17章：域名系统 + 第20章：电子邮件 + 第21章：网络管理与故障排查 + 第23章：网站托管。
学习深度：②

---

## 七
• 日志体系与审计基础（syslog/journald、日志轮转、定位问题）；  
材料：第11章：系统日志与日志文件。
学习深度：③

---

## 八
• 监控与性能分析（CPU/内存/IO/负载、容量趋势、瓶颈定位）；  
• 资产与容量台账维护（资源清单、容量评估、扩容建议）；  
材料：第29章：性能分析。
学习深度：②

---

## 九
• 安全基线与加固（最小权限、补丁、安全审计、入侵迹象基础）；  
材料：第22章：安全。
学习深度：②

---

## 十
• 故障响应与排障闭环（告警确认、止血、根因、复盘与改进）；  
• 变更实施与风险控制（计划、窗口、回退、记录、通知）；  
• 运维文档与知识库（SOP、Runbook、拓扑、资产、交接文档）；  
材料：第1章：从何入手 + 第32章：管理、策略与组织政治。
学习深度：③

---

## 十一
• Shell/脚本与任务调度（cron、批处理、参数化、错误处理）；  
材料：第2章：脚本与 Shell + 第9章：周期性任务。
学习深度：③

---

## 十二
• 运维脚本纳入版本控制与协作（分支、合并、评审、发布）；  
材料：第2章：脚本与 Shell。
学习深度：②
材料覆盖说明：  
未覆盖：版本控制协作流程、代码评审与合并策略、发布协作规范；  
补充：  
https://git-scm.com/doc ，  
https://docs.github.com/en/pull-requests ，  
https://docs.gitlab.com/user/project/merge_requests/ 。

---

## 十三
• 配置模板化/参数化与可复用（环境差异、变量、模板、清单）；  
• 批量操作与并发控制（并行执行、限速、幂等、失败重试/回滚）；  
材料：第2章：脚本与 Shell。
学习深度：①
材料覆盖说明：  
未覆盖：专门的配置管理体系（声明式、清单/Inventory、模板渲染、幂等模型）与大规模编排并发控制/幂等重试模型的工程化方法；  
补充：  
https://docs.ansible.com/ansible/latest/ ，  
https://www.puppet.com/docs/index.html ，  
https://docs.saltproject.io/salt/user-guide/index.html ，  
https://docs.chef.io/ ，  
https://docs.ansible.com/ansible/latest/playbook_guide/index.html 。

---

## 十四
• 日志/监控的自动化接入（采集、规则、告警路由、仪表盘）；  
• 运维报表与可视化（可用性/容量/告警统计、周月报自动生成）；  
材料：第2章：脚本与 Shell + 第11章：系统日志与日志文件 + 第29章：性能分析。
学习深度：①
材料覆盖说明：  
未覆盖：现代监控/日志平台的标准化接入与自动化编排（采集器、Exporter、Pipeline、告警路由等）与可视化平台报表体系；  
补充：  
https://prometheus.io/docs/introduction/overview/ ，  
https://prometheus.io/docs/prometheus/latest/getting_started/ ，  
https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/ ，  
https://prometheus.io/docs/alerting/latest/alertmanager/ ，  
https://grafana.com/docs/grafana/latest/ ，  
https://www.elastic.co/docs/solutions/observability/get-started ，  
https://www.elastic.co/docs ，  
https://opentelemetry.io/docs/concepts/signals/traces/ 。

---

## 十五
• 自动化中的安全（密钥/凭据管理、权限隔离、审计、最小暴露）；  
材料：第22章：安全 + 第2章：脚本与 Shell。
学习深度：①
材料覆盖说明：  
未覆盖：密钥与机密（Secrets）集中管理、动态凭据、密钥轮换、自动化审计落地方案；  
补充：  
https://developer.hashicorp.com/vault/docs ，  
https://kubernetes.io/docs/concepts/configuration/secret/ 。

---

## 十六
• 自动化变更回滚与发布策略（灰度/滚动/回滚、变更记录自动化）；  
• 自动化部署与发布：版本控制、代码评审、制品管理、发布流水线基础；  
• 将运维动作接入 CI/CD（自动化测试、构建、发布、回滚流水线）；  
材料：第10章：备份 + 第12章：软件安装与管理 + 第32章：管理、策略与组织政治 + 第2章：脚本与 Shell。
学习深度：①
材料覆盖说明：  
未覆盖：滚动/金丝雀/蓝绿等发布策略与平台化回滚细则、DevOps 工具链（VCS/Review/Artifact/Delivery）与流水线体系；  
补充：  
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/ ，  
https://www.jenkins.io/doc/book/pipeline/ ，  
https://docs.github.com/en/actions ，  
https://docs.gitlab.com/ee/ci/ ，  
https://argo-cd.readthedocs.io/en/stable/ ，  
https://fluxcd.io/flux/ ，  
https://docs.github.com/packages ，  
https://jfrog.com/help/r/jfrog-artifactory-documentation ，  
https://help.sonatype.com/en/sonatype-nexus-repository.html 。

---

## 十七
• 基础设施即代码 IaC（资源声明、评审、Plan/Apply、漂移治理）；  
• IaC 与云资源交付（Terraform/模板化部署/状态管理/漂移检测/策略约束）；  
学习深度：①
材料覆盖说明：  
未覆盖：IaC 体系与主流实现；  
补充：  
https://developer.hashicorp.com/terraform/cli ，  
https://developer.hashicorp.com/terraform/language ，  
https://opentofu.org/docs/ ，  
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html ，  
https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/ ，  
https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/ ，  
https://docs.cloud.google.com/deployment-manager/docs 。

---

## 十八
• 容器化与云原生基础运维（镜像、运行时、编排、集群基础管理）；  
• 容器与云平台基础运维（镜像、运行时、编排、集群基本操作与排障）；
学习深度：①
材料覆盖说明：  
未覆盖：容器/编排/云原生运维体系；  
补充：  
https://docs.docker.com/ ，  
https://docs.docker.com/engine/ ，  
https://kubernetes.io/docs/concepts/overview/ ，  
https://kubernetes.io/docs/reference/kubectl/ ，  
https://kubernetes.io/docs/setup/production-environment/container-runtimes/ ，  
https://helm.sh/docs/ ，  
https://specs.opencontainers.org/image-spec/ ，  
https://containerd.io/docs/ 。

---

## 十九
• 自动化测试与预演（脚本测试、配置校验、演练环境、变更前验证）；  
材料：第10章：备份 + 第2章：脚本与 Shell。
学习深度：①
材料覆盖说明：  
未覆盖：自动化测试框架与基础设施/配置测试工具链；  
补充：  
https://molecule.readthedocs.io/ ，  
https://testinfra.readthedocs.io/ ，  
https://docs.pytest.org/ 。

---

## 二十
• 自助化运维与 ChatOps（自助工单/自助脚本入口、审批与审计）；  
• 交付协作：工单/审批/通知联动（与研发/测试/安全/业务协同）；  
• 变更/发布治理：审批、风险评估、窗口与冻结；  
• 交接班与值班轮换管理；  
材料：第1章：从何入手 + 第32章：管理、策略与组织政治。
学习深度：①
材料覆盖说明：  
未覆盖：自助化平台与 ChatOps、ITSM 工具链 API 集成与流程编排、ITIL 式变更细则与值班治理工程化；  
补充：  
https://api.slack.com/ ，  
https://docs.mattermost.com/ ，  
https://docs.botkube.io/ ，  
https://www.atlassian.com/software/jira/service-management/product-guide/getting-started/change-management ，  
https://developer.atlassian.com/cloud/jira/platform/rest/v3/ ，  
https://developer.servicenow.com/ ，  
https://www.peoplecert.org/browse-certifications/it-governance-and-service-management/ITIL-1/itil-4-practitioner-change-enablement-3794 ，  
https://www.atlassian.com/itsm/change-management ，  
https://sre.google/workbook/on-call/ ，  
https://sre.google/sre-book/being-on-call/ 。
