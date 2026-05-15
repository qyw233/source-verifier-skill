
> **本文件由用户和 Agent 共同维护，支持自定义扩展。评估来源时应在分析前读取。**

# 不可靠来源名单

记录已知不可靠的网站、实体或社交媒体账号。命中该名单的来源应大幅降权或直接弃用，除非有强力的其他独立来源印证。

## 使用规则

```text
- 本名单为最高优先级判定依据，命中后不再执行步骤 6（来源类型详细规则逐条检查）
- 在开始逐一评估来源之前，先读取本文件及 reputation_trusted.md、reputation_disputed.md
- 如果来源的域名/实体/URL 命中本名单 → source_reliability_score 直接设为 0-20 分
- citation_usability 直接设为 not_recommended 或 do_not_use（根据严重程度）
- 在 warnings 中注明"该来源在不可靠名单中，为最高优先级不可靠判定"
- 即使来源命中本名单，也不应自动忽略——仍需记录并标注原因，以供用户了解信息来源的全貌
- 如果来源 URL 无法获取且命中本名单 → citation_usability 直接设为 do_not_use
- 名单优先级：可靠名单 > 争议名单 > 不可靠名单（同时命中以最高优先级为准）
```

## 格式说明

```text
每行一个条目，格式：类型 | 名称 | 识别条件 | 备注
类型: domain（域名）/ url_pattern（URL模式）/ social_account（社交账号）/ entity（实体名称）
名称: 来源的简要名称
识别条件: 域名、URL 模式、或社交账号标识（平台:用户名）
备注: 简要说明为何不可靠
```

## 名单

```text
# 示例条目（可按需取消注释或自行添加）：
# domain | 示例假新闻站 | fake-news.example.com | 已知传播虚假信息
# social_account | 示例造谣账号 | X:fake_user_123 | 多次发布未经证实的虚假消息

# === 用户自定义扩展区，请按需添加 ===
# 添加格式：类型 | 名称 | 识别条件 | 备注
# 示例：
# domain | 某内容农场 | example-farm.com | 洗稿、SEO垃圾、无原创内容
# social_account | 某营销号 | weibo:1234567890 | 长期发布虚假营销信息
# entity | 某已知伪科学组织 | - | 传播伪科学，被多家权威机构警告
```
