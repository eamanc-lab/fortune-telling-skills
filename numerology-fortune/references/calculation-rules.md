# Numerology Calculation Rules

## Table of Contents

- [I. Letter-to-Number Conversion Chart (Pythagorean System)](#letter-to-number-conversion-chart-pythagorean-system)
- [II. Reduction Rules](#reduction-rules)
- [III. The Five Core Numbers](#the-five-core-numbers)
  - [1. Life Path Number](#1-life-path-number)
  - [2. Expression Number](#2-expression-number--destiny-number)
  - [3. Soul Urge Number](#3-soul-urge-number--hearts-desire-number)
  - [4. Personality Number](#4-personality-number)
  - [5. Birthday Number](#5-birthday-number)
- [IV. Personal Cycle Calculations](#personal-cycle-calculations)
  - [Personal Year](#personal-year)
  - [Personal Month](#personal-month)
  - [Personal Day](#personal-day)

## Letter-to-Number Conversion Chart (Pythagorean System)

```
1  2  3  4  5  6  7  8  9
A  B  C  D  E  F  G  H  I
J  K  L  M  N  O  P  Q  R
S  T  U  V  W  X  Y  Z
```

**Formula**: `(letter position - 1) % 9 + 1`, i.e. `(ord(letter) - ord('A')) % 9 + 1`

**Vowels**: A, E, I, O, U

**Special rule for Y**: Y is treated as a vowel when it functions as one phonetically (e.g., the leading Y in "Yvonne," or the Y in "Rhys"). Otherwise, Y is treated as a consonant. When in doubt, default to consonant.

## Reduction Rules

Reduce any positive integer to a single digit (1–9), but **preserve Master Numbers** (11, 22, 33) — do not reduce them further.

```
reduce(n):
  while n > 9 and n is not 11, 22, or 33:
    n = sum of digits of n
  return n
```

## The Five Core Numbers

### 1. Life Path Number

**Source**: Date of birth
**Significance**: The most important number — represents your life's central theme and purpose

**Calculation**: Reduce the birth year, month, and day **separately**, then add them together and reduce the sum.

> Key rule: Year, month, and day must each be reduced individually before being added. Adding all digits together at once can cause you to miss a Master Number.

```
Example: June 15, 1990

Month: 6 → 6
Day: 15 → 1+5 = 6
Year: 1990 → 1+9+9+0 = 19 → 1+9 = 10 → 1+0 = 1

Sum: 6 + 6 + 1 = 13 → 1+3 = 4

Life Path Number = 4
```

### 2. Expression Number / Destiny Number

**Source**: **All letters** of the full legal name at birth
**Meaning**: Natural talents, abilities, and life purpose

**Calculation**: Convert each letter of the full name to its number value, reduce the sum for each name segment, then reduce the total.

```
Example: JOHN SMITH

J=1 O=6 H=8 N=5 → 20 → 2
S=1 M=4 I=9 T=2 H=8 → 24 → 6

Total: 2 + 6 = 8

Expression Number = 8
```

### 3. Soul Urge Number / Heart's Desire Number

**Source**: **All vowels** in the full name
**Meaning**: Your deepest inner desires and motivations

```
Example: JOHN SMITH

Vowels: O(6) + I(9) = 15 → 1+5 = 6

Soul Urge Number = 6
```

### 4. Personality Number

**Source**: **All consonants** in the full name
**Meaning**: The outward impression you make — how others perceive you

```
Example: JOHN SMITH

Consonants: J(1) H(8) N(5) + S(1) M(4) T(2) H(8) = 29 → 2+9 = 11

Personality Number = 11 (Master Number — do not reduce further)
```

**Verification check**: The raw totals of Soul Urge + Personality = the raw total of the Expression Number.

### 5. Birthday Number

**Source**: The "day" portion of the birth date
**Meaning**: A special talent or gift

```
Day 15 → 1+5 = 6
Birthday Number = 6
```

Day 11 = 11, Day 22 = 22 (Master Numbers are preserved).

## Personal Cycle Calculations

### Personal Year

```
Personal Year = reduce(reduce(birth month) + reduce(birth day) + reduce(sum of digits of current year))
```

```
Example: Birthday June 15, year 2026

Month: 6
Day: 1+5 = 6
Year: 2+0+2+6 = 10 → 1

Personal Year = 6 + 6 + 1 = 13 → 4
```

Personal Year cycles in a repeating 1–9 sequence.

### Personal Month

```
Personal Month = reduce(Personal Year number + current month)
```

### Personal Day

```
Personal Day = reduce(Personal Month number + current date)
```
