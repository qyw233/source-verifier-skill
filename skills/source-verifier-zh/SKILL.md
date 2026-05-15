---
name: source-verifier-zh
description: "Evaluates reliability of web information sources and answers user questions based on verified sources. Determines source type (official/academic/news/social_media/self_media/blog_forum), assesses domain authority, article quality, timeliness, and resolves source conflicts. Outputs structured citation usability reports and verified answers. USE FOR: source verification, check source reliability, verify web sources, fact-check sources, evaluate citation quality, source credibility assessment, inspect URL authority, cross-reference sources, answer questions with source verification. DO NOT USE FOR: general web search without source evaluation."
license: MIT
metadata:
  author: qyw233
  version: "0.1"
---

# 信源核实 Skill

## 目标

核实所提供的网络信息来源是否可靠，判断这些来源的权威度、真实性和质量，并基于可靠信源回答用户提问。

本 Skill 关注的是：

- 信源收集与整理
- 来源类型识别
- 信源可靠性评估
- 文章质量评估
- 时效性判断
- 多来源冲突处理
- 生成给大模型或用户参考的信源评估报告
- 基于核实后的可靠信源，回答用户的原始提问

## ⚠️ 核心铁律：数量≠质量，重复≠验证

**这是本 Skill 最重要的原则，贯穿所有评估步骤，任何时候不得违反。**

```text
没有权威信源支撑的说法，即使被再多的来源重复传播，也绝不能视为"多方独立验证"。
数量再多也无法提升可信度等级——

特别是：
  - 一般媒体（第二级、第三级媒体）
  - 自媒体（任何类型）
  - 社交平台普通用户
  - 博客论坛
  - 内容聚合站、搬运号

这些来源的可信度永远不能给到"高"（citation_usability 最高不超过 use_with_caution），
无论它们有多少个、说法多么一致。

"多个来源说法一致"只有在以下条件同时满足时才能视为有效多方验证：
  1. 至少有一个权威一手来源（官方/学术/高信誉第一级媒体）独立确认
  2. 各来源之间不存在互相引用、洗稿、转载关系
  3. 各来源独立获取信息，而非来自同一个上游消息源

否则，"数量多"恰恰是洗稿/搬运/病毒式传播的警示信号，而非可信度的加分项。
```

## 工作模式

### 默认模式：信源核实 + 解答

核实所有来源后，基于通过验证的可靠信源，直接回答用户的问题。输出包含两部分：信源评估报告 + 基于可靠来源的答案。模型可自行判断如何组织答案格式。

### 仅标记模式

仅对信源进行分类和可信度标记，不做解答。仅当用户明确要求"只标记""只分类""不需要答案"等时启用。

## 触发条件

当任务涉及以下情况时，应调用本 Skill：

- 用户要求核实网络搜索结果的来源可靠性
- 用户要求判断引用是否可靠
- 用户要求检查某个网页是否能作为参考
- 用户要求比较多个来源可信度
- 用户要求评估信源风险
- 用户问题属于新闻、医疗、政策、金融、科技发布等高时效或高风险领域

## 总体流程

0. **收集与整理信源**：在核实之前，首先整理当前对话上下文中所有可用信源：
   - 根据用户指令收集整理来自之前搜索工具（web search）、API、MCP 工具、或已加载 skill 检索到的结果
   - 或者用户手动提交的 URL 或来源引用
   - 将来源统一整理为待核实列表，不遗漏任何可用来源
1. 读取用户的原始提问（User Question）、URL 列表或搜索结果。往往来源于之前的检索，或者用户直接提供的链接，首先需要对输入进行规范化处理，确保 URL 格式正确，提取出域名、路径等关键信息。一次性有多个 URL 时，需要对每个 URL 进行独立处理，生成独立对应的信源评估报告。
1.5. **使用 `rules/05_cross_region_verification.md` 进行跨区域/跨语言溯源分析**：从用户提问中判断信息原产地语言（English-origin / Chinese-origin / 其他），设定后续评估的跨语言基线。此步骤在评估各 URL 之前执行，其输出影响后续所有评分规则中的跨语言降权判断，并为冲突解决阶段提供信息茧房检测依据。
2. 对每个 URL 做标准化处理：
   - 去除 `utm_*` 等追踪参数
   - 识别主域名
   - 尝试获取标题、正文摘要、作者、发布时间、更新时间
   - 检查重定向、镜像、转载、404 等情况
3. **当页面无法正常获取时**（包括但不限于：网络超时、传输错误、返回 403/404、仅返回极少量文本如只有一个标题、需要登录才能查看、页面依赖 JS 渲染导致纯文本抓取无法获取有效内容），不得跳过该 URL，必须基于已有信息（域名、URL 路径结构、已知的域名背景）给出**初步判断**（preliminary assessment），同时输出详细的 `warnings` 明确标注缺失信息。初步判断规则：
    - 仍可基于域名判断 `source_type`（如已知 shlab.org.cn 是上海人工智能实验室官网，即使无法抓取也属于 `official`）
    - `article_quality_score` 标记为无法评估，给出最低可用分数并附说明
    - `citation_usability` 默认不超过 `use_with_caution`
    - `freshness` 标记为 `unknown`
    - `warnings` 中必须逐条列出未能获取到的信息项（标题、作者、发布时间、正文摘要等），以及无法评估的原因（如"纯文本抓取仅返回标题，无法获取正文内容""目标服务器连接超时，未获取到任何页面内容"）
    - `reasons` 中必须注明"基于域名的初步判断，未经页面内容验证"
3.5. **信誉名单预检（最高优先级）**：在进入来源分类和评分之前，先读取以下三个信誉名单文件，检查每个 URL 的域名/实体/社交账号是否命中：
    - `rules/reputation_trusted.md` —— 可靠来源名单
    - `rules/reputation_unreliable.md` —— 不可靠来源名单
    - `rules/reputation_disputed.md` —— 争议来源名单
    命中名单的来源，直接按名单规则设定 `source_reliability_score` 和 `citation_usability`，**跳过步骤 6 的逐条详细规则检查**（文章质量评分和时效性仍需独立评估）。名单优先级为：可靠 > 争议 > 不可靠（同时命中以高优先级为准）。三个文件均由用户和 Agent 共同维护，支持细粒度到具体社交账号的自定义扩展。未命中任何名单的来源正常进入后续流程。
4. 使用 `rules/00_source_taxonomy.md` 判断来源类型。
5. 使用 `rules/01_general_scoring.md` 进行通用评分。
6. 对**未命中信誉名单**的来源，根据来源类型加载对应规则，不仅仅是以下列出的，需要仔细检查 `rules/` 目录下的所有规则文件：
   - 官方来源 → `rules/source_official.md`
   - 学术来源 → `rules/source_academic.md`
   - 新闻媒体 → `rules/source_news.md`
   - 社交平台（先判断是否自媒体，若是则终止并切换） → `rules/source_social.md`
   - 自媒体 → `rules/source_self_media.md`
   - 博客论坛 → `rules/source_blog_forum.md`
   - 可疑来源 → `rules/source_suspicious.md`
   - 购物平台 → `rules/source_commerce.md`
6.5. **漏网之鱼复查**：在完成所有来源的评估后，回头检查所有来源中是否有应命中信誉名单但被遗漏的条目（例如域名匹配但未识别、社交账号别名未收录等）。若发现遗漏，将其补充到对应名单文件中，确保下次不再遗漏。
7. 读取 `rules/00_topic_registry.md`，根据用户提问中涉及的主题（如 AI/科技、医疗健康、法律政策等），加载注册表中对应的主题特殊规则文件进行叠加评估。注册表支持用户自定义扩展，详见注册表文件。
8. 使用 `rules/03_freshness.md` 判断来源是否过时。
9. 使用 `rules/04_conflict_resolution.md` 解决来源冲突。
10. 输出符合 `schemas/source_report.schema.json` 的报告。
11. **（默认模式）回答用户提问**：完成信源核实后，结合用户原始提问生成详细报告给出答案。默认整理出详细的报告，对信源进行评估分类详细分析，该模式下不需要展示每个信源的完整标签，某些特别需要引发的注意需要在报告中体现，但是所有信源在按照观点或者信源种类分类的情况下全部包括，最后回答用户问题。

## 输出原则

输出时必须区分：

```text
来源实体（域名/机构）是否可靠
文章本身（内容/证据）质量如何
页面内容是否与用户提问高度相关
该来源是否适合作为解答该问题的最终引用
```

不要只输出一个总分。

## 推荐标签

### 来源类型

```text
official
academic
news
professional_analysis
blog_forum
social_media
self_media
aggregator_or_scraper
suspicious
```

### 引用可用性

```text
highly_usable
usable
use_with_caution
not_recommended
do_not_use
```

## 最终回答约束

当信源可靠性较低或证据不足时，不要输出确定性结论。

应使用类似表达：

```text
该来源可信度一般。
该说法缺少权威原始来源支持。
目前只能基于现有非官方来源进行评估。
多个二手来源重复该说法，但尚未找到官方或一手证据。
```