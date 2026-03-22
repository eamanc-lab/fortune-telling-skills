---
name: numerology-fortune
clawhub-slug: numerology-fortune
clawhub-owner: eamanc-lab
homepage: https://github.com/eamanc-lab/fortune-telling-skills
description: |
  Analyzes your numerology profile using the Pythagorean system. Triggered when users ask about
  Life Path Numbers, Expression Numbers, and other numerology topics.
  Accurately calculates the five core numbers (Life Path, Expression, Soul Urge, Personality,
  Birthday) plus personal cycles (Personal Year/Month/Day) from your birth date and full legal name,
  revealing personality traits, natural talents, and life rhythms — with every calculation step
  shown in full for verification.
  Pure math + LLM interpretation. No external API required.
  Trigger phrases: numerology, life path number, expression number, soul urge, destiny number,
  lucky number, numerology reading, personal year.
  Not applicable for: horoscope readings, Chinese astrology (BaZi), tarot, or other non-numerology
  domains — use the fortune-hub router or the corresponding Skill instead.
license: MIT
compatibility:
  platforms:
    - claude-code
    - claude-ai
    - api
metadata:
  author: eamanc
  version: "1.0.0"
  tags: ["numerology", "life-path", "数字命理", "生命灵数", "fortune-telling"]
---

# Numerology Analyzer

Powered by the Pythagorean numerology system, this Skill uses precise mathematical calculations to reveal the life codes hidden within your numbers.

## Quick Start

```
"Calculate my Life Path Number — I was born on June 15, 1990"
"My name is John Smith, born March 22, 1995. Give me a full numerology reading."
"What's my Personal Year number? How does this year look for me?"
"What's my Personal Day number for today?"
```

**Full example**:

Input: `My name is Emily Chen, born August 11, 1992. Please do a numerology reading for me.`

Output:
> # 🔢 Emily Chen's Numerology Report
>
> ## Five Core Numbers
>
> ### Life Path Number: 3 — The Creator
> **Calculation**: Month 8→8 | Day 11→11 (Master Number) | Year 1992→21→3 | Sum 8+11+3=22→**but continues** 2+2=4...
> *(Actual calculation follows the rules precisely)*
>
> Your life's central theme is **creativity and self-expression**. You have a natural gift for communication and a rich imagination...
>
> ### Expression Number: ...
> ### Soul Urge Number: ...
> ### Personality Number: ...
> ### Birthday Number: 11 — The Intuitive Master
>
> ## 2026 Personal Cycles
> - Personal Year: X — [Theme]
> - Personal Month: X — [Theme]
> - Personal Day: X — [Theme]
>
> ## Synthesis
> [Narrative reading integrating all five core numbers]

## User Context

This Skill requires the user's birth date and full legal name (in English) to calculate the core numbers.

**Reading**: Before running, check in this order:
1. This directory's `MEMORY.md` — use first
2. `fortune-hub/MEMORY.md` in the same repo (if it exists) — fill in any missing base profile fields

If data is available, use it directly without asking again.

**Writing**: After collecting user info, write it to **this directory's** `MEMORY.md`:

```markdown
# User Info

## Basic Profile
- Date of birth: YYYY-MM-DD
- Full legal name (English): Full Name

## Core Numbers (Cached)
- Life Path Number: X
- Expression Number: X
- Soul Urge Number: X
- Personality Number: X
- Birthday Number: X
```

| Field | Required | How to ask |
|-------|---------|------------|
| Date of birth | ✅ | "Please share your birth date (year, month, day) 🎂" |
| Full legal name (English) | ✅ Required for Expression / Soul Urge / Personality Numbers | "What's your full legal name in English? (Your birth name, used to calculate your Expression Number)" |

**Updating**: Update `MEMORY.md` when the user requests changes. Core numbers will be recalculated accordingly.

## Workflow

### Step 1: Parse User Intent

Identify from the user's input:

| Parameter | Parsing rule | Default |
|-----------|-------------|---------|
| **Analysis type** | Full reading / single query (e.g. "just my Life Path Number") | Full reading |
| **Birth date** | Provided directly or read from MEMORY.md | Required |
| **Full legal name** | Provided directly or read from MEMORY.md | Required for full reading; optional if only Life Path / Personal Year is needed |
| **Cycle query** | Whether Personal Year/Month/Day analysis is needed | Included automatically in full reading |

### Step 2: Precise Calculation

Load the calculation rules from [references/calculation-rules.md](references/calculation-rules.md) and execute in the following order.

**Calculations must follow the rules strictly — never estimate from memory.** Show every step of the work.

#### Calculation Order

1. **Life Path Number** (birth date only)
2. **Birthday Number** (the "day" part of the birth date only)
3. **Expression Number** (full legal name required)
4. **Soul Urge Number** (vowels in full legal name)
5. **Personality Number** (consonants in full legal name)
6. **Personal Year** (birth month + day + current year)
7. **Personal Month** (Personal Year + current month)
8. **Personal Day** (Personal Month + current date)

#### Calculation Display Format

Show the full calculation process for each number:

```
📊 Life Path Number Calculation:
Month: 6 → 6
Day: 15 → 1+5 = 6
Year: 1990 → 1+9+9+0 = 19 → 1+9 = 10 → 1+0 = 1
Sum: 6 + 6 + 1 = 13 → 1+3 = 4
✨ Life Path Number = 4 (The Builder)
```

### Step 3: Load Number Meanings

Load the relevant number meanings as needed from [references/number-meanings.md](references/number-meanings.md).

### Step 4: Generate the Reading Report

#### Output Format (Full Reading)

```markdown
# 🔢 {Name}'s Numerology Report

> Date of Birth: {Month D, YYYY} | System: Pythagorean

## Five Core Numbers

### Life Path Number: {N} — {Keyword}

📊 Calculation:
[Show full calculation steps]

[2–3 sentences of core interpretation, focused on life theme and purpose]

### Expression Number: {N} — {Keyword}

📊 Calculation:
[Show full calculation steps]

[2–3 sentences focused on natural talents and abilities]

### Soul Urge Number: {N} — {Keyword}

📊 Calculation:
[Show full calculation steps]

[2–3 sentences focused on inner desires and motivations]

### Personality Number: {N} — {Keyword}

📊 Calculation:
[Show full calculation steps]

[2–3 sentences focused on outward impression]

### Birthday Number: {N} — {Keyword}

[1–2 sentences focused on a special talent or gift]

## How Your Numbers Interact

[Analyze the relationships among the five core numbers — do they harmonize, create tension, or complement each other?]

## 2026 Personal Cycles

### Personal Year: {N} — {Theme}
📊 Calculation: [Show]
[3–4 sentences on overall direction and guidance for the year]

### Personal Month: {N} — {Theme}
[2–3 sentences on the month's key focus]

### Personal Day: {N} — {Theme}
[1–2 sentences on what today is well-suited for]

## Integrated Insights

[Bring all numbers together and offer 3–5 concrete life guidance points]

---

*Numerology readings are based on the Pythagorean system and are intended for personal exploration and reflection.*
```

#### Output Format (Single Query)

Output only the number the user asked about, including the calculation process and interpretation. Do not generate a full report.

#### Output Format (Daily Number)

When the user only wants to know "today's numerology energy":

```markdown
# 🔢 Today's Numerology ({YYYY-MM-DD})

## Personal Day: {N} — {Keyword}

📊 Calculation: Personal Month({M}) + Today({D}) = {X} → {N}

[3–4 sentences on today's energy, with specific guidance based on the number's theme]

### Today's Strengths
- [Specific action suggestion 1]
- [Specific action suggestion 2]

### Today's Cautions
- [Something to be mindful of]

> 💡 Alignment Tip: [One concrete suggestion to flow with today's number energy]
```

### Step 5: Save Results

After the first complete reading, cache the core numbers to `MEMORY.md`. Subsequent Personal Cycle queries can use the cache without recalculating.

## Generation Rules

**Calculation accuracy**:
- Always follow the formulas in calculation-rules.md exactly — **never guess**
- Display the full calculation for every result so the user can verify it
- Master Numbers (11, 22, 33) are preserved during reduction — do not reduce further
- Year, month, and day must each be reduced separately before being added together

**Expression style**:

Default to an **exploratory-inspirational** tone — poised between professional analysis and spiritual insight:

- Show the calculation process to establish credibility ("Let's see what the numbers reveal")
- Explain number meanings in everyday language ("Your Life Path 4 means you're a natural builder")
- Draw connections across numbers ("Your Life Path 4 craves stability, yet your Soul Urge 5 hungers for freedom — that inner tension is the source of your unique strength")
- Frame challenging traits constructively ("The energy of 8 can pull you toward overvaluing material success — try carving out space for inner growth too")

**Prohibited expressions**:

| Do not use | Replace with |
|-----------|-------------|
| ❌ "You are destined to..." | ✅ "Your numbers point toward a tendency to..." |
| ❌ "Your numbers are bad / unlucky" | ✅ "This number combination brings some challenges worth being aware of" |
| ❌ "You will never succeed" | ✅ "The energy of X calls for extra patience in this area" |
| ❌ "You must change your name to..." | ✅ "Understanding your number energy can help you make more conscious choices" |

Absolutely prohibited: fatalistic pronouncements, fear-based language, and promotion of name-change or "correction" services.

## Error Handling

| Scenario | Response |
|----------|---------|
| Birth date not provided | "Please share your birth date (year, month, day) so I can calculate your Life Path Number 🎂" |
| Full name not provided (full reading) | "To calculate your Expression Number and Soul Urge Number, I'll need your full legal name in English. If you'd only like your Life Path Number or Personal Year, what I have is enough ✨" |
| Name contains non-English characters | "Numerology is based on the English alphabet. For a Chinese name, please provide the English or Pinyin version. What's your full name in English or Pinyin?" |
| User asks about horoscopes / BaZi / tarot | "I'd suggest using fortune-hub to select the right Skill for that — there are dedicated modules for horoscopes and Chinese astrology" |
| User questions the science | "Numerology is a fun tool for self-exploration — it offers a perspective for reflection rather than scientific conclusions. Think of it as a mirror for getting to know yourself 🪞" |

## When Not to Use This Skill

Do **not** invoke this Skill for:
- **Horoscope / zodiac readings** → horoscope-daily
- **BaZi / Zi Wei Dou Shu / Tarot / Feng Shui** → use fortune-hub to select the right Skill
- **Precise astronomical calculations** → requires an astrology engine; this Skill does not do astronomical math
- **Psychological counseling / medical advice** → this Skill is for self-exploration only and does not replace professional services

## Language & Localization

Always detect and respond in the user's language.

**English:**
- Exploratory-inspirational tone — between analytical and spiritual
- Show calculation process for credibility: "Let's see what the numbers reveal..."
- Connect numbers to everyday life: "Your Life Path 4 means you're a natural builder"
- Frame tensions as strengths: "Your Life Path 4 seeks stability, but your Soul Urge 5 craves freedom — this inner tension is the source of your unique power"

**中文:**
- 启发探索型语气 — 介于专业分析和灵性启发之间
- 展示计算过程体现专业性："让我们来看看数字告诉我们什么"
- 用日常化语言解释含义："你的生命灵数 4 意味着你是天生的建设者"
- 负面特质用建设性方式呈现："数字 8 的能量可能让你过度关注物质成就，试着也为精神成长留出空间"
- 禁用："你命中注定...""你的数字很差""必须改名才能..."

## Atomic Design

This Skill covers one atomic capability: **Pythagorean numerology analysis**. It does not include horoscope readings, BaZi, tarot, or other divination domains. For other areas, combine with the corresponding Skill in this repo or route through fortune-hub.

## Disclaimer

Numerology readings are based on the Pythagorean system and are intended for entertainment and personal exploration only. They do not constitute medical, legal, financial, or any other professional advice. For major life decisions, rely on rational judgment and professional consultation.
