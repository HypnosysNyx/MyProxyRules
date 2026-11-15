# MyProxyRules

个人维护的代理分流规则仓库，面向 Egern、Clash / Mihomo 使用。

**仓库地址：** https://github.com/HypnosysNyx/MyProxyRules  
规则文件通过 GitHub Raw 地址提供，可供客户端下载和更新。

## 规则集目录

| 规则集 | Egern | Clash / Mihomo | 指定策略组 | 规则数 |
|---|---|---|---|---:|
| Siri AI | `Egern/Siri-AI.list` / `Egern/Siri-AI.yaml` | `Clash/Siri-AI.yaml` | Proxy | 21 |
| Apple Music | `Egern/AppleMusic补充.list` / `Egern/AppleMusic补充.yaml` | `Clash/AppleMusic补充.yaml` | Apple中国 | 6 |
| Google | `Egern/Google补充.list` / `Egern/Google补充.yaml` | `Clash/Google补充.yaml` | Google手动 | 12 |
| YouTube | `Egern/YouTube补充.list` / `Egern/YouTube补充.yaml` | `Clash/YouTube补充.yaml` | Google手动 | 6 |
| Crypto | `Egern/Crypto补充.list` / `Egern/Crypto补充.yaml` | `Clash/Crypto补充.yaml` | 金融消费 | 9 |
| Mail | `Egern/Mail补充.list` / `Egern/Mail补充.yaml` | `Clash/Mail补充.yaml` | 全球手动 | 4 |
| 机场 | `Egern/机场.list` / `Egern/机场.yaml` | `Clash/机场.yaml` | 金融消费 | 2 |
| 国内镜像 | `Egern/国内镜像.list` / `Egern/国内镜像.yaml` | `Clash/国内镜像.yaml` | 国内网站 | 3 |

当前共 **8 组规则、63 条规则**。

每组提供三种格式：
- **Egern Surge Rule Set**：`.list`，可在 Egern 的 Tools → Rules → + → Rule Set 中添加。
- **Egern 原生 Rule Set**：`.yaml`，通过配置中的 `rule_set` 引用。
- **Clash / Mihomo Rule Provider**：`payload` YAML，使用 `behavior: classical`、`format: yaml` 加载。

规则文件只保存匹配条件；策略组绑定在客户端主配置中。请确保表格中的策略组名称与你的客户端配置完全一致。

## Clash / Mihomo 配置示例

将以下内容合并到现有配置的 `rule-providers:` 下：

```yaml
rule-providers:
  SiriAI:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/Siri-AI.yaml
    path: ./ruleset/Siri-AI.yaml
    interval: 86400
    behavior: classical
    format: yaml
  AppleMusicExtra:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/AppleMusic%E8%A1%A5%E5%85%85.yaml
    path: ./ruleset/AppleMusic补充.yaml
    interval: 86400
    behavior: classical
    format: yaml
  GoogleExtra:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/Google%E8%A1%A5%E5%85%85.yaml
    path: ./ruleset/Google补充.yaml
    interval: 86400
    behavior: classical
    format: yaml
  YouTubeExtra:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/YouTube%E8%A1%A5%E5%85%85.yaml
    path: ./ruleset/YouTube补充.yaml
    interval: 86400
    behavior: classical
    format: yaml
  CryptoExtra:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/Crypto%E8%A1%A5%E5%85%85.yaml
    path: ./ruleset/Crypto补充.yaml
    interval: 86400
    behavior: classical
    format: yaml
  MailExtra:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/Mail%E8%A1%A5%E5%85%85.yaml
    path: ./ruleset/Mail补充.yaml
    interval: 86400
    behavior: classical
    format: yaml
  Airport:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/%E6%9C%BA%E5%9C%BA.yaml
    path: ./ruleset/机场.yaml
    interval: 86400
    behavior: classical
    format: yaml
  ChinaMirrors:
    type: http
    url: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Clash/%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F.yaml
    path: ./ruleset/国内镜像.yaml
    interval: 86400
    behavior: classical
    format: yaml
```

将以下规则合并到现有 `rules:` 列表中。**建议放在原有 DST-PORT 80/443 规则之前；原有 DST-PORT 规则和 MATCH 不要删除或改写，MATCH 继续保持最后。**

```yaml
rules:
  - RULE-SET,SiriAI,Proxy
  - RULE-SET,AppleMusicExtra,Apple中国
  - RULE-SET,GoogleExtra,Google手动
  - RULE-SET,YouTubeExtra,Google手动
  - RULE-SET,CryptoExtra,金融消费
  - RULE-SET,MailExtra,全球手动
  - RULE-SET,Airport,金融消费
  - RULE-SET,ChinaMirrors,国内网站
```

## Egern 配置示例

将以下规则合并到 Egern Profile.yaml 的 `rules:` 中。策略组名称按表格指定：

```yaml
rules:
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/Siri-AI.yaml
      policy: Proxy
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/AppleMusic%E8%A1%A5%E5%85%85.yaml
      policy: Apple中国
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/Google%E8%A1%A5%E5%85%85.yaml
      policy: Google手动
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/YouTube%E8%A1%A5%E5%85%85.yaml
      policy: Google手动
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/Crypto%E8%A1%A5%E5%85%85.yaml
      policy: 金融消费
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/Mail%E8%A1%A5%E5%85%85.yaml
      policy: 全球手动
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/%E6%9C%BA%E5%9C%BA.yaml
      policy: 金融消费
      update_interval: 86400
  - rule_set:
      match: https://raw.githubusercontent.com/HypnosysNyx/MyProxyRules/main/Egern/%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F.yaml
      policy: 国内网站
      update_interval: 86400
```

也可以在 Egern 的 Tools → Rules → + → Rule Set 中添加对应的 `.list` 文件，并为规则集选择对应策略组。

## Siri AI 更新

Siri AI 规则已包含新增域名：
```
DOMAIN-SUFFIX,apple-relay.fastly.net
```
并已同步到 Egern Surge、Egern 原生 YAML 和 Clash / Mihomo 三种格式。

## 主配置保留约定

本规则仓库不包含客户端主配置。以下项目在你的主配置中按要求保持原样：
- `ipa.store`
- `28.0.0.1/8`、`198.18.0.0/15`、`fc00::/18`
- `GEOSITE,category-public-tracker`
- 13 个下载进程名
- 12 个代理工具进程名
- `DST-PORT` 80/443
- `MATCH`

## 维护约定

- Egern 与 Clash / Mihomo 两套规则同步维护。
- 保留规则的域名、IP、规则类型及 `no-resolve` 参数。
- 新增规则时检查重复项，并同步更新三种客户端格式和本 README。
- 策略组名称写在集成配置示例中，不硬编码到规则 payload。
