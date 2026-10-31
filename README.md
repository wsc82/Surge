# Surge 分流规则

自用的 Surge 分流规则集，Clash 通过 Sub-Store 引用同一套规则。

## 引用地址

Apple 推送服务（APNs）（12 条）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/ApplePush.list
```

Telegram 域名与官方 IP 段（25 条，策略 Telegram）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Telegram.list
```

YouTube 视频、图片、短链和 App 接口（10 条，策略 YouTube）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/YouTube.list
```

Cursor、Grok、Muse、OpenAI、Perplexity 与 X（Twitter）（57 条，策略 AI）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/AI.list
```

境外网站与服务的代理合集（454 条）。Global 也包含 Telegram、YouTube、AI 分段（Quantumult X 单独使用 Global）。

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Global.list
```

国内网站、国内 CDN 与 Apple 服务（497 条）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Domestic.list
```

QX 格式的副本（Global、Domestic、ApplePush、YouTube、Telegram、AI）在 [wsc82/QuantumultX](https://github.com/wsc82/QuantumultX)，Clash 格式的副本（Global、Domestic、ApplePush、YouTube、Telegram、AI）在 [wsc82/Clash](https://github.com/wsc82/Clash)，每天自动同步，改规则只改这里就行。

## 规则集

| 规则集 | 内容 | 策略 |
| --- | --- | --- |
| [ApplePush](Ruleset/ApplePush.list) | Apple 推送服务（APNs）域名与官方 IP 段，12 条 | |
| [Telegram](Ruleset/Telegram.list) | Telegram 域名与官方 IP 段，25 条 | Telegram |
| [YouTube](Ruleset/YouTube.list) | YouTube 视频、图片、短链和 App 接口，10 条 | YouTube |
| [AI](Ruleset/AI.list) | Cursor、Grok、Muse、OpenAI、Perplexity 与 X（Twitter），57 条 | AI |
| [Domestic](Ruleset/Domestic.list) | 国内网站、国内 CDN 与 Apple 服务，497 条 | DIRECT（直连） |
| [Global](Ruleset/Global.list) | 境外网站与服务的代理合集，也包含 Telegram、YouTube、AI 分段，454 条 | Self |

按 Surge 配置里的匹配顺序，Apple 推送服务、Telegram、YouTube、AI、Global（Self）和 Domestic（直连），然后是内置的 `RULE-SET,LAN`、`GEOIP,CN` 和 `FINAL`。AI 是独立规则，策略组 AI，排在 YouTube 之后、Global 之前。

```
RULE-SET,https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Telegram.list,Telegram,extended-matching,no-resolve
RULE-SET,https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/YouTube.list,YouTube,extended-matching,no-resolve
RULE-SET,https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/AI.list,AI,extended-matching,no-resolve
RULE-SET,https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Global.list,Self,extended-matching,no-resolve
RULE-SET,https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Domestic.list,DIRECT,extended-matching,no-resolve
RULE-SET,LAN
GEOIP,CN
FINAL
```

## 格式约定

- 文件开头是说明块：名称、说明、策略、规则条数、更新日期。
- 按服务分段，每段以 `# > 服务名` 开头，段与段之间空一行。
- 段内按类型排序：DOMAIN → DOMAIN-SUFFIX → DOMAIN-KEYWORD → … → IP-CIDR → IP-CIDR6 → GEOIP，同类型按字母排序，IP 按数值排序。
- 在 Surge 里引用时建议加 `extended-matching,no-resolve`。
