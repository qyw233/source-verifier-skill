
> **本文件由用户和 Agent 共同维护，支持自定义扩展。评估来源时应在分析前读取。**

# 可靠来源名单

记录已知可靠的网站、实体或社交媒体账号。命中该名单的来源默认提高信任基线，但仍需结合具体文章质量和用户提问进行最终判断。

## 使用规则

```text
- 本名单为最高优先级判定依据，命中后不再执行步骤 6（来源类型详细规则逐条检查）
- 在开始逐一评估来源之前，先读取本文件及 reputation_unreliable.md、reputation_disputed.md
- 如果来源的域名/实体/URL 命中本名单 → source_reliability_score 直接设为 85-95 分
- citation_usability 默认设为 usable 或 highly_usable
- 在 reasons 中注明"该来源在可信名单中，为最高优先级判定"
- 仍需检查文章质量（article_quality_score 独立评估）和时效性（freshness）
- 名单优先级：可靠名单 > 争议名单 > 不可靠名单（同时命中以最高优先级为准）
- 如果来源 URL 无法获取但命中本名单 → 可给出较高的初步评估
```

## 格式说明

```text
每行一个条目，格式：类型 | 名称 | 识别条件 | 备注
类型: domain（域名）/ url_pattern（URL模式）/ social_account（社交账号）/ entity（实体名称）
名称: 来源的简要名称
识别条件: 域名、URL 模式、或社交账号标识（平台:用户名）
备注: 简要说明为何可信
```

## 名单
```text
domain | 中国政府网 | gov.cn | 中国政府官方网站
domain | 新华社 | xinhuanet.com | 中国国家通讯社
domain | 人民日报 | people.com.cn | 中国共产党中央委员会机关报
domain | Reuters | reuters.com | 国际权威通讯社
domain | Associated Press | apnews.com, ap.org | 国际权威通讯社
domain | BBC News | bbc.com, bbc.co.uk | 英国公共广播机构
domain | 世界卫生组织 | who.int | 联合国卫生专门机构
domain | IEEE | ieee.org | 国际电气电子工程师学会
domain | ACM | acm.org | 国际计算机学会
domain | Nature | nature.com | 顶级科学期刊
domain | Science | science.org | 顶级科学期刊
domain | GitHub | github.com | 代码托管平台（注意区分官方仓库与个人仓库）
domain | Wikipedia | wikipedia.org | 百科全书（仅作背景参考，不宜作最终证据）
domain | PubMed | pubmed.ncbi.nlm.nih.gov | 生物医学文献数据库
domain | FDA | fda.gov | 美国食品药品监督管理局
domain | NMPA | nmpa.gov.cn | 中国国家药品监督管理局
domain | 中国裁判文书网 | wenshu.court.gov.cn | 中国司法裁判文书官方平台

# === 以下为用户自定义扩展区，可按需添加或修改 ===
# 添加格式：domain | 名称 | 识别条件 | 备注
# 示例：domain | 财新网 | caixin.com | 中国知名财经媒体
```
