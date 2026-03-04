---
name: daily-hotspot-snap
description: 每日全球热点快照 - 基于多维度评分的智能信息筛选工具。从AI、科技、金融等领域自动筛选高价值信息，生成结构化的每日热点简报。
version: 0.1.0
author: 一石半会儿
license: MIT
tags: [news, ai, finance, crypto, daily, signal]
---

# Daily Hotspot Snap - 每日全球热点快照

一个基于"热度+情绪信号+相关度+时效性"四维评分模型的智能信息筛选工具，帮助你从信息洪流中提取真正重要的信号。

## 核心价值

- **信息降噪**：从每天数百条信息中筛选出10条最有价值的
- **结构化输出**：每条信息包含"来源-解读-影响"三层信息
- **多场景适配**：支持对内分析版（含持仓建议）和对外发布版（纯信息）
- **可定制化**：数据源、评分权重、输出格式均可配置

## 适用场景

1. **投资者**：快速掌握影响持仓的全球宏观信号
2. **产品经理**：跟踪AI、科技领域的产品范式变化
3. **内容创作者**：获取每日选题灵感
4. **研究人员**：建立个人知识库的信息输入源

## 工作流程

```
07:30 自动触发
   ↓
抓取数据源（Bloomberg/Reuters/arXiv/HN等）
   ↓
按评分公式计算每条信息得分
   ↓
取前10名高分信息
   ↓
生成双版本（对内版/对外版）
   ↓
08:10 发送对外版（公众号/小红书）
08:30 发送对内版（持仓分析）
```

## 评分公式

```
总分 = H×0.4 + S×0.3 + R×0.2 + T×0.1

H (热度 40分): Google Trends变化 + 社交媒体讨论量
S (情绪信号 30分): 市场波动反应 + 专家观点一致性
R (相关度 20分): 与你关注领域的匹配度
T (时效性 10分): 24h内(10分) / 本周(5分)

入选阈值: ≥60分
```

## 数据源配置

默认覆盖以下权威信源：

### AI/科技 (P0)
- arXiv cs.AI/cs.IR: https://arxiv.org/rss/cs.AI
- OpenAI Blog: https://openai.com/blog/rss.xml
- Hacker News: https://hnrss.org/frontpage
- MIT Tech Review: https://www.technologyreview.com/feed/

### 金融/宏观 (P0)
- Bloomberg Markets: https://www.bloomberg.com/feeds/markets
- Reuters Breaking News: https://www.reuters.com/markets/rss
- CBOE VIX: https://www.cboe.com/tradable_products/vix/

### Crypto (P1)
- CoinDesk: https://www.coindesk.com/arc/outboundfeeds/rss/
- The Block: https://www.theblock.co/rss.xml

### 产品/商业 (P1)
- First Round Review: https://review.firstround.com/rss
- Stratechery: https://stratechery.com/feed/

## 安装

```bash
clawdhub install daily-hotspot-snap
```

## 配置

编辑 `config.yaml`：

```yaml
# 基础设置
schedule:
  time: "08:10"        # 对外版发送时间
  timezone: "Asia/Shanghai"
  
# 评分权重（可调整）
scoring:
  heat: 0.4            # 热度权重
  signal: 0.3          # 情绪信号权重
  relevance: 0.2       # 相关度权重
  timeliness: 0.1      # 时效性权重
  threshold: 60        # 入选阈值

# 关注领域（影响相关度评分）
interests:
  - ai                 # AI/大模型
  - fintech            # 金融科技
  - crypto             # 加密货币
  - product            # 产品方法论

# 数据源开关
data_sources:
  bloomberg: true
  reuters: true
  arxiv: true
  hackernews: true
  coindesk: true
  # 添加自定义RSS
  custom:
    - name: "My Source"
      url: "https://example.com/rss"
      weight: 1.0

# 输出配置
output:
  # 对外版设置
  external:
    max_length: 800        # 字数限制
    include_score: false   # 是否显示分数
    signature: "一石半会儿 | 产品经理、AI学习者"
  
  # 对内版设置
  internal:
    include_portfolio: true    # 是否关联持仓分析
    include_action: true       # 是否给出操作建议
```

## 使用方法

### 自动模式（推荐）

配置好后，每天自动执行：
- 08:10 发送对外版（可发公众号/小红书）
- 08:30 发送对内版（持仓分析）

### 手动触发

```
用户：今天的热点
助手：生成今日全球热点快照（双版本）

用户：刷新数据源
助手：重新抓取并生成最新热点
```

### 查看历史

```
用户：本周热点汇总
助手：基于本周7天热点生成周报
```

## 输出格式

### 对外版（纯信息，可公开发布）

```
全球热点快照 | 2026-03-04

▌AI 科技

❶ OpenAI发布GPT-5.3 Instant
来源：OpenAI官方 + HN热榜
解读：新一代模型大幅降低推理成本...

▎金融 宏观

❷ 中东冲突升级...
来源：Bloomberg + Reuters
解读：全球20%石油运输通道面临中断...

今日情绪：Risk OFF（VIX 24）
关键信号：❶AI迭代 ❷地缘风险

新闻逻辑：热度 + 情绪信号 + 相关度 + 时效性
免责声明：个人学习笔记，不构成投资建议

一石半会儿 | 产品经理、AI学习者
```

### 对内版（含持仓关联）

```
全球热点快照 | 对内版 | 2026-03-04

❶ 中东冲突升级（⭐95）
→ 油价突破$85，通胀预期升温
→ 你的持仓影响：QQQ承压，IEF作为防守层持有
→ 建议：关注10Y收益率，若突破4.2%考虑加仓IEF
...
```

## 自定义模板

在 `templates/` 目录下创建自定义模板：

```markdown
<!-- templates/custom.md -->
# {{date}} 每日精选

{{#items}}
## {{number}}. {{title}}
- 来源：{{source}}
- 我的观点：{{comment}}
{{/items}}

---
生成时间：{{generated_at}}
```

## 注意事项

1. **数据源限制**：部分源（如Bloomberg）可能需要订阅
2. **评分主观性**：公式权重可根据个人偏好调整
3. **延迟问题**：RSS抓取有15-30分钟延迟，突发新闻可能滞后
4. **合规风险**：对外发布请遵守平台规则，加免责声明

## 更新日志

### v0.1.0 (2026-03-04)
- 初始版本发布
- 支持双版本输出（对内/对外）
- 内置6个一级数据源
- 支持自定义RSS源

## 贡献

欢迎提交 PR 改进：
- 新增数据源
- 优化评分算法
- 改进输出模板
- 修复问题

GitHub: https://github.com/yourname/daily-hotspot-snap

## 联系

一石半会儿 | 产品经理、AI学习者
