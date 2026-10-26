# Surge 分流规则

自用的 Surge 分流规则集，Clash 通过 Sub-Store 引用同一套规则。

## 引用地址

下载、系统更新等需要强制直连

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Special.list
```

Telegram 域名与官方 IP 段

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Telegram.list
```

YouTube 与 Google 视频 CDN

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/YouTube.list
```

香港区流媒体：Disney+、Max、myTV SUPER、Netflix、ViuTV

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/HK.list
```

日本站点：Yahoo! JAPAN、DMM

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/JP.list
```

新加坡区流媒体：TVBanywhere、meWATCH

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/SG.list
```

OpenAI、Cursor、Grok、Perplexity、Spotify、TikTok、X 等

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/US.list
```

常用境外网站与服务

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/ProxyLite.list
```

国内网站、国内 CDN 与 Apple 服务

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Domestic.list
```

QX 用的代理合集（ProxyLite、US、Telegram、YouTube 的合并版）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Global.list
```

AI 服务：Apple Intelligence、Claude、Gemini、Copilot 等

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/AI.list
```

台湾站点与流媒体：巴哈姆特、KKTV、LINE TV 等

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/TW.list
```

Amazon 购物、开发者与广告域名

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Amazon.list
```

Apple 推送服务（APNs）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/ApplePush.list
```

QX 格式的副本在 [wsc82/QuantumultX](https://github.com/wsc82/QuantumultX)，Clash 格式的副本（Global、Domestic、JP）在 [wsc82/Clash](https://github.com/wsc82/Clash)，每天自动同步，改规则只改这里就行。

## 规则集

按 Surge 配置里的匹配顺序排列：

| 规则集 | 内容 | 策略 |
| --- | --- | --- |
| [Special](Ruleset/Special.list) | 下载、系统更新等需要强制直连的流量，排在最前面 | DIRECT |
| [Telegram](Ruleset/Telegram.list) | Telegram 域名与官方 IP 段 | Telegram |
| [YouTube](Ruleset/YouTube.list) | YouTube 与 Google 视频 CDN | YouTube |
| [HK](Ruleset/HK.list) | 香港区流媒体：Disney+、Max、myTV SUPER、Netflix、ViuTV | HK |
| [JP](Ruleset/JP.list) | 日本站点：Yahoo! JAPAN、DMM | JP |
| [SG](Ruleset/SG.list) | 新加坡区流媒体：TVBanywhere、meWATCH | SG |
| [US](Ruleset/US.list) | OpenAI、Cursor、Grok、Perplexity、Spotify、TikTok、X 等 | US |
| [ProxyLite](Ruleset/ProxyLite.list) | 常用境外网站与服务 | TOP |
| [Domestic](Ruleset/Domestic.list) | 国内网站、国内 CDN 与 Apple 服务 | DIRECT |

之后是 Surge 内置的 `RULE-SET,LAN`、`GEOIP,CN` 和 `FINAL`。

## 其他规则集

[Global](Ruleset/Global.list) 是 Quantumult X 在用的代理合集（ProxyLite、US、Telegram、YouTube 的合并版），配合 Domestic 直连。Quantumult X 的配置及其专用规则现已移至 https://github.com/wsc82/QuantumultX。

下面几个目前没有被引用，留着以后可能用：

| 规则集 | 内容 |
| --- | --- |
| [AI](Ruleset/AI.list) | AI 服务：Apple Intelligence、Claude、Gemini、Copilot 等 |
| [TW](Ruleset/TW.list) | 台湾站点与流媒体：巴哈姆特、KKTV、LINE TV 等 |
| [Amazon](Ruleset/Amazon.list) | Amazon 购物、开发者与广告域名 |
| [ApplePush](Ruleset/ApplePush.list) | Apple 推送服务（APNs） |

## 格式约定

- 文件开头是说明块：名称、说明、策略、规则条数、更新日期。
- 按服务分段，每段以 `# > 服务名` 开头，段与段之间空一行。
- 段内按类型排序：DOMAIN → DOMAIN-SUFFIX → DOMAIN-KEYWORD → … → IP-CIDR → IP-CIDR6 → GEOIP，同类型按字母排序，IP 按数值排序。
- 在 Surge 里引用时建议加 `extended-matching,no-resolve`。
