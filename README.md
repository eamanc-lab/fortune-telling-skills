# Fortune Telling Skills — 运势测算 Skill 套件

跨玄学领域的 Claude Code Skill 集合，覆盖中西方主流运势测算体系。每个 Skill 独立可用，也可通过 fortune-hub 统一入口串联使用。

## Skills 一览

| Skill | 领域 | 说明 | 所需信息 |
|-------|------|------|---------|
| [fortune-hub](fortune-hub/) | 路由入口 | 引导选择领域、收集信息、路由到对应 Skill | — |
| [horoscope-daily](horoscope-daily/) | 星座运势 | 日/周/月运势预测，五大维度评分 | 出生日期 |
| [numerology-fortune](numerology-fortune/) | 数字命理 | 生命灵数、表达数等核心数字分析 | 出生日期 + 英文全名 |
| [tarot-reading](tarot-reading/) | 塔罗占卜 | 78 张牌义 + 5 种牌阵解读 | 具体问题（现场提供） |
| [bazi-fortune](bazi-fortune/) | 八字四柱 | 五行分析、十神推算、大运流年 | 出生日期 + 时辰 + 性别 |
| [meihua-yishu](meihua-yishu/) | 梅花易数 | 即时起卦、体用断卦 | 具体问题（现场提供） |
| [ziwei-fortune](ziwei-fortune/) | 紫微斗数 | 十四主星排盘、十二宫解读 | 农历出生日期 + 时辰 + 性别 |
| [liuyao-yijing](liuyao-yijing/) | 六爻易经 | 铜钱起卦、纳甲装卦、六亲断卦 | 具体问题（现场提供） |
| [vedic-astrology](vedic-astrology/) | 吠陀占星 | Nakshatra 月宿 + Dasha 大运系统 | 出生日期 + 时间 + 出生地 |
| [qimen-dunjia](qimen-dunjia/) | 奇门遁甲 | 九宫四层盘面排盘、择时决策 | 具体问题（现场提供） |
| [fengshui-advisor](fengshui-advisor/) | 风水顾问 | 八宅风水 + 玄空飞星、方位布局 | 出生年份 + 性别（+ 房屋坐向） |

## 安装

### 通过 ClawHub（推荐）

```bash
# 安装单个 Skill
npx clawhub@latest install fortune-hub
npx clawhub@latest install horoscope-daily
npx clawhub@latest install numerology-fortune
# ... 其他 skill 同理
```

### 手动安装

```bash
git clone git@github.com:eamanc-lab/fortune-telling-skills.git
# 链接需要的 Skill 到 ~/.claude/skills/
ln -s $(pwd)/fortune-telling-skills/fortune-hub ~/.claude/skills/fortune-hub
ln -s $(pwd)/fortune-telling-skills/horoscope-daily ~/.claude/skills/horoscope-daily
```

## 使用示例

```
# 通过 fortune-hub 路由（不确定要什么时）
"帮我看看运势"        →  展示领域菜单
"帮我算算"            →  引导选择

# 直接使用具体 Skill
"白羊座今日运势"       →  horoscope-daily
"帮我算生命灵数"       →  numerology-fortune
"塔罗占卜，问事业"     →  tarot-reading
"帮我排八字"          →  bazi-fortune
"起一卦"             →  meihua-yishu
"紫微斗数排盘"        →  ziwei-fortune
"六爻占卜"           →  liuyao-yijing
"看看风水"           →  fengshui-advisor
```

## 架构

```
fortune-telling-skills/
├── fortune-hub/              ← 路由入口（引导 + 信息收集 + 共享记忆）
├── horoscope-daily/          ← 星座运势（12 星座知识库 + 日/周/月格式）
├── numerology-fortune/       ← 数字命理（计算规则 + 数字含义库）
├── tarot-reading/            ← 塔罗占卜（78 牌义 + 5 牌阵 + 解读规则）
├── bazi-fortune/             ← 八字四柱（排盘规则 + 十神 + 神煞 + 大运）
├── meihua-yishu/             ← 梅花易数（起卦规则 + 64 卦表 + 万物类象）
├── ziwei-fortune/            ← 紫微斗数（安星规则 + 十四主星 + 四化）
├── liuyao-yijing/            ← 六爻易经（纳甲规则 + 八宫 64 卦 + 六亲六神）
├── vedic-astrology/          ← 吠陀占星（Nakshatra + Dasha + 九曜）
├── qimen-dunjia/             ← 奇门遁甲（九宫 + 九星八门八神 + 格局）
└── fengshui-advisor/         ← 风水顾问（八宅 + 飞星 + 三元九运）
```

### 记忆系统

每个 Skill 独立存储用户信息（`MEMORY.md`，gitignored），支持双源读取：

1. 本 Skill 的 `MEMORY.md`（最优先）
2. `fortune-hub/MEMORY.md`（补充共享字段）

用户只需提供一次出生信息，所有 Skill 自动复用。

## 许可证

MIT
