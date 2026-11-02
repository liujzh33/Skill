---
name: annotation 静态页发布
description: '当用户要把标注对比/流程拆解类静态网页发布到 GitHub Pages，或挂到本机/服务器 IP:端口上公网或局域网访问时使用。'
---
# annotation 静态页发布

面向 `liujzh33/annotation` 这类「纯静态 HTML + data.js + 媒体」展示页。页面不依赖后端；GitHub Pages 与本机/VPS 静态服务可用同一套文件。

## 页面约定（每个展示页一个子目录）

子目录名即 URL 路径段，例如 `trace_352/`：

| 路径 | 作用 |
|---|---|
| `index.html` | 页面壳：样式 + 用 `window.DATA` 渲染步骤/调用卡片 |
| `data.js` | 以 `window.DATA = {...}` 导出 episode、步骤、模型调用与相对媒体路径 |
| 媒体目录 | 如 `a/`、`qm/`、`fm/`；`data.js` 里路径必须相对本子目录 |

仓库根目录额外需要：

- 空文件 `.nojekyll`（关闭 Jekyll，避免 `_` 开头路径被忽略）
- 可选根 `index.html`：列出各子目录链接

参考实现：仓库 `liujzh33/annotation` 的 `trace_352/`。

## A. 发布到 GitHub Pages

1. 确认目标仓库已开 GitHub Pages（Settings → Pages，源一般为 `main` / root）。公开仓地址形如 `https://<user>.github.io/<repo>/<subdir>/`。
2. 把完整子目录（html + data.js + 全部媒体）推到该仓库对应路径；勿漏相对路径引用的文件。
3. 大仓注意 GitHub 单文件 ≤100MB、建议单文件尽量小于约 50MB；视频可压缩或外链。
4. 推送后等 Pages 更新（通常一两分钟），用浏览器打开上述 URL 并点几处媒体确认能加载。
5. 新页若根目录有索引页，补上链接。

不要 clone 仅为了「看一眼」；读写文件用 GitHub 工具或云端 agent。用户明确要求本地预览/本机挂服务时，才下载静态产物到本机。

## B. 挂到本机或服务器 IP:端口

与 Pages 文件完全相同，只是换托管方式。

1. 取得静态站点根（含各子目录与 `.nojekyll`）。可从 GitHub 下 zip，或同步已有构建产物。
2. 查本机局域网 IPv4（Windows：`Get-NetIPAddress -AddressFamily IPv4`；优先 WLAN/以太网，忽略 `127.*`、常见虚拟网如 `198.18.*`；若有 Tailscale 可另报 `100.*`）。
3. 在**站点根目录**起静态服务，监听 `0.0.0.0` 与约定端口（常用 `10100`）：
   - `python -m http.server 10100 --bind 0.0.0.0`
   - 或 nginx/Caddy 把 root 指到该目录并 listen 该端口
4. 访问：`http://<局域网IP>:<端口>/<subdir>/`。同网段设备用局域网 IP；仅 Tailscale 互通时用 Tailscale IP。
5. 若打不开：检查进程是否在听、系统防火墙是否放行入站 TCP 端口、是否绑错网卡。
6. GitHub Pages **不能**变成 `http://IP:端口`；要 IP:端口必须自己跑静态服务。两套可并存。

## C. 以后「再写一页」时的执行顺序

1. 明确：子目录名、数据来源、媒体是否已齐、发到哪个仓库和/或哪台机器哪个端口。
2. 生成或拷贝 `index.html`（可复用现有壳）+ 写好相对路径的 `data.js` + 放入媒体。
3. 本地或临时目录打开 `index.html`/`data.js` 抽查路径。
4. 按用户要求走 A（Pages）和/或 B（IP:端口）。
5. 把可打开的最终 URL 发给用户。

## 成功标准

- Pages 或 `http://IP:端口/子目录/` 能打开，导航与图片/视频可加载。
- 未把仅适合某一台机器的绝对路径写进 skill；具体仓库、端口、IP 以当次用户说明与本机探测为准。
