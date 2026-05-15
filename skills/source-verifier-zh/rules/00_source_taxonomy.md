
> **阅读本文件前必须先阅读 SKILL.md 以了解完整任务上下文。**

# 信息来源分类规则

本文件用于判断一个来源属于哪种类型。每个来源必须有一个主类型，可以额外添加多个次级标签。

## 主类型

### 1. official：官方来源

来自原始组织、公司、政府机构、项目团队、标准组织、作者本人或产品维护方的来源。

判断 official 的核心问题不是“这个实体是什么类型”，而是“**对于用户当前要查的这个信息，谁是它的原始发布者 / 维护方？**” 只要该实体自己就是信息的原创生产者，且用户访问的是该实体直接发布的页面，就是 official。

例子：

- 公司官网公告
- 政府网站
- 官方文档
- 官方 GitHub 仓库
- 官方 release note
- Hugging Face 官方模型页
- 标准组织文件
- 项目维护者发布的原始说明
- 基准评测项目官网（如某个 benchmark 项目的官方站点——对于该评测分数而言是 official）
- 独立研究机构的官方数据平台（如 Epoch AI 的官方 benchmark 数据库——对于 AI 能力数据而言是 official）

默认信任等级：A

注意：official 只代表“该数据存在官方原始发布方，信息可追溯”，不代表数据结论本身正确。benchmark 可能存在方法缺陷、数据污染，厂商自评可能存在选择性评测。official 回答“信息从哪来”，不回答“信息是否成立”。

---

### 2. academic：学术来源

论文、预印本、学术数据库、大学页面、出版社页面或 DOI 页面。

例子：

- arXiv
- IEEE
- ACM
- Springer
- Elsevier
- Nature / Science / Cell 系列
- 大学机构知识库
- DOI landing page

默认信任等级：A 或 B

需要区分：

- 同行评审论文：较强
- 预印本：有价值，但未必经过同行评审
- 会议海报、PPT、实验室博客：证据强度较低

---

### 3. news：新闻媒体

新闻机构、科技媒体、财经媒体、专业报道平台。

例子：

- Reuters
- AP
- BBC
- The Verge
- TechCrunch
- 财新

默认信任等级：B 或 C，取决于媒体信誉、文章质量和是否链接原始来源。

---

### 4. professional_analysis：专业分析来源

专业机构、行业报告、智库、咨询公司、技术团队博客等。

例子：

- Gartner
- McKinsey
- Forrester
- 研究机构报告
- 企业工程博客
- 专业技术分析文章

默认信任等级：B 或 C。

---

### 5. blog_forum：博客、论坛和社区

个人博客、问答网站、技术社区、论坛帖子、用户经验分享。

例子：

- CSDN
- 知乎
- Medium
- Reddit
- Stack Overflow
- 个人网站
- 论坛帖子

默认信任等级：C 或 D。

适合做线索、经验、排错参考，不适合直接支撑高风险事实结论。

---

### 6. social_media：社交平台

短帖、账号动态、评论、截图、转发等。社交平台的证据强度高度依赖账号主体身份，需逐账号评估其身份、认证质量、专业领域匹配度、立场倾向和利益关系。

例子：

- X / Twitter
- 微博
- LinkedIn 帖子
- YouTube 评论
- Bilibili 评论
- Telegram 截图
- 小红书帖子

默认信任等级：D（普通用户），但可根据账号主体身份上调。

例外：如果账号是原始人物、公司、政府机构或项目维护者的认证账号，可加次级标签 `official_social`。

注意：如果判定为自媒体（个人 IP 化运营、有商业变现行为、内容以个人观点为主），应重新分类为 `self_media`，终止 `source_social.md` 规则，切换至 `source_self_media.md`。

详细评估规则见 `rules/source_social.md`。

---

### 7. self_media：自媒体

个人或小团队以独立创作者身份在社交/内容平台上运营的账号。与普通社交平台用户的区别在于：具有明确的个人 IP 属性、持续产出内容、通常依赖流量或商业变现。

识别特征：

- 账号名称带有个人 IP 化特征（如"XX说""XX观察""XX老师""XX哥/姐"）
- 以个人身份持续产出内容，非偶发性的个人分享
- 存在商业变现行为（带货、课程、赞助、流量分成）
- 内容以观点、评论、经验、教程为主
- 缺乏机构编辑审核机制

默认信任等级：D 或 E，取决于作者资质和内容质量。

具体评估规则见 `rules/source_self_media.md`。

---

### 8. aggregator_or_scraper：聚合或采集站

转载、采集、镜像、SEO 内容农场、无原创信息页面。

默认信任等级：D。

具体情况依赖原始来源的可靠性和是否正确引用原始来源。

---

### 9. suspicious：可疑来源

存在严重可靠性风险的来源。

典型信号：

- 无作者
- 无日期
- 无机构信息
- 内容疑似复制
- 标题党
- 域名伪装成官方
- 大量广告和跳转
- 无出站引用
- 语言夸张、煽动、营销化
- 疑似 AI 生成垃圾内容

默认信任等级：E。

## 次级标签

可按需添加：

```text
primary_source              原始来源
secondary_report            二手报道
opinion                     评论或观点
sponsored                   赞助内容
press_release               新闻稿
preprint                    预印本
peer_reviewed               同行评审
outdated                    可能过时
no_author                   无作者
no_date                     无日期
cites_original              引用了原始来源
does_not_cite_original      未引用原始来源
possible_scraper            可能是采集站
  official_social             官方社交账号
  social_media_standalone_post 权威媒体在社交平台独立发布的内容（未引用自家报道）
  undisclosed_advertisement    未标注的商业推广
  disclosed_advertisement      已标注的商业推广/赞助
  potential_conflict_of_interest 潜在利益关系
  political_bias_detected      政治立场偏倚
  commercial_bias_detected     商业立场偏倚
  preference_bias_detected     偏好/价值观立场偏倚
  brand_preference_detected    品牌偏好（意见领袖）
  commercial_collaboration_detected 商业合作关系（意见领袖）
  value_stance_detected        价值观立场（意见领袖）
  industry_side_detected       行业站队（意见领袖）
  opinion_leader               意见领袖/KOL/大V
  controversial_topic         争议性话题
  high_stakes                 高风险话题
  cross_language_report       跨语言报道（非原产地语言来源）
  echo_chamber_risk           信息茧房风险（单一语言生态内重复，无原产地语言一手来源）
  origin_language_primary     原产地语言一手来源（已引用原始语言官方/权威来源）
```
以及其他根据实际情况定义的标签。
## 分类优先级

如果一个来源同时符合多个类别，优先选择更能代表其证据性质的类别：

```text
官方原文 > 法规/标准/论文 > 原始数据/代码 > 新闻报道 > 专业分析 > 博客论坛 > 社交平台（官方账号） > 自媒体 > 社交平台（普通用户） > 采集站/可疑站点
```

例子：

- 公司官网发布的博客文章：`official`，可加 `press_release` 或 `marketing` 标签。
- 公司创始人认证 X 账号发公告：`social_media` + `official_social`。
- 个人博主在微博/小红书持续发布美妆评测并带货：`self_media`。
- 新闻媒体转载公司新闻稿：`news` + `press_release` + `secondary_report`。
- GitHub 上原项目 release：`official` + `primary_source`。
