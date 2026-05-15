[![English README](https://img.shields.io/badge/README-English-blue)](README.md)
[![简体中文 README](https://img.shields.io/badge/README-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-red)](README.zh-CN.md)

当前语言：简体中文。

> 本仓库提供两个语义对齐、可安装的 Skill 包：[英文版](skills/source-verifier-en) 和 [中文版](skills/source-verifier-zh)。中文版针对中文互联网信息生态、中文信源判断习惯以及中国模型/中文模型工作流，可能有更好的实际效果。

# 信源核实 Skill （Source Verifier skill）

大语言模型正在成为信息获取的主要入口，信源的质量直接影响着模型输出的可靠性。但一个日益突出的问题是：互联网上大量内容并不来自人或机构的审慎撰写，而是由自动化工具批量生成、经内容分发网络广泛扩散的低质文本。它们不追求准确，只追求被模型抓取和引用。

2026年的一项公开调查展示了一个典型案例：借助售价低廉的软件工具，一款完全虚构的产品被包装为"行业第一"，连同伪造的技术参数、用户评价和排名数据，在数小时内进入了主流AI搜索的推荐结果。这并非孤立的漏洞利用，而是一条名为"生成式引擎优化"（Generative Engine Optimization, GEO）的产业链——通过向网络批量投放定向设计的文本，影响大语言模型在检索增强生成过程中对信源的信任权重。第三方机构核查发现，在特定领域的AI搜索返回结果中，近三成参考链接属于此类定向投放内容。当这些文本在语义上彼此印证、在数量上占优，便形成了一种"虚假的共识"：看似多方报道，实则同一模板的循环引用。

上述现象引出一个朴素而紧迫的问题：**如何判断一个来源是否值得相信？**

本 Skill 即为此而设计。它提供了一套系统化的信源评估框架，判断某个网页信息来源的类型、可靠性、内容质量及引用价值。工作范围涵盖：

- 信源收集与整理
- 来源类型识别（官方 / 学术 / 新闻 / 社交 / 自媒体 / 博客论坛 / 聚合站 / 可疑来源）
- 来源实体可靠性与单篇文章质量的分开评估
- 时效性判断
- 多来源冲突处理
- 跨区域 / 跨语言信息溯源验证
- 输出信源评估报告或来源评估结果
- 基于核实后的可靠信源回答用户提问

因此，本 Skill 优先回答一个问题：**这个来源是否足以支撑当前问题下的具体结论？**

## 适用场景

- 检查搜索结果、网页链接或引用列表的可靠性
- 在 Claude Code、Codex、OpenCode，OpenClaw（龙虾）及其衍生 Agent 以及 Hermes Agent 等支持 Skill 的 Agent 环境中，作为搜索、研究、写报告前的信源核实 Skill
- 为 Dify、LangGraph、CrewAI 等流程增加信源检查节点
- 评估新闻、科技发布、论文、政策、医疗等高时效或高风险信息

## 不适用场景

- 只想做通用搜索，不关心来源质量
- 需要法律、医疗、金融等专业意见的最终裁决
- 没有任何 URL、来源名称、搜索结果或可核查材料
- 需要判断事实真伪，但无法访问原始证据或上下文

## 快速开始

安装或启用本 Skill 后，直接向模型提出信源核实任务即可。用户不需要手动指定读取哪些规则文件；模型会根据 `SKILL.md` 的流程自动加载对应规则。

### 基本用法

```text
请使用 source-verifier 评估以下来源是否可靠，并回答我的问题：

问题：某视频生成模型是不是已经开源？

来源：
1. https://official.example.com/blog/model-release
2. https://news.example.com/ai/model-open-source
```

模型会自动识别来源类型，区分来源实体可靠性和文章质量，检查时效性、转载、二手转述、跨语言传播和多来源冲突风险，然后基于可靠来源回答问题。

### 只评估来源

如果只想标记来源质量，不需要模型回答原问题，可以明确说明：

```text
请只对以下链接做信源可靠性评估，不需要回答原问题：

问题：某视频生成模型是不是已经开源？

来源：
1. https://official.example.com/blog/model-release
2. https://news.example.com/ai/model-open-source
```

### 结合搜索工具使用

更常见的用法是先让模型搜索或收集来源，再强制整理所有来源并调用本 Skill 核实：

```text
帮我查找某视频生成模型是否已经开源。

请先利用可用的搜索工具收集来源，不要直接下结论。
然后整理所有找到的信源网站，使用 source-verifier 对每个来源进行可靠性核查。
最后只基于通过核实的可靠来源回答问题。
```

如果已经有搜索结果，也可以直接提供标题、URL 和摘要：

```text
请核实下面这些搜索结果的来源质量，筛掉不适合作为引用的来源，并基于可靠来源回答问题：

问题：某视频生成模型是不是已经开源？

搜索结果：
1. 标题：模型发布公告
   URL：https://official.example.com/blog/model-release
   摘要：我们发布了新的视频生成模型。

2. 标题：某公司开源视频模型
   URL：https://news.example.com/ai/model-open-source
   摘要：媒体称该模型已经开源。
```

### 自定义信誉名单和领域规则

如果你对某些媒体、机构、账号或专业领域有更细的判断，可以让模型直接维护本 Skill 的信誉名单和领域规则。这样后续评估会自动应用你的本地知识，而不需要每次在提示词里重复说明。

信誉名单可以记录可靠、不可靠和争议来源，条目支持域名、URL 模式、社交账号或实体名称。

```text
请把以下来源加入 source-verifier 的信誉名单：

可靠来源：
- domain | 示例官方机构 | example.gov | 某领域官方发布渠道

不可靠来源：
- domain | 示例采集站 | scraper.example | 长期搬运、无作者、无原始来源

争议来源：
- domain | 示例争议媒体 | disputed.example | 有明显立场偏向，事实报道需交叉验证
```

也可以扩展特定领域规则：

```text
请为 source-verifier 增加一个金融投资领域规则。

要求：
- 涉及股票、基金、加密货币、理财产品时触发
- 优先使用监管机构公告、交易所文件、上市公司公告、基金招募说明书
- 自媒体、社群截图、带单内容只能作为线索
- 对收益承诺、内幕消息、价格预测自动降权
```

相关文件：

```text
rules/reputation_trusted.md      可靠来源名单
rules/reputation_unreliable.md   不可靠来源名单
rules/reputation_disputed.md     争议来源名单
rules/00_topic_registry.md       领域规则注册表
rules/source_<domain>.md         自定义领域规则
```

信誉名单只影响来源实体的可信基线，不代表当前页面一定能支撑用户问题。即使来源命中可靠名单，仍需独立评估文章质量、相关度、时效性和具体 claim 的证据强度。


## 输出方式

本 Skill 有两种输出方式，二者的格式要求不同：

1. **默认模式：信源评估报告 + 回答**  
   适合用户希望核实来源并得到最终答案的场景。报告格式暂不做严格约束，模型可根据用户问题、来源数量和冲突情况自行组织。输出应包含：
   - 各来源的可靠性判断和主要风险
   - 哪些来源可以引用，哪些只能作为线索，哪些不建议使用
   - 多来源之间是否存在冲突、转载、洗稿或共同上游
   - 基于可靠来源得出的回答
   - 证据不足时的不确定性说明

2. **仅评估模式：只输出评估结果**  
   当用户明确要求"只评估来源""只标记""不需要回答问题"时启用。该模式应输出结构化评估结果，便于后续工作流读取或复用。

   单个来源的评估结果应包含 `schemas/source_report.schema.json` 中定义的核心字段：

   ```text
   user_question              用户问题
   url                        来源 URL
   domain                     主域名
   title                      页面标题
   source_type                来源类型
   relevance_to_question      与问题的相关度
   source_reliability_score   来源实体可靠性评分
   article_quality_score      当前页面质量评分
   citation_usability         引用可用性
   freshness                  时效性
   reasons                    评分原因
   warnings                   风险提示
   recommended_action         建议动作
   ```

   如果用户问题被拆成多个 claim，或需要汇总多个来源对同一问题的支持情况，可以输出问题级证据包，结构参考 `examples/example_evidence_pack.json`。

## 核心原则

> **数量 != 质量，重复 != 验证。**

1. **信源实体可靠性** 与 **单篇文章质量** 必须分开评估。
2. 没有权威一手来源支撑的说法，即使被许多二手来源重复，也不能视为多方独立验证。
3. 官方来源、论文、法规原文、标准文件、项目仓库通常优先级更高。
4. 多个来源说法一致，只有在至少存在一个权威一手来源、来源之间没有转载或洗稿关系、且各自独立获取信息时，才可以作为有效交叉验证。
5. 社交平台、论坛、自媒体通常只能作为线索，不能单独支撑高风险结论。
6. 跨语言报道如果没有引用原产地语言的一手来源，应自动降权。
7. 输出结果必须说明原因，不能只给分数。

## 来源类型

`source_type` 当前支持：

```text
official                 官方来源
academic                 学术来源
news                     新闻媒体
professional_analysis    专业分析、行业报告、智库或机构研究
blog_forum               博客、论坛、社区问答
social_media             社交平台内容
self_media               自媒体、个人 IP 或小团队内容
aggregator_or_scraper    聚合站、采集站、搬运站
suspicious               可疑来源
unknown                  无法判断
```

最小规则路由：

```text
official              -> rules/source_official.md
academic              -> rules/source_academic.md
news                  -> rules/source_news.md
professional_analysis -> rules/01_general_scoring.md + 主题规则
blog_forum            -> rules/source_blog_forum.md
social_media          -> rules/source_social.md
self_media            -> rules/source_self_media.md
aggregator_or_scraper -> rules/00_source_taxonomy.md + rules/source_suspicious.md
suspicious            -> rules/source_suspicious.md
```

主题规则按 `rules/00_topic_registry.md` 加载，例如：

```text
AI / 科技 -> rules/source_ai_tech.md
医疗健康  -> rules/source_medical.md
法律政策  -> rules/source_law_policy.md
```

## 运行流程

详细流程见 `SKILL.md`。简化流程如下：

```text
1. 收集用户问题、URL、搜索结果或引用列表
2. 规范化 URL，提取域名、标题、作者、发布时间、正文摘要
3. 判断信息原产地语言，识别跨语言二手传播风险
4. 读取信誉名单，设置来源实体的初始可信基线
5. 判断来源类型，加载对应规则
6. 评估文章质量、相关度、时效性和引用可用性
7. 处理多来源冲突，优先采用证据强度而非来源数量
8. 输出信源评估报告或来源评估结果
9. 基于通过验证的来源回答用户问题
```

## 目录结构

```text
source-verifier-zh/
├─ README.md                              # 项目说明
├─ SKILL.md                               # Skill 定义与完整执行流程
├─ VERSION                                # 版本号
├─ rules/
│  ├─ 00_source_taxonomy.md               # 来源类型分类规则
│  ├─ 00_topic_registry.md                # 主题特殊规则注册表
│  ├─ 01_general_scoring.md               # 通用评分规则
│  ├─ 03_freshness.md                     # 时效性判断规则
│  ├─ 04_conflict_resolution.md           # 多来源冲突处理规则
│  ├─ 05_cross_region_verification.md     # 跨区域 / 跨语言溯源验证规则
│  ├─ reputation_trusted.md               # 可靠来源信誉名单
│  ├─ reputation_unreliable.md            # 不可靠来源信誉名单
│  ├─ reputation_disputed.md              # 争议来源信誉名单
│  ├─ source_official.md                  # 官方来源专项规则
│  ├─ source_academic.md                  # 学术来源专项规则
│  ├─ source_news.md                      # 新闻媒体专项规则
│  ├─ source_social.md                    # 社交平台专项规则
│  ├─ source_self_media.md                # 自媒体专项规则
│  ├─ source_blog_forum.md                # 博客论坛专项规则
│  ├─ source_suspicious.md                # 可疑来源专项规则
│  ├─ source_ai_tech.md                   # AI / 科技主题规则
│  ├─ source_medical.md                   # 医疗健康主题规则
│  └─ source_law_policy.md                # 法律政策主题规则
├─ prompts/
│  └─ evaluate_source.prompt.md           # 单来源评估 Prompt 模板
├─ schemas/
│  └─ source_report.schema.json           # 仅评估模式的单来源结果 Schema
└─ examples/
   ├─ example_input.json                  # 结构化输入样例（开发者参考）
   └─ example_evidence_pack.json          # 仅评估模式的问题级证据包样例
```

## 示例：排除被污染的搜索结果

下面是一个真实使用场景：同一个问题、同一批网页端搜索信源，在未做信源核实和使用本 Skill 核实后，得到的结论明显不同。

原始问题为中文询问grok2的参数量，即：

```text
Grok-2 的参数量是多少？
```

DeepSeek 网页端快速模式搜索结果：[https://chat.deepseek.com/share/j7ou83xvm9ib30i7tt](https://chat.deepseek.com/share/j7ou83xvm9ib30i7tt)
结论如下：
```text
Grok-2 的总参数量约为 905B（9050 亿），激活参数约为 136B。
```

这个结论的问题在于：中文某个影响力较大的媒体给出了缺少原始来源支撑的 905B 说法，随后多个中文媒体、聚合站和转载站继续扩散，导致搜索结果中出现"很多来源都这么说"的假象。

之后使用 DeepSeek V4 Flash 结合 OpenCode，提取 DeepSeek 网页端使用过的同一批信源，并调用本 Skill 进行核实。生成报告结论如下：

```text
Grok-2 的参数量无官方确认数字。
基于对开源权重的技术分析，总参数约 269B（2690 亿），激活参数约 115B（1150 亿）。
媒体报道的 905B（9050 亿）说法无官方来源支撑，不可靠。
```

本 Skill 在这个案例中发挥的作用是：

- 识别 905B 说法主要来自中文媒体转载链，而不是官方或技术原始来源。
- 判断多个转载来源内容高度重合，不能算作独立交叉验证。
- 发现 xAI / Hugging Face 官方仓库没有公布 Grok-2 参数量，因此不能断言官方确认了某个数字。
- 将更强证据来源优先级提高：DataLearner、Unsloth、Ollama 等技术来源基于开源权重、模型配置或 metadata，指向约 269B-270B 总参数。

这个例子展示了本 Skill 的核心价值：基于鱼龙混杂的搜索结果，识别转载污染、区分一手来源与二手扩散、排除干扰项，使得 AI 搜索从"看起来很多来源都这么说"变成"哪些来源真正能支撑结论"。

## 已知限制

- 本 Skill 主要指导 Agent 在已经获得搜索结果、网页链接或候选信源后进行分析和核实；它不负责指导 Agent 如何设计更有效的主动搜索策略。
- 使用效果仍然依赖输入信源的质量。如果搜索工具返回的来源本身很差、覆盖不全或缺少一手来源，本 Skill 仍有一定概率得出错误或不完整的结论。因此，高风险问题应优先使用更好的搜索工具，并主动补充官方、一手、法规、论文、标准、代码仓库或原始数据来源。
- 本 Skill 只能根据信源类型、来源实体、文章质量、时效性、证据链和冲突情况做初步评估。即使某个来源较权威，也不保证其具体说法一定正确；最终判断和决策仍需由用户自行承担。本 Skill 会尽量提示每个来源特别需要注意的风险点。
- 医疗、法律、金融、教育、电商等专业领域规则目前主要是占位和通用约束，作者并不熟悉所有细分领域。用户应根据自己的专业知识修改 `rules/00_topic_registry.md` 和对应 `rules/source_<domain>.md`。
- 页面无法抓取时只能做基于域名和已知信息的初步判断，不能替代正文级核实。

## 版本

当前版本：`0.1`



