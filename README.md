<p align="center">
  <h1 align="center">Fortune Telling Skills</h1>
  <p align="center">
    <strong>10 divination systems in one Claude Code skill suite — from Horoscope to Feng Shui</strong>
    <br/>
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

A collection of Claude Code Skills covering major Eastern and Western divination systems. Each skill works **independently** or connects through `fortune-hub` as a unified entry point. Pure LLM reasoning + deterministic calculation, no external API required.

## Highlights

- **10 Divination Domains** — Horoscope, Numerology, Tarot, Bazi, Zi Wei, Meihua, Liu Yao, Vedic, Qi Men, Feng Shui
- **Zero Config** — Each skill runs standalone, no API keys or external services needed
- **Smart Memory** — Enter your birth info once, all skills auto-share via dual-source `MEMORY.md`
- **Unified Entry** — Not sure what you need? `fortune-hub` guides you to the right domain
- **Bilingual** — Western skills (Horoscope, Tarot, Numerology, Vedic) respond in English or Chinese based on user language; Eastern skills (Bazi, Zi Wei, etc.) are Chinese-native
- **Ethical Expression** — All skills follow unified guidelines: empower, never frighten; suggest, never dictate

## Skills

### Western Systems (English + Chinese)

| Skill | Domain | Description | Input |
|-------|--------|-------------|-------|
| [horoscope-daily](horoscope-daily/) | Horoscope | Daily/weekly/monthly forecasts, 5 dimensions + lucky guide | Birthday |
| [numerology-fortune](numerology-fortune/) | Numerology | Life Path, Expression, Soul Urge & 2 more core numbers | Birthday + full name |
| [tarot-reading](tarot-reading/) | Tarot | 78-card RWS deck, 5 spreads, elemental interaction rules | Your question |
| [vedic-astrology](vedic-astrology/) | Vedic / Jyotish | 27 Nakshatras + Vimshottari Dasha system | Birthday + time + birthplace |

### Eastern Systems (Chinese 中文)

| Skill | 领域 | 说明 | 所需信息 |
|-------|------|------|---------|
| [bazi-fortune](bazi-fortune/) | 八字四柱 | 四柱排盘 + 十神 + 大运流年 | 出生日期 + 时辰 + 性别 |
| [ziwei-fortune](ziwei-fortune/) | 紫微斗数 | 十四主星排盘 + 十二宫 + 四化 | 农历生日 + 时辰 + 性别 |
| [meihua-yishu](meihua-yishu/) | 梅花易数 | 时间/数字/文字起卦 + 体用断卦 | 具体问题 |
| [liuyao-yijing](liuyao-yijing/) | 六爻易经 | 铜钱起卦 + 纳甲装卦 + 六亲断卦 | 具体问题 |
| [qimen-dunjia](qimen-dunjia/) | 奇门遁甲 | 九宫四层盘面 + 格局判断 | 具体问题 |
| [fengshui-advisor](fengshui-advisor/) | 风水顾问 | 八宅本命卦 + 玄空飞星 | 出生年份 + 性别 |

### Hub

| Skill | Description |
|-------|-------------|
| [fortune-hub](fortune-hub/) | Unified entry point — guides domain selection, collects info, routes to the right skill |

## Quick Start

### Install

**Via ClawHub (recommended):**

```bash
npx clawhub@latest install fortune-hub
npx clawhub@latest install horoscope-daily
npx clawhub@latest install tarot-reading
# install others as needed
```

**Manual:**

```bash
git clone git@github.com:eamanc-lab/fortune-telling-skills.git
ln -s $(pwd)/fortune-telling-skills/fortune-hub ~/.claude/skills/fortune-hub
ln -s $(pwd)/fortune-telling-skills/horoscope-daily ~/.claude/skills/horoscope-daily
```

### Usage

```
# Not sure what you need? Let fortune-hub guide you
"Help me check my fortune"     →  shows 10-domain menu
"What's my luck today?"        →  guided selection

# Use a specific skill directly
"Aries horoscope today"        →  horoscope-daily
"Calculate my life path number" →  numerology-fortune
"Tarot reading for career"     →  tarot-reading
"Vedic chart analysis"         →  vedic-astrology
"帮我排八字"                    →  bazi-fortune
"起一卦"                       →  meihua-yishu
"紫微斗数排盘"                  →  ziwei-fortune
"六爻占卜"                     →  liuyao-yijing
"奇门遁甲排盘"                  →  qimen-dunjia
"看看风水"                     →  fengshui-advisor
```

## Architecture

```
fortune-telling-skills/
├── fortune-hub/              ← Unified entry (routing + info collection + shared memory)
│
├── horoscope-daily/          ← Horoscope (12-sign knowledge base, daily/weekly/monthly)
├── numerology-fortune/       ← Numerology (Pythagorean system + number meanings)
├── tarot-reading/            ← Tarot (78 card meanings + 5 spreads + interpretation rules)
├── vedic-astrology/          ← Vedic (Nakshatra + Dasha + Navagraha)
│
├── bazi-fortune/             ← 八字 (Four Pillars + Ten Gods + Major Cycles)
├── ziwei-fortune/            ← 紫微 (14 Major Stars + 12 Palaces + Four Transformations)
├── meihua-yishu/             ← 梅花 (Hexagram casting + Ti-Yong interpretation)
├── liuyao-yijing/            ← 六爻 (Na-Jia system + Six Relatives + Six Spirits)
├── qimen-dunjia/             ← 奇门 (Nine Palaces + Stars/Gates/Spirits/Stems)
└── fengshui-advisor/         ← 风水 (Ba Zhai + Flying Stars + San Yuan Nine Periods)
```

### Memory System

Each skill stores user data independently (`MEMORY.md`, gitignored), with **dual-source reading**:

1. **This skill's `MEMORY.md`** — highest priority, includes domain-specific data
2. **`fortune-hub/MEMORY.md`** — supplements shared fields (birthday, birth time, gender, etc.)

Enter your birth info once, every skill reuses it automatically. Each skill also runs fully standalone — no dependency on fortune-hub.

## License

[MIT](LICENSE)
