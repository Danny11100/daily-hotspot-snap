# Daily Hotspot Snap

每日全球热点快照 - 基于多维度评分的智能信息筛选工具。

## 快速开始

1. 安装 skill
```bash
clawdhub install daily-hotspot-snap
```

2. 复制配置
```bash
cp skills/daily-hotspot-snap/config.yaml config.yaml
```

3. 编辑配置（设置你的关注领域、数据源等）

4. 启动自动推送
```bash
openclaw cron enable daily-hotspot-snap
```

## 文件结构

```
daily-hotspot-snap/
├── SKILL.md              # 使用说明
├── config.yaml           # 用户配置文件
├── templates/
│   ├── external.txt      # 对外版模板（公众号）
│   └── internal.txt      # 对内版模板（持仓分析）
├── examples/             # 示例输出
└── README.md             # 本文件
```

## 示例输出

### 对外版

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

### 对内版

```
全球热点快照 | 对内版 | 2026-03-04

❶ 中东冲突升级（⭐95）
来源：Bloomberg + Reuters
核心变化：伊朗威胁封锁霍尔木兹海峡，油价突破$85

→ 你的持仓影响：
  QQQ可能承压，IEF作为防守层持有观察

→ 建议动作：
  关注10Y收益率，若突破4.2%考虑加仓IEF
```

## 评分公式

```
总分 = H×0.4 + S×0.3 + R×0.2 + T×0.1

H (热度 40分): Google Trends + 社交媒体讨论
S (情绪信号 30分): 市场波动 + 专家一致性
R (相关度 20分): 与你关注领域的匹配度
T (时效性 10分): 24h内(10分) / 本周(5分)
```

## 贡献

欢迎提交 PR 改进：
- 新增数据源
- 优化评分算法
- 改进模板设计
- 修复问题

## License

MIT
