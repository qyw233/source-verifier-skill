> **阅读本文件前必须先阅读 SKILL.md 以了解完整任务上下文。**

# 购物平台来源处理规则

购物平台来源包括电商平台、品牌旗舰店、第三方商家店铺、商品详情页、用户评价、榜单、直播带货页、优惠信息页和比价页面。此类来源的核心特点是：页面通常服务于交易转化，存在天然商业动机，因此不能仅因平台知名或销量高就视为可靠事实来源。

**本规则是叠加规则。** 当前 schema 中没有独立的 `commerce` 主类型，因此不要输出 `source_type: commerce`。应根据页面证据性质选择最接近的主类型，并添加次级标签：

```text
官方品牌旗舰店/品牌自营页 → source_type: official，secondary_tags 添加 official_store、commercial_page
第三方商家商品页 → source_type: professional_analysis 或 unknown，secondary_tags 添加 merchant_page、commercial_page
平台榜单/推荐页/比价页 → source_type: aggregator_or_scraper 或 professional_analysis，secondary_tags 添加 ranking_page、commercial_page
用户评价/问答区 → source_type: blog_forum，secondary_tags 添加 user_reviews、commerce_platform
直播带货/达人种草页 → source_type: self_media 或 social_media，按对应规则继续评估
仿冒店铺、诱导跳转、异常低价页面 → source_type: suspicious
```

## 一、首先判断页面角色

评估购物平台来源时，必须先判断页面承担的角色。不同角色的证据价值不同：

```text
平台本身：平台规则、交易状态、物流、销量、评分、推荐排序
品牌官方店铺：品牌对商品名称、规格、价格、售卖状态的商业声明
第三方商家：该商家对商品、库存、价格、售后承诺的声明
用户评价：消费者个人体验集合
平台榜单/推荐：平台算法或商业运营结果
带货内容：营销内容或商业推广
```

## 二、可以支持哪些结论

### 可较强支持

购物平台页面可以较强支持与交易页面自身直接相关的事实：

```text
某商品当前是否在该平台上架
页面标注的价格、规格、套餐、库存状态
商家或店铺对商品的描述
平台展示的销量、评分、评价数量
该平台上某个店铺是否存在
用户评价中是否有人表达过某种体验
```

使用时必须说明：这些结论只代表**该页面或该平台展示的信息**，不自动等于产品真实质量、全网销量、官方事实或长期状态。

### 只能谨慎支持

```text
产品质量好坏
真实用户满意度
同类产品排名
性价比结论
长期价格趋势
缺货、停售、涨价等状态是否具有全渠道代表性
```

这些结论需要交叉验证中立评测、品牌官方信息、监管资料、第三方检测、价格历史工具或多平台数据。

### 不可单独支持

```text
医学功效、治疗效果、保健功效
金融收益、投资回报、稳赚承诺
安全性绝对保证
产品是否获得官方认证或监管批准
品牌真实市场份额
全网销量第一、行业第一等排名性宣传
重大质量问题或违法事实
```

## 三、品牌官方店铺与第三方商家

### 3.1 品牌官方店铺

若页面明确属于品牌官方旗舰店、品牌自营店或平台认证的官方店铺，可作为该品牌在该平台上的商业声明。

```text
可用于确认：商品名称、规格、官方套餐、在售状态、该平台售价、售后说明
不可直接用于确认：产品效果优于竞品、真实销量、用户满意度、医学/法律/金融效果
```

必须检查：

```text
店铺是否有平台官方认证
店铺名称是否与品牌主体一致
是否存在“授权店”“专卖店”“专营店”冒充官方旗舰店的风险
页面是否为广告落地页或活动页
商品描述是否包含夸大宣传
```

若确认是官方店铺：

```text
source_type: official
secondary_tags: ["official_store", "commercial_page"]
citation_usability: usable 或 use_with_caution
```

即使是官方店铺，也应在 warnings 中标注“该页面具有商业销售目的，涉及效果、领先性、排名等主张需独立验证”。

### 3.2 第三方商家页面

第三方商家页面只代表该商家的销售声明，证据强度低于品牌官方来源。

```text
默认 citation_usability: use_with_caution 或 not_recommended
source_reliability_score 通常不应高于 65
article_quality_score 取决于页面信息完整性、资质披露和可核验程度
```

负面信号：

```text
店铺主体不清晰
商品品牌、授权关系不明
标题堆砌关键词或夸张营销
价格异常低于市场水平
图片、详情页疑似复制
承诺绝对效果或夸大保障
售后、资质、检测报告不可核验
```

若涉及假货、仿冒、诱导跳转、刷单或异常低价，应改判为 `suspicious`。

## 四、用户评价和问答区

用户评价是个人体验集合，不等于经过验证的事实。

### 可参考

```text
用户主观体验
常见问题线索
售后问题线索
包装、物流、安装、使用场景反馈
```

### 不可作为

```text
产品真实功效证明
医学、法律、金融等高风险结论
统计意义上的满意度结论
判断商品是否合规或安全的唯一依据
```

必须检查刷评和异常评价信号：

```text
大量评价时间集中
评价措辞高度相似
图片或视频重复
大量无细节短评
追评模板化
差评被商家解释但没有实质回应
评论区出现引流、返现、好评奖励
```

处理方式：

```text
普通评价集合 → citation_usability: use_with_caution，标注为 user_experience
疑似刷评 → 添加 secondary_tags: suspected_review_manipulation，citation_usability: not_recommended
评价与官方/检测/监管来源冲突 → 以更高证据等级来源为准
```

## 五、平台榜单、推荐和销量

平台榜单、推荐位、热销榜、搜索排序通常混合了销量、广告、转化率、库存、用户画像和商业投放等因素。不得将其直接等同于客观排名。

```text
可说明：该平台在某时刻展示了某种排序或标签
不可说明：该商品客观排名第一、行业领先、全网最受欢迎
```

必须检查：

```text
榜单规则是否公开
是否标注广告、赞助、推广
是否为个性化推荐
是否有时间范围
是否只覆盖平台内数据
是否能导出或复核原始数据
```

若榜单缺少方法说明：

```text
citation_usability: not_recommended
recommended_action: seek_independent_market_data
```

## 六、价格、库存和时效性

购物平台信息高度动态，价格、库存、活动、优惠券和销量随时变化。

```text
必须记录访问时间或页面截图时间
freshness 默认要求非常高
价格和库存信息过期风险高
促销活动结束后，页面不再能支持历史价格判断，除非有可靠存档
```

时效性建议：

```text
当天或实时页面 → fresh
超过 7 天的价格/库存/促销信息 → possibly_outdated
超过 30 天的价格/库存/促销信息 → outdated
无访问时间或页面时间 → freshness: unknown
```

## 七、广告、带货和利益关系

购物平台页面通常具有商业目的，但仍需区分公开销售页面、平台广告、达人带货和未披露推广。

高风险信号：

```text
“必买”“闭眼入”“全网最低”“第一名”等无依据话术
强制引导下单、加私域、领券返现
评价区或问答区出现商家引导
达人内容未披露佣金、合作或赞助
页面主要由营销话术构成，缺少可核验规格
```

处理方式：

```text
明确广告/赞助 → 添加 disclosed_advertisement，citation_usability: use_with_caution
疑似未披露广告 → 添加 undisclosed_advertisement，citation_usability: not_recommended 或 do_not_use
达人带货内容 → 切换到 source_self_media.md 或 source_social.md 继续评估
```

## 八、高风险品类特殊规则

### 医疗健康、保健品、药品、医疗器械

```text
购物页面不能证明治疗效果或医学安全性
必须优先查找监管批准、说明书、临床指南、论文或官方药监信息
用户评价不能作为疗效证据
夸大疗效、暗示替代治疗 → citation_usability: do_not_use
```

### 金融、保险、投资课程

```text
商品页或课程页不能证明收益能力
必须检查资质、监管许可、风险披露和利益关系
承诺收益、稳赚、保本、高回报 → citation_usability: do_not_use
```

### 儿童用品、食品、化妆品、安全设备

```text
商品页只能说明商家声明
安全性、合规性、认证状态需查监管、检测报告或认证机构原文
```

## 九、输出建议

```json
{
  "source_type": "official | professional_analysis | blog_forum | self_media | social_media | aggregator_or_scraper | suspicious | unknown",
  "secondary_tags": [
    "commerce_platform",
    "commercial_page",
    "official_store",
    "merchant_page",
    "user_reviews",
    "ranking_page",
    "suspected_review_manipulation"
  ],
  "citation_usability": "usable | use_with_caution | not_recommended | do_not_use",
  "warnings": [
    "该页面具有商业销售目的",
    "价格、库存和销量信息高度依赖访问时间",
    "用户评价只能作为体验线索，不能作为高风险事实证据"
  ],
  "recommended_action": "cross_check_with_official_or_independent_sources"
}
```

