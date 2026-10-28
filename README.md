# Surge 分流规则

自用的 Surge 分流规则集，Clash 通过 Sub-Store 引用同一套规则。

## 引用地址

下载、系统更新等需要强制直连

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Special.list
```

境外网站与服务的代理合集

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Global.list
```

国内网站、国内 CDN 与 Apple 服务

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Domestic.list
```

Apple 推送服务（APNs）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/ApplePush.list
```

YouTube 视频、图片、短链和 App 接口（7 条，策略 YouTube）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/YouTube.list
```

Telegram 域名与官方 IP 段（16 条，策略 Telegram）

```
https://raw.githubusercontent.com/wsc82/Surge/main/Ruleset/Telegram.list
```

QX 格式的副本（Global、Domestic、ApplePush、YouTube、Telegram）在 [wsc82/QuantumultX](https://github.com/wsc82/QuantumultX)，Clash 格式的副本（Global、Domestic、ApplePush、YouTube、Telegram）在 [wsc82/Clash](https://github.com/wsc82/Clash)，每天自动同步，改规则只改这里就行。

## 规则集

| 规则集 | 内容 | 策略 |
| --- | --- | --- |
| [Special](Ruleset/Special.list) | 下载、系统更新等需要强制直连的流量，排在最前面 | DIRECT（直连） |
| [Domestic](Ruleset/Domestic.list) | 国内网站、国内 CDN 与 Apple 服务 | DIRECT（直连） |
| [Global](Ruleset/Global.list) | 境外网站与服务的代理合集 | 备用（当前 Surge 配置未引用） |
| [ApplePush](Ruleset/ApplePush.list) | Apple 推送服务（APNs）域名与官方 IP 段 | 备用（当前 Surge 配置未引用） |
| [YouTube](Ruleset/YouTube.list) | YouTube 视频、图片、短链和 App 接口，7 条 | YouTube |
| [Telegram](Ruleset/Telegram.list) | Telegram 域名与官方 IP 段，16 条 | Telegram |

按 Surge 配置里的匹配顺序，Special 在最前面，Domestic 在其后，然后是内置的 `RULE-SET,LAN`、`GEOIP,CN` 和 `FINAL`。

## 格式约定

- 文件开头是说明块：名称、说明、策略、规则条数、更新日期。
- 按服务分段，每段以 `# > 服务名` 开头，段与段之间空一行。
- 段内按类型排序：DOMAIN → DOMAIN-SUFFIX → DOMAIN-KEYWORD → … → IP-CIDR → IP-CIDR6 → GEOIP，同类型按字母排序，IP 按数值排序。
- 在 Surge 里引用时建议加 `extended-matching,no-resolve`。
