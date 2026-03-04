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
- **可定制化**：数据源、评分权重、输出格式均可配置

## 适用场景

1. **内容创作者**：获取每日选题灵感，建立个人知识库
2. **产品经理**：跟踪AI、科技领域的产品范式变化
3. **研究人员**：建立信息输入源，节省筛选时间
4. **投资者**：快速掌握影响持仓的全球宏观信号

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
生成热点快照
   ↓
08:10 发送到你的频道
```

## 评分公式

```
总分 = H×0.4 + S×0.3 + R×0.2 + T×0.1

H（热度 40分）: Google Trends变化 + 社交媒体讨论量
S（情绪信号 30分）: 市场波动反应 + 专家观点一致性
R（相关度 20分）: 与你关注领域的匹配度
T（时效性 10分）: 24h内(10分) / 本周(5分)

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
- Bloomberg Markets RSS
- Reuters Breaking News
- CBOE VIX数据

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
name: "daily-hotspot-snap"
version: "0.1.0"

# 定时任务
schedule:
  enabled: true
  time: "08:10"        # 发送时间
  timezone: "Asia/Shanghai"
  
# 评分权重（所有权重之和应等于1.0）
scoring:
  heat: 0.4            # 热度：讨论量、搜索趋势
  signal: 0.3          # 情绪信号：市场反应、专家一致性
  relevance: 0.2       # 相关度：与你关注领域的匹配
  timeliness: 0.1      # 时效性：24h内得分最高
  threshold: 60        # 入选阈值（0-100）
  max_items: 10        # 每日最大条数

# 关注领域（用于计算相关度）
# 可选：ai, fintech, crypto, product, biotech, energy, geopolitics
interests:
  - ai
  - fintech
  - crypto
  - product

# 数据源配置
data_sources:
  # 一级信源（AI/科技）
  arxiv_ai:
    enabled: true
    url: "https://arxiv.org/rss/cs.AI"
    category: "ai"
    weight: 1.0
    
  openai_blog:
    enabled: true
    url: "https://openai.com/blog/rss.xml"
    category: "ai"
    weight: 1.2
    
  hackernews:
    enabled: true
    url: "https://hnrss.org/frontpage"
    category: "tech"
    weight: 1.0
  
  # 一级信源（金融/宏观）
  bloomberg:
    enabled: true
    url: "https://www.bloomberg.com/feeds/markets"
    category: "finance"
    weight: 1.2
    note: "可能需要订阅"
    
  reuters:
    enabled: true
    url: "https://www.reuters.com/markets/rss"
    category: "finance"
    weight: 1.1
    
  # 二级信源（Crypto）
  coindesk:
    enabled: true
    url: "https://www.coindesk.com/arc/outboundfeeds/rss/"
    category: "crypto"
    weight: 1.0
    
  the_block:
    enabled: true
    url: "https://www.theblock.co/rss.xml"
    category: "crypto"
    weight: 0.9
  
  # 二级信源（产品/商业）
  first_round:
    enabled: true
    url: "https://review.firstround.com/rss"
    category: "product"
    weight: 0.8
    
  stratechery:
    enabled: true
    url: "https://stratechery.com/feed/"
    category: "product"
    weight: 0.9
  
  # 自定义RSS源（用户可添加）
  custom: []
  # 示例：
  # - name: "My Blog"
  #   url: "https://myblog.com/rss"
  #   category: "personal"
  #   weight: 0.5

# 输出配置
output:
  max_length: 800              # 正文字数限制
  include_score: false         # 是否显示分数
  include_source_icon: false   # 是否显示来源标识
  signature: "一石半会儿 | 产品经理、AI学习者"
  disclaimer: "个人学习笔记，不构成投资建议"
  format: "text"               # 格式：text/markdown

# 推送渠道
channels:
  telegram:
    enabled: true
    target: "YOUR_TELEGRAM_ID"         # 你的Telegram ID
  
  # 可选：邮件推送
  email:
    enabled: false
    smtp_server: ""
    smtp_port: 587
    username: ""
    password: ""
    to: ""
  
  # 可选：保存到文件
  file:
    enabled: false
    path: "output/hotspot/"
    format: "markdown"

# 高级设置
advanced:
  # 缓存时间（分钟）
  cache_duration: 30
  
  # 重试次数
  retry_count: 3
  
  # 日志级别
  log_level: "info"              # debug/info/warn/error
  
  # 周报生成（周日）
  weekly_summary:
    enabled: true
    time: "22:00"
    include_charts: false        # 是否生成趋势图
```

## 使用方法

### 自动模式（推荐）

配置好后，每天自动执行：
- 08:10 生成并发送热点快照

### 手动触发

```
用户：今天的热点
助手：生成今日全球热点快照

用户：刷新数据源
助手：重新抓取并生成最新热点
```

### 查看历史

```
用户：本周热点汇总
助手：基于本周7天热点生成周报
```

## 输出格式

```
全球热点快照 | 2026-03-04

▌AI 科技

❶ OpenAI发布GPT-5.3 Instant，推理效率提升40%
来源：OpenAI官方 + HN热榜
解读：新一代模型大幅降低推理成本，API价格可能下调，内容社区产品形态将迎来新一轮迭代

❷ 多智能体协作框架DIG实现"可解释AI"突破
来源：arXiv + MIT Tech Review
解读：首次将多代理协作建模为动态因果网络，推荐系统的debug和优化将有新工具

▎金融 宏观

❸ 中东冲突升级，伊朗威胁封锁霍尔木兹海峡
来源：Bloomberg + Reuters
解读：全球20%石油运输通道面临中断，油价突破$85，通胀预期升温

❹ 美联储3月会议纪要显示降息预期降温
来源：Bloomberg
解读：10Y收益率升至4.086%，高利率维持时间可能延长，成长股估值承压

▏Crypto

❺ Trump发文力挺稳定币法案CLARITY
来源：Truth Social + Bloomberg
解读：明确支持稳定币立法，监管框架加速成型，合规稳定币（USDC）受益

今日情绪：Risk OFF（VIX 24，黄金+1.5%，资金避险）
关键信号：❸中东局势 ❹美联储政策 ❺监管框架

新闻逻辑：热度 + 情绪信号 + 相关度 + 时效性
免责声明：个人学习笔记，不构成投资建议

一石半会儿 | 产品经理、AI学习者
```

## 自定义模板

在 `templates/` 目录下创建自定义模板：

```markdown
<!-- templates/custom.txt -->
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
- 支持全球化一级数据源
- 基于H+S+R+T四维评分模型
- 支持自定义模板和配置

## 贡献

欢迎提交 PR 改进：
- 新增数据源
- 优化评分算法
- 改进模板设计
- 修复问题

GitHub: https://github.com/Danny11100/daily-hotspot-snap

## 联系

一石半会儿 | 产品经理、AI学习者

## License

MIT
