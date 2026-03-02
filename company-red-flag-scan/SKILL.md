---
name: company-red-flag-scan
description: Investigate a listed company's negative history and red flags in Chinese, including short-seller reports, regulatory penalties, accounting fraud, litigation, negative public controversies, and reverse stock splits or share consolidations. Use when the user asks for “排雷”, “负面信息梳理”, “黑历史”, “公司是否暴雷过”, “有没有被做空/处罚/起诉过”, or wants a concise source-linked due diligence note on a target company.
---

# Company Red Flag Scan

## Overview

Use this skill to produce a concise Chinese investment-research memo focused on a target company's negative history and governance red flags.

Cover six checks in a fixed order:

1. 做空报告
2. 监管处罚
3. 财务造假
4. 诉讼
5. 负面舆情
6. 合股历史

Read [references/source-priority.md](references/source-priority.md) before searching so source selection and query patterns stay consistent.

## Input Contract

Start by identifying:

- 公司名称
- 股票代码或交易所
- 是否存在常见英文名、旧称、简称

If the user only gives a company name, resolve the listed entity first and note the full legal or listed name used for the search.

## Workflow

### 1. Define The Search Entity

Normalize the target into a search set:

- 中文全称
- 英文全称
- 常见简称
- 股票代码
- 历史名称或品牌名

For cross-listed companies, make sure the findings refer to the same legal or listed entity instead of an affiliate with a similar name.

### 2. Search By Checklist

Run the six checks in this order and stop only after each item is either supported by evidence or marked `未发现公开可靠记录`.

#### A. 做空报告

Look for:

- Known short sellers or activist research firms
- Named reports, letters, or public presentations
- Publication date

Record:

- 是否存在
- 机构名称
- 发布时间
- 链接

#### B. 监管处罚

Look for enforcement, penalty, censure, settlement, or disciplinary actions from regulators such as:

- 中国证监会及交易所
- 美国 SEC
- 香港 SFC / 联交所
- 其他与上市地匹配的主要监管机构

Record:

- 是否存在
- 监管机构
- 处罚或执法时间
- 事由
- 链接

#### C. 财务造假

Look for:

- Fraud, misstatement, fabricated revenue, false disclosure, internal-control failure
- Accounting restatement tied to misconduct
- Court or regulator findings

Do not label a company as `财务造假` based only on market rumors. Require a strong source.

Record:

- 是否存在
- 事件时间
- 核心事实
- 链接

#### D. 诉讼

Look for material lawsuits, class actions, shareholder suits, fraud suits, contract disputes, insolvency-related claims, or enforcement litigation.

Record:

- 是否存在
- 时间
- 原因
- 当前已知进展
- 链接

#### E. 负面舆情

Search at minimum with these Chinese keywords combined with the company name:

- 老千
- 庄家
- 质疑
- 危机
- 风波

Add company-specific risk words when relevant, but separate rumor from substantiated reporting.

Record:

- 是否存在
- 关键词或事件标签
- 时间
- 链接

#### F. 合股历史

This mainly applies to Hong Kong listed names. Search for:

- 合股
- 股份合并
- Share consolidation
- Reverse split

Record:

- 是否存在
- 时间
- 方案摘要
- 链接

### 3. Evaluate Evidence Strength

Use this hierarchy:

1. Official regulator, court, exchange, company filings
2. Named research institutions or established media
3. Reputable market commentary or archive copies when the primary link is unavailable

If a finding only appears in forum posts, reposts, or anonymous commentary, do not state it as fact. Mark it as `存在市场质疑，但缺少公开可靠证据`.

### 4. Write The Output

Write in Chinese and keep the tone factual, restrained, and memo-like.

Use this exact section order:

```text
公司：...
上市地/代码：...
检索实体：中文名 / 英文名 / 代码
检索日期：YYYY-MM-DD
风险判断：高风险 / 有历史瑕疵 / 未见重大公开红旗
核心关注点：
- ...
- ...
备注：如公司存在同名主体、跨市场上市或历史更名，在此说明口径。

## 1. 做空报告
结论：...
- 时间 | 机构 | 关键指控或结论 | 链接
- ...

## 2. 监管处罚
结论：...
- 时间 | 监管机构 | 事由 | 处置结果 | 链接
- ...

## 3. 财务造假
结论：...
- 时间 | 事件概述 | 证据层级 | 链接
- ...

## 4. 诉讼
结论：...
- 时间 | 原因 | 当前已知进展 | 链接
- ...

## 5. 负面舆情
结论：...
- 时间 | 关键词或事件标签 | 摘要 | 链接
- ...

## 6. 合股历史
结论：...
- 时间 | 方案摘要 | 背景或后续影响 | 链接
- ...

## 来源
- 机构或网站 | 标题 | YYYY-MM-DD | 链接
- ...
```

Apply these writing rules:

- `核心关注点` 只提最值得投研进一步核查的两到三点，不重复所有事实
- Each checklist section begins with a one-line conclusion using one of:
  - `发现明确记录`
  - `未见公开可靠记录`
  - `存在市场质疑，但证据不足`
- Give exact dates whenever known
- Prefer one to three bullets per section
- Present facts in time order when multiple events exist
- End with links, not bare domain names
- Do not pad the memo with generic company background, valuation views, or投资建议
- When an item is disputed, separate `已确认事实` from `市场指控`

## Decision Rules

- `高风险`: multiple confirmed negative events, or any confirmed fraud / major enforcement / repeated capital-market controversy
- `有历史瑕疵`: one or more confirmed incidents, but the evidence does not indicate a persistent or extreme risk profile
- `未见重大公开红旗`: no strong-source evidence found for the checklist as of the search date

If evidence is mixed, state the uncertainty explicitly instead of forcing a hard label.

## Memo Style

Aim for a house-style investment memo rather than a compliance checklist.

Write with these habits:

- Put the bottom line first
- Compress each event into one sentence before adding bullets
- Prefer `需要关注`, `需进一步核查`, `历史上曾出现`, `公开资料显示` over emotionally loaded labels
- Treat `老千`, `庄家` and similar terms as search cues, not the memo's own voice, unless quoting a source
- Keep the final note readable in three minutes
