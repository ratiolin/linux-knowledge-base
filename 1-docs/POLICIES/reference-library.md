# 权威资料离线库（Reference Library）

> 来源：`技术氛围.md`。  
> 目标：一次性下载、长期复用，作为“事实层权威锚点”，减少二手教程污染。

---

一次性下载，十年内语言不过期。

⸻

📁 01-system-state-language

01.1 Linux man-pages（整包，必须）

文件
man-pages-6.x.tar.gz（以最新稳定主线为准）

官方项目主页（权威源）
	•	Linux man-pages Project
https://www.kernel.org/doc/man-pages/

直接下载（kernel.org，长期稳定）
	•	最新稳定版本目录：
https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/

示例（版本号随时间变化）：

https://mirrors.edge.kernel.org/pub/linux/docs/man-pages/man-pages-6.06.tar.gz

说明
	•	这是 Linus / kernel.org 官方镜像
	•	这是“语言环境塑形”的核心，不是工具文档
	•	DESCRIPTION / NOTES / SEE ALSO 的写法就是你要被浸泡的“空气”

⸻

01.2 systemd 官方文档（只要这 5 个）

来源组织
systemd

官方文档入口（HTML，权威）
https://www.freedesktop.org/software/systemd/man/

你只下载以下 5 个 man page（HTML 或保存为 PDF 均可）：
	1.	systemd.unit
https://www.freedesktop.org/software/systemd/man/systemd.unit.html
	2.	systemd.service
https://www.freedesktop.org/software/systemd/man/systemd.service.html
	3.	systemd.target
https://www.freedesktop.org/software/systemd/man/systemd.target.html
	4.	systemd-journald
https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html
	5.	systemd-analyze
https://www.freedesktop.org/software/systemd/man/systemd-analyze.html

说明
	•	这是 systemd 的“状态机母语”
	•	能直接决定你是否能看懂 systemctl status 的每一行
	•	不要 wiki、不要博客、不要教程

⸻

01.3 /proc 状态字段说明（只保留字段解释）

来源组织
Linux Kernel Organization

官方文档（权威文本）
	•	procfs 文档（内核文档）
https://www.kernel.org/doc/html/latest/filesystems/proc.html

你只保留并裁剪的部分：
	•	/proc/meminfo
	•	/proc/loadavg
	•	/proc/stat

可选：单文件版本（老但稳定，字段语言极其经典）

https://www.kernel.org/doc/Documentation/filesystems/proc.txt

说明
	•	这是“字段即事实”的典型语言
	•	不解释原因，只陈述状态
	•	对训练“看到数字就有直觉”非常关键

⸻

📁 02-incident-timelines

这一类不是官方文档，但必须来自真实生产事故，并且能长期访问。

⸻

02.1 内存 / OOM（必选 2 份）

文件 1
Linux OOM killer explained through a real incident

来源（权威技术博客，含真实输出）
	•	[Post Mortem: Kubernetes Node OOM](https://www.bluematador.com/blog/post-mortem-kubernetes-node-oom?utm_source=chatgpt.com)

（包含 dmesg / OOM 日志 / 误判过程）

文件 2 Out of memory outage postmortem (production server) 来源（真实事故复盘） • [Getting There | Ep. #7, The March 2023 Datadog Outage with Laura de Vesine | Heavybit](https://www.heavybit.com/library/podcasts/getting-there/ep-7-the-march-2023-datadog-outage-with-laura-de-vesine/)说明 • 明确时间线 • 含 free / top / kernel log • 不是“OOM 原理”，而是“怎么一步步翻车” ⸻

02.2 磁盘 / inode（必选 2 份）

文件 3
Disk full incident on Linux server – postmortem

来源
	•	[2018/02/07 Dynalist outage post-mortem - 🐛Bugs - Dynalist Forum](https://talk.dynalist.io/t/2018-02-07-dynalist-outage-post-mortem/1808?utm_source=chatgpt.com)

⸻

文件 4
inode exhaustion caused service outage

来源（经典 inode 翻车案例）
	•	[autofs service is failing due to exhausted inodes in "/tmp" filesystem | SUSE | Support Center](https://support.scc.suse.com/s/kb/autofs-service-is-failing-due-to-exhausted-inodes-in-tmp-filesystem?language=en_US&utm_source=chatgpt.com)

（文字不花，但信号极强）

⸻

02.3 systemd / 服务异常（必选 2 份）

文件 5
systemd service active but not responding – incident analysis

来源
	•	[centos - systemd service active but not executing - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/445901/systemd-service-active-but-not-executing?utm_source=chatgpt.com)

⸻

文件 6
Service startup failure due to dependency loop

来源（systemd 官方 issue 级分析）
	•	https://www.freedesktop.org/wiki/Software/systemd/Debugging/

（重点看 dependency loop / ordering）

⸻

02.4 权威平台事故（只选 2 份）

文件 7
GitHub Engineering – production outage postmortem

来源组织
GitHub

官方事故复盘入口
https://github.blog/category/engineering/

推荐具体一篇（经典时间线）：

https://github.blog/2018-10-30-oct21-post-incident-analysis/


⸻

文件 8
Cloudflare – incident report（network / system level）

来源组织
Cloudflare

官方事故报告索引
https://www.cloudflarestatus.com/incidents

推荐一篇（信号 / 发现 / 影响清晰）：

https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/

按你的要求：
只保留 Timeline / Impact / Detection，其余删掉。

⸻

✅ 你最终会得到什么
	•	约 10–12 个文件
	•	全部是：
	•	官方语言
	•	真实事故
	•	不依赖流行技术
	•	这是一个可以陪你整个运维生涯的“语言环境仓库”
