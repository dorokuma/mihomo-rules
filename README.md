# Mihomo Rules — 分流规则集

Mihomo / Clash Meta 分流规则集，每个服务独立一个文件。

## 规则列表

**ai_rules.yaml** — AI 服务
Grok + Gemini + Claude + ChatGPT（OpenAI）四家 AI 的分流规则，含域名和 IP。

更多规则按需添加，每个服务一个独立文件。

## 使用方式

在 Mihomo 配置中通过 `rule-providers` 引用：

```yaml
rule-providers:
  AI:
    type: http
    behavior: classical
    format: yaml
    url: "https://raw.githubusercontent.com/dorokuma/mihomo-rules/main/ai_rules.yaml"
    interval: 86400

rules:
  - RULE-SET,AI,AI
```

需要引用多个规则时，每个服务对应一个 `rule-providers` 条目和一条 `RULE-SET` 规则。

## 新增规则

需要加新服务时，在仓库根目录新建一个独立的 YAML 文件。

例如新增 Netflix 规则 `netflix_rules.yaml`：

```yaml
payload:
  - DOMAIN-SUFFIX,netflix.com
  - IP-CIDR,1.2.3.4/32,no-resolve
```

然后在 Mihomo 配置中添加对应的引用：

```yaml
rule-providers:
  Netflix:
    type: http
    behavior: classical
    format: yaml
    url: "https://raw.githubusercontent.com/dorokuma/mihomo-rules/main/netflix_rules.yaml"
    interval: 86400

rules:
  - RULE-SET,Netflix,Netflix
```

### 命名规范

- `xxx_rules.yaml` — classical 格式，含域名和 IP 规则
- `xxx_domains.list` — 纯域名列表，用于 behavior: domain

## 覆盖服务

**ai_rules.yaml** 目前包含：
- 🤖 ChatGPT（OpenAI）— 35 条规则
- 🎨 Claude（Anthropic）— 3 条规则
- 🌀 Grok（xAI）— 5 条规则
- ✨ Gemini（Google）— 46 条规则

## 数据来源

- [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- [Accademia/Additional_Rule_For_Clash](https://github.com/Accademia/Additional_Rule_For_Clash)

## 更新

规则集手动维护，数据源上游更新后同步。
