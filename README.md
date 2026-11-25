# 个人 Shadowrocket 配置

给自己长期使用的规则分流配置。目标是看懂并控制流量走向，而不是做成另一份通用懒人配置。

## 项目目标

- iPhone 全天开启 Shadowrocket，使用规则分流。
- 国内服务直连，国外服务默认走首页所选节点。
- AI、流媒体、Apple、海外游戏可以单独改出口，但默认不自动测速。
- 局域网、自建服务和 Tailscale 有明确位置。
- 公共域名交给维护中的开源规则，个人只保留策略和例外。

优先级：安全性、网络稳定性、兼容性、可维护性，其后才是资源消耗和功能数量。没有手机实测之前，不把任何一项改动说成已经降低耗电或已经修好断网。

## 设计原则

- 主配置自己维护。LOWERTOP 的 `lazy_group.conf` 只作设计参考和上游快照。
- 公共规则优先直接引用上游维护的独立规则集，核对格式、覆盖范围和匹配顺序。现有来源见下文。
- 自建分流、个人例外，以及没有同范围独立上游文件的少量补充留在本地。
- 地区组保持四个。大公司单独建手动组，默认仍跟随「🚀 代理」，需要不同出口时再改。
- 不启用 Script。主配置不写 MITM 证书，默认不开启 HTTPS 解密。
- 不保存节点密码、订阅地址、Token、API Key、Tailscale 认证密钥、CA 私钥或证书密码。
- 不写 `update-url`。远程配置自动更新会覆盖个人修改。

## 配置来源与许可证

| 来源 | 用途 | 许可证 |
| --- | --- | --- |
| [LOWERTOP/Shadowrocket](https://github.com/LOWERTOP/Shadowrocket) `lazy_group.conf` | 设计参考与原始快照 | 仓库没有 LICENSE 文件。文件头写明基于官方群组「懒人配置.conf 2025-02-26 22:31:11」 |
| [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script) | 通用分流、服务及广告规则 | [GPL-2.0](https://github.com/blackmatrix7/ios_rule_script/blob/0b6897dc17e0c513d25449c935a9694818e32f0c/LICENSE)，README 另有转载声明。本仓库引用 URL |
| [TG-Twilight/AWAvenue-Ads-Rule](https://github.com/TG-Twilight/AWAvenue-Ads-Rule) | 多个 App 的纯广告规则 | [GPL-3.0](https://github.com/TG-Twilight/AWAvenue-Ads-Rule/blob/8965815bf3978bdaccdd7a18ec694db67e14d5c1/LICENSE)。本仓库引用 URL |
| [YUDIDIFEI/Scripts](https://github.com/YUDIDIFEI/Scripts) | 海外 AI 域名规则 | 仓库根目录未提供独立许可证。第三方来源见 [许可声明](https://github.com/YUDIDIFEI/Scripts/blob/30f374f407c20ba3ba1e4cb02650cdd658a3d42e/THIRD_PARTY_NOTICES.md) |
| [Repcz/Tool](https://github.com/Repcz/Tool) | 配置与聚合结构参考 | [MIT](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/LICENSE)，README 另有限制转载的声明 |
| [iab0x00/ProxyRules](https://github.com/iab0x00/ProxyRules) | 服务规则与转换模块参考 | 没有根许可证。[README](https://github.com/iab0x00/ProxyRules/blob/96cfe3360e70a2031b034fa0e8dd8228d1a7c3c7/README.md) 声明限制使用及转载 |
| [Johnshall/Shadowrocket-ADBlock-Rules-Forever](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever) | 规则构建与发布参考 | [CC BY-SA 4.0](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/192f7e7e5a71d4210f6e6e5d5a6b7d0f4fada2ef/LICENSE) |
| [luestr/ProxyResource](https://github.com/luestr/ProxyResource) | Loon 插件索引 | [CC BY-NC-SA 4.0](https://github.com/luestr/ProxyResource/blob/b7f70ce6ed207a2225851f0a2827675a3a538fe3/LICENSE)，仅配置模板声明开源，外部插件需另核对 |
| [akiralereal/shadowrocket-toolkit](https://github.com/akiralereal/shadowrocket-toolkit) | 原生模块与依赖验证参考 | [GPL-3.0](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/LICENSE)，第三方文件另附声明和许可证 |

公开可访问不等于可以镜像或再分发。公共规则直接引用 blackmatrix7、AWAvenue 和 YUDIDIFEI/Scripts 的上游文件。Module、Rewrite、MITM 和 JavaScript 不自动更新；真要使用时，固定提交、核对内容，并保留回滚。

上游快照：

- 文件：`upstream/lazy_group.conf`
- 获取日期：2026-11-25
- 下载地址：`https://raw.githubusercontent.com/LOWERTOP/Shadowrocket/main/lazy_group.conf`
- Pages 地址与 raw 内容 SHA-256 相同：`2B9A7E621301FCF4CF5FF572A6D00FDA52186495C138577C6035C3B912279A86`
- 上游标注日期：2026-10-15
- 对应提交：[`e1ee7d7`](https://github.com/LOWERTOP/Shadowrocket/commit/e1ee7d7a201fe55cfa3ec8f93d70fd6a76a33a3f)（2026-10-15）
- 提交说明：更新版本日期并加入 STUN 虚假地址

参数行为以 [LOWERTOP 手册](https://github.com/LOWERTOP/Shadowrocket/blob/main/README.md) 为准。手册依据 Shadowrocket 官方群组资料、更新日志和社区反馈整理，软件版本不同仍可能有差别。没有把 Surge、Clash 或 Quantumult X 的参数直接当成 Shadowrocket 行为。

blackmatrix7 仓库在 2026-10-28 仍有提交。具体规则文件的更新日期写在各文件头部，见下文表格。

## 文件结构

```text
Shadowrocket.conf                      实际导入的个人配置，不含证书
upstream/lazy_group.conf               上游原文，不参与导入
modules/google-cn-redirect.module      可选的 Google 入口跳转
modules/mitm-cert.module.example       证书模块模板，没有私钥
modules/mitm-cert.module               填好的证书模块，被 .gitignore 排除
README.md                              设计决策和用法
.gitignore                             避免提交密钥、证书和本地节点
```

规则数量还少，没有拆 `Rules/`，也没有生成器、CI 或定时同步。公共规则、功能模块和个人证书分开存放，更新其中一项时不改另外两项。

## DNS

直连域名使用两个国内 DoH，并行查询，谁先返回用谁：

- `https://doh.pub/dns-query`
- `https://dns.alidns.com/dns-query`

2026-11-25 对这两个地址发送了 `www.qq.com` 的标准 DoH 查询，都返回 HTTP 200 和应答。这只说明当时服务器有响应，不代表手机上的解析路径已经验证。

备用 DNS 是 `system`。覆写 DNS 失败或查询超过约 2 秒时，回退到系统 DNS。公共 Wi-Fi 的 `captive.apple.com` 单独匹配直连规则，并通过 `[Host]` 使用系统 DNS。

没有再加入 `223.5.5.5` 和 `119.29.29.29`。手册写明多个 DNS 并行、采用最先返回的结果；明文 DNS 可能比 DoH 更快返回，加密就失去意义。两家服务本身仍然保留。

其他关系：

- 命中代理策略的域名，由代理服务器解析，不走上面的国内 DoH。
- 未设置 `direct-dns-server`，直连域名使用 DNS 覆写。
- `dns-direct-system = false`，直连域名默认使用 DNS 覆写。`*.apple.com`、`*.icloud.com`、`home.arpa` 及其子域在 `[Host]` 里指定系统 DNS。局域网设备名称需要由当前网络提供的 DNS 解析。
- `dns-direct-fallback-proxy = true`：直连解析失败后改走代理。节点故障时，国内网站也可能一起失败。
- `hijack-dns` 只接管 `8.8.8.8:53` 和 `8.8.4.4:53`。
- `private-ip-answer = true`：解析到私有地址时不当成 DNS 劫持。局域网和 Tailscale 需要它。副作用是，污染结果若是私有地址，也不会因此强制走代理。
- IPv6 开启，但不优先 IPv6。与上游一致，避免一次改掉底层地址族行为。
- 配置没有指定 MagicDNS 服务器。启用自己的 tailnet 域名规则后，需要在手机上验证 Shadowrocket 能否解析完整主机名。

## 策略组

| 策略组 | 类型 | 默认 | 用途 |
| --- | --- | --- | --- |
| 🚀 代理 | select | 首页节点 `PROXY` | 普通代理流量。可改选地区组或 DIRECT |
| 🤖 AI | select | 🇺🇸 美国 | ChatGPT、Claude、Gemini、Grok、Copilot。规则在 Google 前面。默认美国，可改日本、新加坡、代理或直连 |
| 🎬 流媒体 | select | 🚀 代理 | YouTube、Netflix、Disney、Max、Spotify、TikTok |
| 🍎 苹果服务 | select | DIRECT | App Store、iCloud 等。需要时代理 |
| 🎮 游戏 | select | 🚀 代理 | Steam 国际、Epic、Nintendo。国内游戏不进这个组 |
| 🔍 Google | select | 🚀 代理 | 搜索、Gmail、Drive、Android 和 Google Cloud 托管域名。AI 列表已命中的域名不再进入本组，YouTube 由流媒体规则先匹配 |
| 🪟 微软 | select | 🚀 代理 | Microsoft 365、Windows、登录域名。Copilot 专用域名仍归 AI |
| 🐙 GitHub | select | 🚀 代理 | GitHub、GitHub Pages、npm。Copilot 专用域名仍归 AI |
| 🐦 X | select | 🚀 代理 | X、Twitter、t.co。Grok 仍归 AI |
| 👥 Facebook | select | 🚀 代理 | Facebook、Instagram、WhatsApp、Messenger |
| ✈️ Telegram | select | 🚀 代理 | Telegram 域名和地址段 |
| 🇭🇰 香港 / 🇯🇵 日本 / 🇸🇬 新加坡 / 🇺🇸 美国 | url-test | 第一个匹配节点 | 只有被上面的组选中后才参与自动测速 |

地区组参数：`interval=1800`，`tolerance=100`，`timeout=5`，测试地址 `http://www.gstatic.com/generate_204`。手册对 url-test 的说明是：连接命中该组后，使用最近一次结果，并按间隔进行下一轮测试。默认选择都不是地区组，所以导入后的默认路径不应自动测速。这个推断还没有在手机上确认。

节点来自 Shadowrocket 订阅。香港、日本和新加坡组支持国旗、地区名及独立的 `HK`、`JP`、`SG` 缩写。美国组支持国旗、美国城市名、国名和独立的 `USA`。短缩写要与相邻的拉丁字母和数字隔开，例如 `JP-01` 或 `SG_01`。没有匹配节点时，该组是空的，不要选择它。

台湾和韩国没有建组。首页节点仍然可以直接选用这些地区的服务器。

🤖 AI 默认选「🇺🇸 美国」。可选出口还有「🚀 代理」、日本、新加坡和直连。选中美国组后，AI 流量会触发该组的自动测速。没有名称匹配的美国节点时，这个组是空的，需要改选其他出口。

分组名称前的 Emoji 会显示在策略组列表里。规则里的策略名必须连同 Emoji 一起写。

YouTube、Netflix 仍共用「🎬 流媒体」。Google、微软、GitHub、X、Facebook 和 Telegram 已单独建组，导入后的默认出口仍是「🚀 代理」。Amazon 不建组，它的列表含有 AWS 域名。

## 规则顺序

1. 个人例外和公共 Wi-Fi 认证域名 `captive.apple.com`。
2. Tailscale 地址段和可选的个人 tailnet 后缀。其余 `ts.net` 域名走「🚀 代理」。
3. `localhost`、`.local`、`home.arpa`，然后是局域网规则集。
4. blackmatrix7 通用广告规则及 AWAvenue 纯广告补充，策略为 `REJECT`。
5. DeepSeek 直连。
6. 流媒体规则集。YouTube 在 Google 列表前面。
7. Steam 国区直连，Steam 国际、Epic、Nintendo 进入「🎮 游戏」。
8. Apple 域名集和规则集，进入「🍎 苹果服务」。
9. 海外 AI 规则集进入「🤖 AI」，然后才是 Google、微软、GitHub、X、Facebook、Telegram。
10. 中国域名集和规则集，直连。
11. Global 域名集和规则集，进入「🚀 代理」。
12. `GEOIP,CN,DIRECT`。
13. `FINAL,🚀 代理`。

`no-resolve` 加在局域网、Tailscale 和远程列表自带的 IP 规则上。域名请求遇到带 `no-resolve` 的 IP 规则时跳过，不额外做 DNS 查询。`GEOIP,CN` 不加 `no-resolve`，用来接住域名库没有收录、但地址属于国内的网站。

Tailscale 地址段和 `ts.net` 域名规则要放在 `Lan.list` 前面。该列表会将 `ts.net`、`100.64.0.0/10` 和覆盖 Tailscale IPv6 地址的 `fc00::/7` 匹配为直连。

`skip-proxy`、`tun-excluded-routes`、`DIRECT`、`TAILSCALE` 不是一回事：

- `DIRECT`：按规则直连。
- `TAILSCALE`：交给 Shadowrocket 内置 Tailscale 模块。
- `skip-proxy`：改由 TUN 处理，不是直连。纯 TUN 模式下此列表无效。
- `tun-excluded-routes`：IP 完全不进 TUN，让非 TCP 通过。

Tailscale 使用前要在 Shadowrocket「设置 > Tailscale」启用。需要 2.2.89 (3314) 或更高版本。认证密钥只填在软件设置里。默认可使用 `100.x` 或 `fd7a:115c:a1e0::/48` 内的设备地址。要用 MagicDNS，把注释规则里的 `your-tailnet.ts.net` 换成自己的 tailnet 后缀，再取消注释并使用完整主机名，例如 `nas.your-tailnet.ts.net`。若要经公网访问这个后缀下的某个 Funnel 主机，可在 tailnet 后缀规则前为该主机添加一条匹配「🚀 代理」的 `DOMAIN` 规则。

不要把 `100.64.0.0/10` 加入 TUN 旁路。官方 Tailscale App 与 Shadowrocket 同时作为系统 VPN 的行为没有在这台环境验证。

## 远程规则集

基础地址：

`https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Shadowrocket/`

通用规则来自 [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script) 的 `master` 分支。App 广告补充引用 AWAvenue 的 `main` 分支，海外 AI 引用 YUDIDIFEI/Scripts 的 `master` 分支。

域名规则超过 1000 条时，项目会把域名拆到 `*_Domain.list`。只引用短的 `.list` 会丢掉绝大部分域名。Apple、中国、Global 和去广告因此各用一对文件：`DOMAIN-SET` 引用域名集，`RULE-SET` 引用关键字、User-Agent、URL 正则和 IP。这个拆分来自项目自己的说明，以及 Apple 规则被误认为「只剩几十条」的问题记录。

Quantumult X 文件使用 `HOST-SUFFIX` 等类型。LOWERTOP 手册列出的 Shadowrocket 规则类型是 `DOMAIN-SUFFIX`，没有把 `HOST-SUFFIX` 列进去，所以这里不引用 Quantumult X 文件。

| 文件 | 引用方式 | 策略 | 文件内更新日期 | 原因 |
| --- | --- | --- | --- | --- |
| `Lan/Lan.list` | RULE-SET | DIRECT | 2026-10-20 | 私有地址和常见路由域名 |
| `Advertising/Advertising_Domain.list` | DOMAIN-SET | REJECT | 2026-10-28 | 去广告域名主体，约 29 万条 |
| `Advertising/Advertising.list` | RULE-SET | REJECT | 2026-10-28 | 关键字、URL 正则和带 `no-resolve` 的 IP |
| `AWAvenue-Ads-Rule-Surge-RULE-SET-Only.Ads.list` | RULE-SET | REJECT | 2026-11-23 | 补充多个 App 的开屏及广告 SDK 域名 |
| [YUDIDIFEI `AI.list`](https://github.com/YUDIDIFEI/Scripts/blob/30f374f407c20ba3ba1e4cb02650cdd658a3d42e/rule/Shadowrocket/AI/AI.list) | RULE-SET | 🤖 AI | 2026-11-25 | 写在 Google 列表前。列表内的 Gemini 域名进 AI，不另写本地例外 |
| `YouTube/YouTube.list` | RULE-SET | 🎬 流媒体 | 2025-06-06 | 需要独立出口 |
| `Netflix/Netflix.list` | RULE-SET | 🎬 流媒体 | 2025-06-06 | 同上 |
| `Disney/Disney.list` | RULE-SET | 🎬 流媒体 | 2025-07-30 | 同上 |
| `HBO/HBO.list` | RULE-SET | 🎬 流媒体 | 2025-06-06 | Max / HBO。补充 `discomax.com` 和 `brightline.tv`，`litix.io` 由广告规则先匹配 |
| `Spotify/Spotify.list` | RULE-SET | 🎬 流媒体 | 2025-06-06 | 与其他流媒体共用出口 |
| `TikTok/TikTok.list` | RULE-SET | 🎬 流媒体 | 2026-10-16 | 国际版。抖音在中国域名集里，不进这个组 |
| `SteamCN/SteamCN.list` | RULE-SET | DIRECT | 2025-06-06 | 国区 CDN，写在 Steam 国际规则前面 |
| `Steam/Steam.list` | RULE-SET | 🎮 游戏 | 2026-10-24 | 国际 Steam |
| `Epic/Epic.list` | RULE-SET | 🎮 游戏 | 2025-06-06 | Epic |
| `Nintendo/Nintendo.list` | RULE-SET | 🎮 游戏 | 2026-05-04 | Nintendo |
| `Apple/Apple_Domain.list` | DOMAIN-SET | 🍎 苹果服务 | 2026-10-26 | Apple 域名主体 |
| `Apple/Apple.list` | RULE-SET | 🍎 苹果服务 | 2026-10-26 | 关键字、User-Agent、IP |
| `Google/Google.list` | RULE-SET | 🔍 Google | 2026-05-12 | 不含 YouTube。接收 AI 列表没有先命中的 Google 域名 |
| `Microsoft/Microsoft.list` | RULE-SET | 🪟 微软 | 2025-12-08 | 避免被中国规则里的 `microsoft` 关键字直连 |
| `GitHub/GitHub.list` | RULE-SET | 🐙 GitHub | 2025-06-12 | 从 Global 拆出。同时含 `npmjs.com`、`github.io` |
| `Twitter/Twitter.list` | RULE-SET | 🐦 X | 2025-09-28 | `x.com`、`twitter.com`、`t.co` |
| `Facebook/Facebook.list` | RULE-SET | 👥 Facebook | 2025-06-06 | 已含 Instagram、WhatsApp、Messenger |
| `Telegram/Telegram.list` | RULE-SET | ✈️ Telegram | 2025-09-10 | 域名、地址段和 ASN |
| `China/China_Domain.list` | DOMAIN-SET | DIRECT | 2026-06-22 | 国内域名主体 |
| `China/China.list` | RULE-SET | DIRECT | 2026-06-22 | `.cn`、关键字、User-Agent、少量 IP |
| `Global/Global_Domain.list` | DOMAIN-SET | 🚀 代理 | 2026-10-28 | 国外域名主体，约 3.5 万条 |
| `Global/Global.list` | RULE-SET | 🚀 代理 | 2026-10-28 | 关键字、User-Agent、IP |

这些 URL 在 2026-11-25 可以下载，内容是规则或域名，不是 HTML，也没有再嵌套远程规则。Global、中国列表和去广告列表必须成对使用，不能只留其中一个。去广告域名集约 5.9 MB、290392 条；规则集 781 条，其中 IP 规则全部带 `no-resolve`。抽查时 `apple.com`、`google.com`、`github.com`、`qq.com`、`baidu.com`、`microsoft.com` 的主域名不在域名集里。`doubleclick` 由规则集里的关键字覆盖。

没有同时引入功能重复的列表：

- 不用 `Proxy.list`。它和 Global 都是国外代理列表。
- 不用 `ChinaMax.list`。体积很大，并带有大量 User-Agent，和中国列表、GEOIP 重复。
- 不单独引用哔哩哔哩、微信、百度、抖音等。`bilibili.com`、`qq.com`、`taobao.com` 已在中国域名集。
- GitHub 使用独立列表，写在 Global 前面。GitHub Copilot 专用域名仍由更早的 AI 规则集匹配。
- 不引用 Instagram、WhatsApp 短列表。Facebook 列表已经包含这些域名。
- 不引用 Amazon 列表。其中有 AWS 域名，会把大量第三方服务带进同一个组。
- 海外 AI 直接引用一份 Shadowrocket `AI.list`，写在 Google 列表前面。列表里已有的 Gemini 域名进「🤖 AI」，没有再手写一套 Google AI 域名。其余 Google 流量进「🔍 Google」。 [取样提交](https://github.com/YUDIDIFEI/Scripts/blob/30f374f407c20ba3ba1e4cb02650cdd658a3d42e/rule/Shadowrocket/AI/AI.list)
- Repcz 的 HBO 列表包含所需的 Max 域名，也包含整个 `s3-ap-southeast-1.amazonaws.com`。保留 blackmatrix7 HBO 和两条独立的 Max 后缀，避免把该 S3 区域一起送入流媒体组。 [Repcz HBO 列表](https://github.com/Repcz/Tool/blob/X/Shadowrocket/Rules/HBO.list)
- 不引用 `Game.list`。其中有 `login.live.com` 和国内游戏域名。
- 不引用 `Sony.list`。其中同时有 `sony.com` 和 `sony.com.cn`。
- 不引用 LOWERTOP 使用的 `iab0x00/ProxyRules` AI 合集。2026-11-25 复核过正文，见「候选上游审查」。
- 不引入 Loyalsoldier。它与 Global、GEOIP 的职责重叠。
- 广告规则使用 blackmatrix7 `Advertising` 和秋风广告规则 `Only.Ads`。`Only.Ads` 有 671 条规则，其中 654 条是精确域名或后缀。与 blackmatrix7 的域名、后缀和关键字对照，有 220 条尚未覆盖，包括 `api.aqyad.com`、`adxstatic.vivo.com.cn`、`adsfileretry.service.kugou.com` 和 `ads-vp5.xhscdn.com`。`api.aqyad.com` 现由远程规则维护。 [取样版本](https://github.com/TG-Twilight/AWAvenue-Ads-Rule/blob/8965815bf3978bdaccdd7a18ec694db67e14d5c1/Filters/AWAvenue-Ads-Rule-Surge-RULE-SET-Only.Ads.list) · [Shadowrocket 引用方法](https://doc.awads.cc/ShadowRocket.html)

重新编译时，blackmatrix7 和 YUDIDIFEI/Scripts 从 `master` 获取规则，AWAvenue 从 `main` 获取规则。需要冻结版本时，把对应 URL 的分支名换成该仓库的提交哈希。

已知的远程列表瑕疵，默认出口相同时影响较小，一旦把「流媒体」或「游戏」改到其他地区就会显现：

- Netflix 含有 `us-west-2.amazonaws.com`。
- Disney 和 HBO 含有部分 `execute-api.*.amazonaws.com`。
- Epic 含有共用域名 `helpshift.com`。
- Nintendo 含有 `35.192.0.0/12`，行内带 `no-resolve`，只匹配已经是 IP 的连接。
- 中国规则含有 `DOMAIN-SUFFIX,ms`，会让 `.ms` 后缀直连。
- 中国规则含有 `DOMAIN-KEYWORD,microsoft` 和 `USER-AGENT,Microsoft*`。Microsoft 规则写在前面，已收录的微软域名仍走代理；没命中微软列表、但 User-Agent 像微软的请求，可能在到达中国规则后直连。
- Microsoft 列表含有 `live.com`、`office.com` 这类较宽后缀，因此这些域名进入「🪟 微软」。该组默认仍是「🚀 代理」。
- Google 列表的 `DOMAIN-KEYWORD,google` 是子串匹配，并包含 `google.com`、`googleapis.com`、`gstatic.com`、`appspot.com`、`run.app`、`web.app`、`cloudfunctions.net`、`blogspot` 和 `schema.org`。AI 列表写在它前面，已收录的 Gemini 域名先进入「🤖 AI」。没被 AI 列表收录的 Google 域名仍进「🔍 Google」。把该组改到其他地区后，这些域名会跟着走。
- Facebook 列表含有 `groups.com`、`i.org`、`login-account.net`、`flow.dev`、`parse.com`。Instagram 和 WhatsApp 也在这份列表里。
- Telegram 列表含有 `contest.com`、`graph.org`、`usercontent.dev`。IP 和 ASN 规则带 `no-resolve`。
- X 列表含有 `grok.com`，但 AI 规则写在前面，Grok 仍进「🤖 AI」。
- 去广告规则集里的 `DOMAIN-KEYWORD` 是子串匹配，例如 `umeng`、`adservice`、`openx`、`advert`、`fenxi`。作者说明可能误拦截。被误伤的域名写到规则最前面的个人例外。
- 去广告列表主要按广告和统计域名拦截。YouTube 等与正片共用域名的广告通常仍会出现。`Advertising.list` 的 HTTPS 路径规则需要解密，主配置默认关闭 HTTPS 解密。

## 候选上游审查

2026-11-25 对照实际配置、规则文件、生成脚本和许可证进行静态复核。下表链接指向本次取样的提交。规则比较去掉注释，保留匹配类型，将 `DOMAIN-SET` 中带前导点的条目按后缀处理。计算覆盖时区分完全匹配和父域后缀包含，广告比较另计关键字命中。域名计数不包含 IP、User-Agent、URL 正则，也不代表手机上的广告拦截率。

| 候选 | 内容分类 | 本仓库的取舍 |
| --- | --- | --- |
| [LOWERTOP/Shadowrocket](https://github.com/LOWERTOP/Shadowrocket/tree/9ff0cc1564d528b9e77a863b39fc443b08cf98ae) | 主配置参考 | 保留手册与本地快照作为参考 |
| [Repcz/Tool](https://github.com/Repcz/Tool/tree/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket) | 主配置参考、通用分流规则、精细化服务规则、广告拦截规则 | 参考主配置与外置规则的结构 |
| [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script/tree/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket) | 通用分流规则、精细化服务规则、广告拦截规则、可选功能模块 | 通用分流、服务规则和广告拦截共用这一运行时来源 |
| [Johnshall/Shadowrocket-ADBlock-Rules-Forever](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/tree/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa) | 主配置参考、广告拦截规则、脚本及构建工程参考 | 参考离线模板生成和发布分支的做法 |
| [iab0x00/ProxyRules](https://github.com/iab0x00/ProxyRules/tree/96cfe3360e70a2031b034fa0e8dd8228d1a7c3c7) | 精细化服务规则、广告拦截规则、可选功能模块 | 对照 AI 覆盖和规则粒度，DeepSeek 保留个人直连规则 |
| [akiralereal/shadowrocket-toolkit](https://github.com/akiralereal/shadowrocket-toolkit/tree/f45de28fe932249503bf4d50a285884bc643ca94) | 广告拦截规则、可选功能模块、脚本及构建工程参考 | 参考原生模块和依赖锁定方式 |
| [luestr/ProxyResource](https://github.com/luestr/ProxyResource/tree/b7f70ce6ed207a2225851f0a2827675a3a538fe3) | 可选功能模块的索引 | 用于了解 Loon 插件和转换依赖 |

### LOWERTOP 的 General 与规则注释

| 参数 | 上游配置的实际行为与本仓库的取舍 |
| --- | --- |
| `skip-proxy`、`tun-excluded-routes` | 前者把指定流量交给 TUN，后者让指定 IP 网段绕过 TUN。上游 `skip-proxy` 还列了银行、百度和网易。本仓库保留本机、局域网及认证页相关条目，并用规则单独指定认证页直连。 |
| `dns-server`、`fallback-dns-server` | 上游并列两家 DoH 和两个明文 DNS，并以系统 DNS 备用。按手册的并发解析说明，明文应答可能先返回。本仓库只保留两家 DoH，并保留系统 DNS 备用。 |
| `ipv6`、`prefer-ipv6`、`private-ip-answer`、`dns-direct-fallback-proxy` | 两份配置都启用 IPv6 但优先 IPv4，接受私有地址应答，并允许直连域名解析失败后回退代理。 |
| `hijack-dns`、`udp-policy-not-supported-behaviour`、`block-quic`、`stun-response-ip` | 两份配置都只接管两个 Google DNS 地址，节点不能转发 UDP 时拒绝，代理连接阻断 QUIC。上游额外配置了 STUN 虚假应答，本仓库省略这一项。 |

上游注释区分 `RULE-SET` 和 `DOMAIN-SET`，并说明模块规则优先和 IP 规则的 `no-resolve`。上游成品同时使用若干 Quantumult X 文件，里面有 `HOST-SUFFIX`。本仓库选用 blackmatrix7 的 Shadowrocket 版本，以 `DOMAIN-SUFFIX` 和对应域名集表达分流。抽查的当前 `lazy_group.conf`、本地快照和 Johnshall 同名发布文件 SHA-256 相同，视为同一份参考。 [General 与规则注释](https://github.com/LOWERTOP/Shadowrocket/blob/e1ee7d7a201fe55cfa3ec8f93d70fd6a76a33a3f/lazy_group.conf) · [Johnshall 同步文件](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/192f7e7e5a71d4210f6e6e5d5a6b7d0f4fada2ef/lazy_group.conf)

### Repcz 的外置规则与聚合

`Shadowrocket.conf` 通过 22 个 `RULE-SET` 把规则外置。实际顺序是 `Direct`、`Reject`、AI 和各服务、`Proxy`、`AppleServers`、`Lan`、`GEOIP`、`FINAL`。它启用了 `update-url`、两个明文 DNS、`*:53` 劫持和地区组 300 秒测速。`AppleServers` 指向香港测速组。部署整份配置会改变现有 DNS、Apple 出口和规则优先级。 [主配置](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Shadowrocket.conf)

- `Direct.list` 在 `Reject.list` 前，包含 `dl.google.com`、`update.googleapis.com`、`msg.umeng.com` 等精确直连例外。`AI.list` 匹配 `api.github.com`，并含 `DOMAIN-KEYWORD,openai` 和一条 Google URL 正则。把 AI 列表移到本配置 GitHub 规则前会改变通用 GitHub API 的出口。 [直连](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/Direct.list) · [AI](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/AI.list)
- 它的 `Proxy.list` 有 16,946 条精确域名或后缀，其中 15,330 条由 blackmatrix7 `Global` 的域名或上级后缀覆盖。Netflix 的 28 条后缀全部与现用 Netflix 列表相同，IP 规则另有差异。Steam 的 20 条后缀中有 17 条与现用 Steam 列表相同。差异里有 `steamcontent.com`，Repcz 将其归入游戏组，本仓库由 `SteamCN` 先匹配直连。 [Proxy](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/Proxy.list) · [Netflix](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/Netflix.list) · [Steam](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/Steam.list)
- 主配置实际启用的是 `Reject.list`。仓库还单独提供 `Ads_EasyListChina`、`Ads_EasyListPrivacy`、`Ads_AWAvenue` 等变体。`Reject` 含复合 `AND` 规则，Netflix 文件含 `IP-CIDR6`，所以域名覆盖统计之外还需要核对这些规则的客户端语义。 [Reject](https://github.com/Repcz/Tool/blob/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules/Reject.list)

### blackmatrix7 的覆盖与规则优先级

- 通用层用 `Lan`、`China`、`Global` 配合本地 `GEOIP,CN`。`Proxy` 的 6,859 条域名或后缀中有 6,856 条被 `Global` 的域名和后缀覆盖。差异包括 `chat.openai.com`，现有 `openai.com` 本地规则已将其送入 AI 组。`ChinaMax` 含更多域名、IP 和 ASN。`China` 的 3,691 条域名或后缀有 3,547 条被 `ChinaMax` 的域名和后缀覆盖，因此两者有交集，但不能按文件名假定是严格包含。 [Global](https://github.com/blackmatrix7/ios_rule_script/tree/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/Global) · [Proxy](https://github.com/blackmatrix7/ios_rule_script/tree/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/Proxy) · [ChinaMax](https://github.com/blackmatrix7/ios_rule_script/tree/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/ChinaMax)
- 精细层按服务选择独立出口。`OpenAI` 含 `sentry.io`、`stripe.com` 和 ASN，`Copilot` 含 `www.bing.com`，部分目标会影响其他服务。当前优先级下，`chatgpt.com` 进 AI，`api.github.com` 进普通代理，`sentry.io` 先命中广告规则。改用完整 AI 列表时，其位置会决定这些重叠目标被拒绝还是改走 AI 出口。`captive.apple.com` 的本地直连则先于 Apple 集合。 [OpenAI](https://github.com/blackmatrix7/ios_rule_script/blob/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/OpenAI/OpenAI.list) · [Copilot](https://github.com/blackmatrix7/ios_rule_script/blob/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/Copilot/Copilot.list)
- 广告层的 `Advertising_Domain.list` 有 290,392 条域名，`Advertising.list` 有 278 条关键字、489 条 IP 规则和 14 条 URL 正则。对照同版本 `Advertising_Resolve.list`，实际差异是 IP 规则是否带 `no-resolve`。一对文件都要引用才能保留域名和带类型的规则。HTTPS 路径匹配需要解密，当前配置只使用现有纯规则策略。`googleadservices.com` 会先被拒绝，`ads.youtube.com` 由新增的 AWAvenue 纯广告表匹配。与正片共用 HTTPS 主机的广告需要按路径或响应处理。 [Advertising 说明](https://github.com/blackmatrix7/ios_rule_script/blob/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/Advertising/README.md)

### 广告候选的有效重叠

下表用现用 `Advertising` 两份文件比较候选中的唯一精确域名和后缀。父域后缀能覆盖子域，精确域名不能覆盖整个后缀。第三列额外计算关键字匹配产生的覆盖。IP、复合规则、重写、脚本和相对顺序需要分开判断。

| 候选 | Advertising 域名及后缀覆盖 | 再计 Advertising 关键字 | 差异示例 |
| --- | ---: | ---: | --- |
| blackmatrix7 `AdvertisingLite` | 37,164 / 37,692 | 37,689 / 37,692 | `ad.10010.com`、`awstrack.me`、`imasdk.googleapis.com` 三条精确域名仍未命中，精简版也有独立的 IP 条目 |
| Repcz `Reject` | 6,669 / 7,540 | 6,853 / 7,540 | `getui.cn` 在这份表中被拒绝，当前配置按 `.cn` 直连 |
| Repcz `Ads_EasyListChina` | 5,602 / 5,837 | 5,605 / 5,837 | EasyList China 也被 Johnshall 直接使用，blackmatrix7 通过 ACL4SSR 汇集 |
| Repcz `Ads_AWAvenue` | 430 / 978 | 542 / 978 | Repcz 和 akiralereal 提供了核对 AWAvenue 上游的依据 |
| AWAvenue `Only.Ads` | 364 / 654 | 434 / 654 | 直接引用的纯广告版，补充多个 App 的广告域名 |
| Johnshall `sr_ad_only.conf` | 45,545 / 53,143 | 45,832 / 53,143 | 含 `admob.com` 等完整后缀，无其他模块能力 |
| iab0x00 `Block.txt` | 947 / 1,091 | 1,024 / 1,091 | `a.ki`、`a8.net`、`a9.com` 已命中现用表。`ads.youtube.com` 是新增的精确匹配 |
| akiralereal `adblock.module` 的 `[Rule]` | 161 / 260 | 203 / 260 | `api.aqyad.com` 等独立规则，另有 URL 重写和响应脚本 |

完整版与精简版高度重合。其他列表也有新增，但主要增量来自额外拦截域、规则类型或脚本，叠加会扩大现有拦截范围。当前接入 blackmatrix7 `Advertising` 成对文件和 AWAvenue 原项目的 `Only.Ads`。Repcz 的 AWAvenue 派生表、其他广告变体和整包脚本模块作为比较材料。 [精简版来源](https://github.com/blackmatrix7/ios_rule_script/blob/0b6897dc17e0c513d25449c935a9694818e32f0c/rule/Shadowrocket/AdvertisingLite/README.md) · [Repcz 广告规则](https://github.com/Repcz/Tool/tree/f38c422b03d81dbc73cf9eb233698c04f4fbd053/Shadowrocket/Rules) · [Johnshall 广告输入](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa/factory/ad.py) · [akiralereal 第三方声明](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/third_party/NOTICE.md)

### Johnshall 的构建、离线生成和分支

- `build` 保存模板、手工名单、`resultant/` 中间结果和构建脚本。定时入口 `factory/auto_build.sh` 依次执行 `ad.py`、`gfwlist.py`、`build_confs.py`。`chnroutes.py` 和 `top500.py` 是独立的输入生成工具。广告脚本在线读取 EasyList China、EasyList、乘风规则、Peter Lowe，只提取可表达为整域或 IP 封禁的条目，跳过元素隐藏及带选项的规则，并结合例外和忽略列表。 [构建入口](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa/factory/auto_build.sh) · [广告提取](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa/factory/ad.py)
- 已用取样提交的 `resultant/`、`manual_*.txt` 和 `template/` 禁用联网运行 `build_confs.py`，生成 12 份配置。与本次取样的 `release` 去掉注释后比较，3 份的有效行一致，9 份存在差异。离线渲染依赖已有输入快照，刷新上游输入仍要联网。四份 Top500 成品仍带 blackmatrix7 `AppleNews` 远程规则，`sr_ad_only.conf` 则只有 `[Rule]` 和显式封禁策略，无 `FINAL` 或远程引用。把广告成品用作纯规则集之前，需要去掉配置节头并核对嵌入策略。 [离线生成器](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa/factory/build_confs.py) · [发布产物](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/tree/192f7e7e5a71d4210f6e6e5d5a6b7d0f4fada2ef)
- `release` 是面向用户的默认分支。发布工作流检出 `build` 和 `release`，重新构建，下载 LOWERTOP `main` 的两份懒人配置，并以孤立提交强制更新 `release`。`build` 另有工作流写回构建分支。二者取样时的 cron 为 UTC 23:00，即北京时间次日 07:00，源码注释和 README 写的是 08:00。 [build 工作流](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/ff8ecea54bb71deaab5ef13bfd466e7da03a50fa/.github/workflows/main.yml) · [release 工作流](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/192f7e7e5a71d4210f6e6e5d5a6b7d0f4fada2ef/.github/workflows/release.yml)

### iab0x00 的 AI 与轻量广告

实际规则在 `main`，默认 `master` 只有说明。LOWERTOP 已经引用这里的 `AI.txt`。这些文件的域名规则自带类型，可以按 `RULE-SET` 分配策略。`Block.txt` 另含 IP、User-Agent 和通配符，不能把原文当作 `DOMAIN-SET`。 [main 的 Rule 目录](https://github.com/iab0x00/ProxyRules/tree/96cfe3360e70a2031b034fa0e8dd8228d1a7c3c7/Rule) · [master 说明](https://github.com/iab0x00/ProxyRules/blob/c8db03dff7a95d465391923426f7ae9053f1b8bc/README.md)

| 文件 | 对照与决策 |
| --- | --- |
| `AI.txt`、`AINA.txt` | 实际集合满足 `AI = AINA ∪ AppleIntelligence`。`AINA` 70 条，Apple 段 10 条，互不重复。两版共享整段 `googleapis.com`、`facebook.com`、`meta.com` 和 `www.bing.com`，以及多个统计或认证服务。审查时的 24 条 AI 精确域名或后缀中，18 条受其域名范围覆盖。`gemini.google.com`、`copilot.microsoft.com` 等仅收录精确主机名，范围与原有后缀规则不同。 |
| `AppleIntelligence.txt` | 有 `*mask*.icloud.com`、`*siri*.apple.com`、`smoot.apple.com` 和中继域名。把 `AI.txt` 放在 Apple 规则前会把 `mask.icloud.com` 从 Apple 组改到 AI 组。`AINA` 移除了这一段，仍保留 Google 等宽后缀。 |
| `DeepSeek.txt` | 9 条唯一规则。除 `deepseek.com` 外，还有 `apmplus.volces.com`、`static.portal101.cn`、`nexus-websocket-a.intercom.io` 等。现有本地规则只对 DeepSeek 自有后缀指定直连。 |
| `Block.txt` | 1,104 条唯一规则，其中 1,091 条为精确域名或后缀。`adservice` 是子串关键字，`ads.youtube.com` 是精确域名。后者若放在 YouTube 前会改变该主机的策略，单条域名规则无法判断与正片共用主机的请求。 |

### akiralereal 的原生模块与依赖校验

- `dist/*.module` 是原生模块。通用 `adblock.module` 同时含 `[Rule]`、`[URL Rewrite]`、`[Script]` 和 `[MITM]`。YouTube 对 `youtubei.googleapis.com` 的响应调用脚本，Spotify 还使用 `[Header Rewrite]`。两个红果实验版本中，`hongguo-experimental.module` 只有域名规则，`hongguo-loading-experimental.module` 还启用重写和 MITM。模块规则优先于配置，整包接入可能抢先命中本地策略。 [原生模块](https://github.com/akiralereal/shadowrocket-toolkit/tree/f45de28fe932249503bf4d50a285884bc643ca94/dist)
- README 安装 URL 跟随 `main`，模块内脚本 URL 固定到 40 位提交 `0936bba…`。`third_party/scripts.json` 记录运行时镜像的 SHA-256，以及上游仓库、提交、路径、原始哈希、许可证和改动。独立核验了 8 个模块脚本引用，以及 8 份固定运行时和 8 份原始文件的 SHA-256。CI 执行生成一致性、语法验证、测试和 `audit_scripts.py --local-only`，在线审计模式才重新取第三方原件。 [依赖锁](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/third_party/scripts.json) · [审计脚本](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/tools/audit_scripts.py) · [CI](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/.github/workflows/validate.yml)
- 来源有 app2smile、ofwh（MIT）、Maasea（Apache-2.0），广告域名另选取 AWAvenue 子集（GPL-3.0）。这些文件由第三方声明和许可证逐项记录。主配置直接引用 AWAvenue 原项目的纯广告规则。 [第三方声明](https://github.com/akiralereal/shadowrocket-toolkit/blob/f45de28fe932249503bf4d50a285884bc643ca94/third_party/NOTICE.md)

### luestr 的插件资源与兼容性

公开仓库 `Tool/` 内是 Clash、Loon、Quantumult X 配置，`Resource/Ad/` 中是说明页，插件安装指向外部中心。在仓库快照中未找到 Shadowrocket 原生模块。iab0x00 的 `PluginHub2Rocket.srmodule` 展示了转换链：改写 Loon `.lpx` 导入链接，经 Script-Hub 生成 Shadowrocket 模块，并需要对插件中心启用 MITM。转换路径的存在不能验证每个插件的规则、脚本 API 或改写行为在 Shadowrocket 上等价。插件目录保留为索引参考。luestr 的 README 另列商业用途和传播范围的声明，外部插件由插件来源单独核对。 [luestr 仓库说明](https://github.com/luestr/ProxyResource/blob/b7f70ce6ed207a2225851f0a2827675a3a538fe3/README.md) · [插件中心](https://hub.kelee.one/) · [转换模块源码](https://github.com/iab0x00/ProxyRules/blob/96cfe3360e70a2031b034fa0e8dd8228d1a7c3c7/Rewrite/PluginHub2Rocket.srmodule)

候选项目的根许可证及附加声明见上文。聚合规则或脚本中的单项来源要以各自的版权和授权记录核对。LOWERTOP 和 iab0x00 的取样树均没有根许可证，LOWERTOP 的现有原文快照按本地参考管理。主配置的远程规则来源是 blackmatrix7、AWAvenue 和 YUDIDIFEI/Scripts 的海外 AI 列表。Johnshall 的 LOWERTOP 镜像、Repcz 的聚合规则和各类广告变体作为比较材料。

## 与 LOWERTOP 的主要差异

| 配置项 | 上游 | 最终 | 原因 | 潜在影响 |
| --- | --- | --- | --- | --- |
| DNS | 两个 DoH 加两个明文 DNS | 只保留两个 DoH，失败回退系统 DNS | 并行查询会采用最先返回的结果，明文可能抢先 | DoH 被网络拦截时，要等失败或超时才用系统 DNS |
| skip-proxy | 局域网、认证页，以及银行、百度和网易 | 只留局域网、本机、`.local`、认证页 | 银行和网站条目是个别兼容例外，不是当前场景 | 这些 App 若必须靠原条目，需要再加回 |
| STUN 虚假地址 | `1.1.1.1` 和 `::1` | 不设置 | 稳定性优先于未验证的 WebRTC 防泄漏 | 直连 WebRTC 仍可能暴露地址 |
| URL Rewrite / MITM | 两条 302，解密 `*.google.cn` | 主配置不解密。跳转和解密域名在功能模块，证书在本地模块 | 证书、功能和主配置可以分别更新、回滚 | 未启用本地证书模块时，HTTPS 跳转不生效 |
| 策略组 | 十多个服务组，六个地区组每 600 秒测试、容差 0 | 服务组加 Google、微软、GitHub、X、Facebook、Telegram；四个地区组 1800 秒、容差 100，且默认不选中 | 大公司可以单独改出口，默认仍跟随「🚀 代理」 | 公司列表里的宽域名会跟着该组的出口变化。流媒体内部仍不能拆 Netflix 和 YouTube |
| AI 规则 | 第三方 AI 合集，默认注释里还有整段 Google | 直接引用海外 AI 域名规则集 | 覆盖原有主要 AI 服务及更多专用端点 | 编译时按上游更新，新增服务跟随 AI 策略组 |
| Apple / 中国 / Global | Quantumult X 全量文件 | Shadowrocket 的 `.list` 加 `_Domain.list` | 避免未记录的 `HOST-SUFFIX` 类型，并补齐被拆走的域名 | 远程文件以后拆分方式变化时要重新检查 |
| 国内网站 | 多个单独服务列表 | 中国列表和 GEOIP | 这些域名已经在中国域名集 | 中国列表没收录的国内站靠 GEOIP；解析失败或污染时可能走代理 |
| 广告、脚本 | 上游没有脚本和广告模块 | 主配置通过 blackmatrix7 和 AWAvenue 拦截广告域名 | 域名拦截直接随主配置生效 | 约 29 万条域名，编译时要下载约 6 MB。关键字可能误伤 |
| FINAL | `PROXY` | `🚀 代理` 策略组，默认仍是首页节点 | 需要时可以只改兜底出口 | 把「🚀 代理」选成某个地区组后，未命中流量会进入该组并触发测速 |

保留的上游行为：IPv6 开但 IPv4 优先、私有地址应答、直连解析失败后走代理、DNS 劫持、UDP 不支持时拒绝、只阻断代理连接的 QUIC、TUN 旁路网段、Apple 使用系统 DNS、局域网直连、兜底走代理。

## 导入和使用

1. 把 `Shadowrocket.conf` 传到 iPhone（AirDrop、iCloud 或文件 App）。不要导入 `upstream/lazy_group.conf`。
2. Shadowrocket：配置 → 添加 → 从文件导入。
3. 点该配置，执行「使用配置 / 编译配置」。这一步才会下载远程规则。
4. 打开配置的规则集 URL 页面。失败项要重新拉取后再编译。GitHub 不通时，可临时把全局路由设为「代理」，用一个可用节点完成编译，然后改回「配置」。
5. 首页用订阅添加节点。全局路由选择「配置」。
6. 不要开启简单模式。简单模式会按延迟自动更换首页节点，默认容差是 0，和这份配置的手动选择冲突。
7. 手动延迟测试可以用 CONNECT。这只影响你主动点的测试。

「全局路由 = 代理」会使策略组失效。正常使用时保持「配置」。

## 证书与功能模块

四份东西分开管理：

| 内容 | 位置 | 更新时能否改动其他部分 |
| --- | --- | --- |
| 主配置 | `Shadowrocket.conf` | 不写证书，也不带 `[MITM]` |
| 公共规则 | 配置里的远程 URL | 编译时由软件下载，不进入证书模块 |
| 功能模块 | `modules/google-cn-redirect.module` | 可单独启用，使用 `hostname = %APPEND%` 追加解密主机名 |
| 个人证书 | 本地的 `modules/mitm-cert.module` | 被 `.gitignore` 排除。更新主配置或功能模块时不要覆盖它 |

需要 Google 国内入口的 HTTPS 跳转时：

1. 在 Shadowrocket 里用一份临时配置生成 CA 证书，安装描述文件，并在系统设置 → 通用 → 关于本机 → 证书信任设置中信任它。完成这一步之前不要启用证书模块，否则可能出现 `No PKCS12 Certificates`。
2. 把 `modules/mitm-cert.module.example` 复制为 `modules/mitm-cert.module`。证书内容粘贴到 `ca-p12=` 后面，身份证书密码粘贴到 `ca-passphrase=` 后面，再把 `enable=false` 改为 `enable=true`。安装时提示的常见密码是 `Shadowrocket`。
3. 配置 → 模块 → 新建模块，分别导入功能模块和本地证书模块，并启用。功能模块可以单独停用。
4. 证书模块只留在手机或你自己的加密备份里。不要提交 Git，不要放到 CDN 或公共规则地址上，也不要使用别人模块里的 CA 私钥。

主配置没有 `[MITM]`，所以不启用证书模块时不会解密 HTTPS。以后新增需要解密的功能时，继续用 `hostname = %APPEND%`，不要在功能模块里写 `ca-p12`。模块中的 `h2 = true` 会覆盖主配置里的同名设置。

## 订阅

节点只在 Shadowrocket 的订阅功能里更新。订阅地址、密码和 Token 不进入 Git。更新订阅是软件设置，不是修改本文件。

`PROXY` 指首页当前选中的节点。「🚀 代理」策略组默认选它。换首页节点，就会换所有仍跟随「🚀 代理」的流量。

## 自定义个人规则

在 `[Rule]` 最前面增加，并去掉注释。示例域名不要原样启用。

```text
# DOMAIN-SUFFIX,git.example.com,DIRECT
# DOMAIN,gitea.example.com,DIRECT
# IP-CIDR,192.168.1.50/32,DIRECT,no-resolve
```

自建服务若通过 Tailscale 访问，可用 `100.x`，或启用个人 tailnet 后缀规则后使用完整 MagicDNS 主机名。

只有规则多到难以阅读，或确实要单独更新时，再拆成 `Rules/*.list`。现在不拆。

## 上游更新

LOWERTOP 发布新版本时：

1. 下载新的 `lazy_group.conf`。
2. 与 `upstream/lazy_group.conf` 做 diff。
3. 只挑选有依据的改动进入 `Shadowrocket.conf`。
4. 替换快照，在本说明里更新提交号、日期和 SHA-256。
5. 再做一次静态检查，并在手机上按下面的清单验收。

不要用上游文件覆盖个人配置。

每次编译会按配置里的链接拉取 blackmatrix7、AWAvenue 和 YUDIDIFEI/Scripts。规则集 URL 页面会显示下载结果。

## 故障排查

先区分现象，再改参数。下面没有一项被当成已经验证的修复。

Wi-Fi 显示已连接但不能上网：

- 全局路由是否仍是「配置」，节点是否真的可用。
- `dns-direct-fallback-proxy = true` 时，直连解析失败会改走代理。节点故障会让国内网站一起失败。排查时可以临时改为 `false`。
- 公共 Wi-Fi 认证时，检查 `captive.apple.com` 是否命中直连规则，以及系统 DNS 是否可用。
- 编译失败会导致规则缺失。查看规则集 URL 是否全部成功。
- IPv6 异常时，可以把 `ipv6` 临时改为 `false` 做对比。这不是默认建议。
- DoH 走 HTTP/3 异常时，可以在链接后加 `#no-h3` 做对比。默认没有加。

Tailscale 不通：

- 确认软件版本和「设置 > Tailscale」已启用，且没有把认证密钥写进配置。
- 先用 `100.x` 测试隧道。测试完整 MagicDNS 主机名时，确认个人 tailnet 后缀规则已启用并放在通用 `ts.net` 规则之前。
- 确认 `100.64.0.0/10` 不在 `tun-excluded-routes`。
- 在代理日志里检查请求命中了哪条 `TAILSCALE` 规则。命中后仍无法访问时，检查模块是否已连接到对应的 tailnet。

AI 能开页面但不能登录或调用：

- ChatGPT、Claude、Grok、Copilot 用「测试规则」核对，策略应是「🤖 AI」。
- `gemini.google.com` 在 AI 列表中，策略应是「🤖 AI」。不在该列表里的 Google 域名命中「🔍 Google」，默认跟随「🚀 代理」。

## 回滚

主配置、上游快照和功能模块都在 Git 里，可以按文件恢复，不必连带证书。恢复后在手机上重新导入并编译。`modules/mitm-cert.module` 不在 Git 里，回滚配置或功能模块不会改它；证书要靠手机里的模块或你自己的加密备份恢复。

未提交前，直接从编辑器或 `git checkout --` 恢复对应文件。不要用 `reset --hard` 除非明确知道工作区里没有要留的修改。

上游快照是回看原始行为的副本，不是手机上的第二份可用配置。

## 尚未验证

本环境不能运行 Shadowrocket。下面都不是手机测试结果：

- 配置能否被当前版本完整编译。
- `policy-select-name` 使用中文策略名是否生效。
- 空的地区组会不会在编译时报错。
- url-test 在没有流量命中时是否完全不测试。
- DoH、备用系统 DNS、Apple Host 在 Wi-Fi 和蜂窝切换、公共 Wi-Fi 认证页中的实际顺序。
- Tailscale 模块是否解析 MagicDNS，以及与官方 Tailscale App 能否共存。
- `GEOIP` 触发解析时用的是 DNS 覆写还是系统 DNS。手册对 IP 规则的表述是「本地 DNS」。
- `private-ip-answer` 是否把 `100.64.0.0/10` 视为私有地址。
- IPv6、QUIC、STUN 和耗电的实际影响。
- 启用本地证书模块和 Google 跳转模块后，`g.cn`、`google.cn` 的 HTTPS 302 是否生效。
- 远程列表里的宽规则在改动「流媒体」「游戏」或公司组出口后的误匹配范围。
- 约 29 万条去广告域名在当前版本上能否编译，以及对耗电的影响。
- 去广告关键字是否误伤正在使用的 App。

静态检查已经完成的部分见本次变更说明：配置结构、策略组引用、远程 URL 可访问性和规则格式。

## 手机验收

- 国内网站和 App。
- 国外网站。
- ChatGPT、Claude、Gemini、Grok、Copilot、DeepSeek。Gemini 应命中「🤖 AI」。
- Apple 服务，包括 App Store 和 iCloud。
- Microsoft 登录、GitHub、Google、X、Facebook、Instagram、WhatsApp、Telegram。改公司组出口后再看这些服务是否跟着切换。
- 实际使用的流媒体和游戏。
- 局域网设备，包括使用 `home.arpa` 名称的设备。
- Tailscale 的 `100.x`、启用个人后缀后的完整 MagicDNS 名称，以及需要访问的公网 Funnel。
- Wi-Fi 与蜂窝切换、VPN 重连、长时间待机。
- 公共 Wi-Fi 登录页。
- 规则命中和出口是否与策略组一致。可在 Shadowrocket 的「测试规则」和代理日志里看。
- 选中地区组后，测速间隔和切换是否可接受。
- 连续使用数天后，电池占比是否可接受。
- 常用 App 开屏、网页广告是否减少。若正常功能受影响，在连接日志确认命中的列表和域名，再按需添加个人例外。

## 待确认

- 实际订阅里的地区名称是否能被四个正则匹配。
- 是否需要台湾或韩国组。
- 自建服务器、Gitea 和私有域名的真实地址。确认前不要把示例写进生效规则。
- DeepSeek 若在当前网络必须代理，把那一条从 `DIRECT` 改为 `🚀 代理`。
- Spotify 若必须直连而 Netflix 必须代理，再把 Spotify 从「🎬 流媒体」拆出去。

## 现在不做的事

不增加配置生成器、自动合并、CI、定时拉取上游或独立更新日志。先在手机上稳定使用。以后只有出现明确的维护问题时，再拆规则文件或固定远程规则版本。
