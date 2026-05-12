# Mihomo Rules — AI Services

Grok + Gemini + Claude + ChatGPT（OpenAI）四家 AI 服务的 Mihomo/Clash Meta 分流规则集。

## 规则文件

| 文件 | 格式 | behavior | 说明 |
|------|------|----------|------|
| `ai_rules.yaml` | yaml | classical | AI 服务完整规则集（域名 + IP） |

## 使用方式

在 Mihomo 配置中引用：

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

## 新增规则

在仓库根目录放 YAML 文件，格式和 `ai_rules.yaml` 保持一致：

```yaml
payload:
  - DOMAIN-SUFFIX,example.com
  - IP-CIDR,1.2.3.4/32,no-resolve
```

然后在 Mihomo 配置中添加对应的 `rule-providers` 和 `rules` 条目即可。

### 命名规范

- `xxx_rules.yaml` — classical 格式，含域名和 IP 规则
- `xxx_domains.list` — 纯域名列表，用于 behavior: domain

## 覆盖服务

| 服务 | 标签 | 规则数 |
|------|------|--------|
| 🤖 ChatGPT（OpenAI） | OpenAI | 35 |
| 🎨 Claude（Anthropic） | Claude | 3 |
| 🌀 Grok（xAI） | Grok | 5 |
| ✨ Gemini（Google） | Gemini | 46 |

## 数据来源

- [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- [Accademia/Additional_Rule_For_Clash](https://github.com/Accademia/Additional_Rule_For_Clash)

## 更新

规则集手动维护，数据源上游更新后同步。
