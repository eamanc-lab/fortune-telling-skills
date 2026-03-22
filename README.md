<p align="center">
  <h1 align="center">Fortune Telling Skills</h1>
  <p align="center">
    <strong>覆盖 10 大玄学体系的 Claude Code Skill 套件 — 从星座到风水，一套搞定</strong>
  </p>
</p>

<p align="center">
  <a href="https://github.com/eamanc-lab/fortune-telling-skills/stargazers"><img src="https://img.shields.io/github/stars/eamanc-lab/fortune-telling-skills?style=social" alt="GitHub Stars"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
  <a href="#"><img src="https://img.shields.io/badge/Skills-11-blueviolet" alt="11 Skills"></a>
  <a href="#"><img src="https://img.shields.io/badge/Claude_Code-Compatible-blue" alt="Claude Code"></a>
</p>

---

中西方主流运势测算体系的 Claude Code Skill 集合。每个 Skill **独立可用**，也可通过 `fortune-hub` 统一入口串联使用。纯 LLM 推理 + 确定性计算，无外部 API 依赖。

## 亮点

- **10 大玄学领域**：星座、数字命理、塔罗、八字、紫微、梅花、六爻、吠陀、奇门、风水
- **即装即用**：每个 Skill 独立运行，无需配置 API Key 或外部服务
- **智能记忆**：用户信息一次录入，跨 Skill 自动复用（双源 MEMORY.md 机制）
- **统一入口**：不确定要算什么？`fortune-hub` 引导你选择最合适的领域
- **安全表达**：全部 Skill 遵循统一的表达伦理——赋权而非预测，禁止恐吓性语言

## Skills 一览

| Skill | 领域 | 一句话说明 | 所需信息 |
|-------|------|----------|---------|
| [fortune-hub](fortune-hub/) | 统一入口 | 引导选择领域 + 收集信息 + 智能路由 | — |
| [horoscope-daily](horoscope-daily/) | 星座运势 | 日/周/月运势，五大维度评分 + 幸运指南 | 出生日期 |
| [numerology-fortune](numerology-fortune/) | 数字命理 | 生命灵数等 5 大核心数字 + 个人年周期 | 出生日期 + 英文全名 |
| [tarot-reading](tarot-reading/) | 塔罗占卜 | 78 张牌义 + 5 种牌阵 + 组合解读 | 具体问题 |
| [bazi-fortune](bazi-fortune/) | 八字四柱 | 四柱排盘 + 十神 + 大运流年 | 出生日期 + 时辰 + 性别 |
| [meihua-yishu](meihua-yishu/) | 梅花易数 | 时间/数字/文字起卦 + 体用断卦 | 具体问题 |
| [ziwei-fortune](ziwei-fortune/) | 紫微斗数 | 十四主星排盘 + 十二宫 + 四化 | 农历生日 + 时辰 + 性别 |
| [liuyao-yijing](liuyao-yijing/) | 六爻易经 | 铜钱起卦 + 纳甲装卦 + 六亲断卦 | 具体问题 |
| [vedic-astrology](vedic-astrology/) | 吠陀占星 | 27 Nakshatras + Dasha 大运 | 出生日期 + 时间 + 出生地 |
| [qimen-dunjia](qimen-dunjia/) | 奇门遁甲 | 九宫四层盘面 + 格局判断 | 具体问题 |
| [fengshui-advisor](fengshui-advisor/) | 风水顾问 | 八宅本命卦 + 玄空飞星 | 出生年份 + 性别 |

## 快速开始

### 安装（选一种）

**通过 ClawHub：**

```bash
npx clawhub@latest install fortune-hub
npx clawhub@latest install horoscope-daily
npx clawhub@latest install tarot-reading
# ... 按需安装其他 skill
```

**手动安装：**

```bash
git clone git@github.com:eamanc-lab/fortune-telling-skills.git
ln -s $(pwd)/fortune-telling-skills/fortune-hub ~/.claude/skills/fortune-hub
ln -s $(pwd)/fortune-telling-skills/horoscope-daily ~/.claude/skills/horoscope-daily
```

### 使用

```
# 不确定要什么？让 fortune-hub 引导
"帮我看看运势"        →  展示 10 个领域菜单
"帮我算算"            →  引导选择

# 直接使用具体 Skill
"白羊座今日运势"       →  horoscope-daily
"帮我算生命灵数"       →  numerology-fortune
"塔罗占卜，问事业"     →  tarot-reading
"帮我排八字"          →  bazi-fortune
"起一卦"             →  meihua-yishu
"紫微斗数排盘"        →  ziwei-fortune
"六爻占卜"           →  liuyao-yijing
"吠陀占星分析"        →  vedic-astrology
"奇门遁甲排盘"        →  qimen-dunjia
"看看风水"           →  fengshui-advisor
```

## 架构

```
fortune-telling-skills/
├── fortune-hub/              ← 统一入口（引导 + 信息收集 + 共享记忆）
│
├── horoscope-daily/          ← 星座运势（12 星座知识库 + 日/周/月格式）
├── numerology-fortune/       ← 数字命理（毕达哥拉斯体系 + 数字含义库）
├── tarot-reading/            ← 塔罗占卜（78 牌义 + 5 牌阵 + 解读规则）
│
├── bazi-fortune/             ← 八字四柱（排盘 + 十神 + 神煞 + 大运）
├── meihua-yishu/             ← 梅花易数（起卦 + 64 卦 + 万物类象）
├── ziwei-fortune/            ← 紫微斗数（安星 + 十四主星 + 四化）
├── liuyao-yijing/            ← 六爻易经（纳甲 + 八宫 64 卦 + 六亲六神）
│
├── vedic-astrology/          ← 吠陀占星（Nakshatra + Dasha + 九曜）
├── qimen-dunjia/             ← 奇门遁甲（九宫 + 九星八门八神 + 格局）
└── fengshui-advisor/         ← 风水顾问（八宅 + 飞星 + 三元九运）
```

### 记忆系统

每个 Skill 独立存储用户信息（`MEMORY.md`，gitignored），支持**双源读取**：

1. **本 Skill 的 `MEMORY.md`** — 最优先，含领域专属数据
2. **`fortune-hub/MEMORY.md`** — 补充共享字段（生日、时辰、性别等）

用户只需提供一次出生信息，所有 Skill 自动复用。每个 Skill 也能独立运行——不依赖 fortune-hub。

## 许可证

[MIT](LICENSE)
