
> **阅读本文件前必须先阅读 SKILL.md 以了解完整任务上下文。**

# AI 与科技信息特殊规则

AI、软件、开源、模型能力、API 功能等信息变化快，必须优先使用原始技术来源。

## 最佳来源

```text
官方博客
官方文档
API reference
model card
technical report
arXiv / 论文
GitHub 仓库
Hugging Face 模型页
release note
changelog
package registry
LICENSE 文件
commit / PR / issue
```

## 不同技术点的证据要求

### 开源状态

要确认为“开源”，应当在官方渠道中找到以下证据：

```text
公开代码仓库
公开模型权重
LICENSE 文件
官方发布页链接到代码或权重
包管理器或模型平台上的官方条目
```

不能仅凭以下内容确认：

```text
媒体称“开源”
网友称“开源”
只有 demo 没有代码
只发布 API 没有代码或权重
```

### 模型能力评估

评估建议参考：

```text
官方文档
模型卡
技术报告
论文
可复现实验
独立评测
```

注意区分：

```text
官方宣称能力
实际可用能力
demo 能力
API 稳定功能
beta 功能
```

### API 功能评估

优先参考：

```text
官方 API 文档
SDK changelog
release note
示例代码
开发者公告
```

必须检查：

```text
版本号
地区限制
账号权限
是否 beta
是否弃用
```

### 模型发布时间

优先参考：

```text
官方公告
release note
模型平台发布时间
论文提交日期
GitHub release 时间
```

### 性能评测 (Benchmark)

对于 benchmark 数据查询场景，先确定该页面在分类体系中的位置：

- benchmark 项目自己的官方网站（如 LiveBench、HELM、Open LLM Leaderboard 等）——对于该评测的分数而言是 “official” + “primary_source”，它是该评测数据的原始发布方
- benchmark 的论文（如 arXiv 上的 LiveBench 论文）——属于 “academic”
- 聚合站转载 benchmark 数据（如某些 SEO 站从官方榜单拷贝排名）——属于 “aggregator_or_scraper”，应溯源回到官方榜单
- 媒体/博客转述 benchmark 结果——属于二手报道，不可替代原始来源

必须检查：

```text
测试集名称
评测方法
是否官方自评
是否独立复现
是否可能存在过拟合或 cherry-pick
是否与同级别、同日期模型比较
页面是否是 benchmark 项目自己的官方入口（而非聚合转载）
```

## 红旗信号

```text
无方法的 benchmark 图
泄露截图
社交平台传言
模型聚合站复制列表
许可证不清楚
“最强”“第一”“遥遥领先”但没有方法
```

## 输出建议

```json
{
  "topic_rule": "ai_tech",
  "required_primary_evidence": ["official_docs", "release_notes", "github_repo", "model_card"],
  "warnings": ["媒体报道不能单独证明开源状态"]
}
```
