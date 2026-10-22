# AI Use Tier 2 Disclosure Module 2

## Interaction 1 - Guided Example

**Task**: Generate a formula for an "Early High-Value" classification column.

**Tool**: Claude (claude.ai), accessed [10-22-2026].

**Prompt**:
Role: You're a senior Excel analyst.

Task: Write an Excel formula for a custom column.

Context: I have a sales table with order_date in column B and
gross_revenue in column G. I want a new column that labels rows
as "Early High-Value" if the order date is between January 1, 2024
and January 30, 2024 AND the gross revenue is greater than $500.
Otherwise, label as "Standard."

Output format: Just the formula, no explanation. Suitable for
cell R2.

**Original output**:
`=IF(AND(B2>=DATE(2024,1,1), B2<=DATE(2024,1,30), G2>500), "Early High-Value", "Standard")`

**Verification**:
- Cell references: B2 and G2 both exist and hold the expected data. Confirmed.
- Function calls: IF, AND, DATE. All valid Excel functions. Confirmed.
- Boundary conditions: tested rows on January 1 ($750 revenue produced "Early High-Value"), January 31 ($750 revenue produced "Standard"), January 15 ($300 revenue produced "Standard"), and January 15 ($750 revenue produced "Early High-Value"). All matched expectations.

**Decision**: Accepted the formula as-is. Pasted into column R2 and filled down.

## Interaction 2 - Complex Formulas Explanation

**Task**: Explain the formula used in cell O2 of sales_2024, the IFERROR formula we created

**Tool**: Copilot, accessed [10-22-2026].

**Prompt**:
Highlighted cell, prompt "explain this formula"

**Original output**:
`sales_2024!O2` retrieves the customer’s segment:

```excel
=IFERROR(XLOOKUP(C2,customer_segments!A:A,customer_segments!B:B),"Unknown")
```

- Looks for customer `CUST-6442` from `sales_2024!C2`
- Searches column A on `customer_segments`
- Returns the corresponding segment from column B
- If the lookup fails, returns **“Unknown”**

For this customer, the result is **Lapsed**.

**Verification**:
- Cell references: Column A on customer_segments, column B custoer_segments, both exist. Confirmed it checks good
- Function calls: Uses IFERROR and XLOOKUP, both are valid formulas
- Boundary conditions: There are no boundary conditions on this formula

**Decision**: Explanation makes sense and references valid data in the sheet. Confirmed

## Interaction 3 - Chart Type Suggestion

**Task**: Generate a chart showing which email campaign had the highest open rate

**Tool**: Copilot, accessed [10-22-2026].

**Prompt**:
Role: You're a senior data visualization advisor.

Task: Recommend a chart type for a specific dashboard question.

Context: I'm building a one-page dashboard for a VP of Marketing.
Using the email_campaign_q4_2024 sheet for data.
The question is "Which campaign had a higher open rate" The audience needs the answer in five seconds.

Constraints: Excel chart. Must be readable on a one-page dashboard
alongside two other charts. Categories number 2.

Output format: 2-3 chart type options ranked from best to worst,
with one sentence of rationale per option.

**Original output**:
1. **Horizontal bar chart** — Best five-second comparison: two bars, a zero baseline, direct percentage labels, and the higher campaign highlighted.

2. **Dot plot** — More compact for a crowded dashboard while making the open-rate gap immediately visible with two labeled dots.

3. **Clustered column chart** — Familiar and readable, but uses more vertical space and is slightly slower to compare than horizontal bars.

**Verification**:
- A bar chart is indeed the best suggestion. It would show in 2 seconds what the more opened variant was in simple to read terms
- A dot plot could be confusing for a less technical audience and presents more visual noise
- A clustered column chart would make no sense as there are only 2 variants. If the data had more variants this might be more viable but it is not for the data we have.

**Decision**: Accepted the suggestion, a Bar chart is the best fast look solution to present this specific data. 

## Interaction 4 - Power Query M expression

**Task**: Generate an M expression for Power Query to show high value customers in the email_campaign_q4_2024 sheet and determine which variant they recieved 

**Tool**: Claude (claude.ai), accessed [10-22-2026].

**Prompt**:
Role: You're a senior excel analyst.

Task: Write a Power Query M expression to show which email marketing variant high value customers received.

Context: I have a sheet called  email_marketing_q4_2024 with customer_id and variant as columns. I also have a sheet called customer_segments containing customer_id and segment as columns. If a customer_id shows VIP in segment, identify and show what variant that customer recieved.

Output: Just the M expression, no explanation, exported to a table showing only the VIP customers

**Original output**:
```
let
    Source = Excel.CurrentWorkbook(),
    Emails = Source{[Name="email_marketing_q4_2024"]}[Content],
    Segments = Source{[Name="customer_segments"]}[Content],
    VIPOnly = Table.SelectRows(Segments, each [segment] = "VIP"),
    Joined = Table.NestedJoin(VIPOnly, {"customer_id"}, Emails, {"customer_id"}, "Emails", JoinKind.LeftOuter),
    Expanded = Table.ExpandTableColumn(Joined, "Emails", {"variant"}, {"variant"}),
    Result = Table.SelectColumns(Expanded, {"customer_id", "segment", "variant"})
in
    Result
```

**Verification**:
- Cell references: Sheet references are valid. 
- Function calls: Segments and joins are correctly written, nothing is referenced that doesn't exist

**Decision**: Accepted the formula as-is. This formula should join the tables and present only the VIP customers and which variant they recieved

## Interaction 5 - Two-AI Verification

**Task**: Generate a formula for an "Early High-Value" classification column.

**Tool**: Claude (claude.ai), Copilot, accessed [10-22-2026].

**Prompt**:
role: you're a senior excel analyst

task: write an excel formula for a custom column

Context: I have a returns table with product_name in column J and sku in column C. I want a new column that only shows instances of N/A in that column and returns the sku from column C to spot errors.

Output format: just the formula, no explanation, suitable for column AQ


**Original output**:
Claude

=IF(ISNA(J2), C2, "")

Copilot

=IF(ISNA(J2),C2,"")


**Verification**:
- Cell references: J2 and C2 both contain the data needed to show 
- Function calls: IF and ISNA are real functions and would return the expected results
- Boundary conditions: There are no boundary condition. The boundary is black and white

**Decision**: Did not accept the formula from either AI. These formulas will return the same error we got in the earlier assignment where the empty return shows as text and makes further analysis more complex. I would instead use a power query or filter instead of an IF to prevent that issue moving forward and reduce unnecessary reworking of data. 

## Interaction 6

**Task**: Identify quality issues in a data sample

**Tool**: Claude (claude.ai), accessed 10-12-2026.

**Prompt**:
Role: You're a senior data analyst.

Task: Identify data quality issues in this sample column of values.

Context: This is the return_reason column from a returns table at
an e-commerce company. The values are user-entered or selected from
a dropdown. I'm preparing the column for use in a pivot table that
aggregates by reason. About 50 sample values follow.

Constraints: Focus on issues that would cause a pivot table to
miscount or misaggregate (case inconsistencies, whitespace,
duplicate spellings of the same thing).

Output format: A numbered list of issues. For each issue, name the
problem and give a specific example from the sample.

Data:
[paste the 30-50 values here, one per line]

**Original output**:
Your sample has 49 values, and all of the problems I can see are case inconsistencies. Here is how they affect a pivot, with a note on whitespace at the end.

A quick note on why case matters. Excel and Google Sheets pivot tables usually treat “Damaged” and “damaged” as the same item, but SQL GROUP BY (Postgres, BigQuery, and others), pandas, and many BI tools treat them as different values. Since you didn’t say which tool you’re using, I’d fix these anyway, because the data then behaves the same everywhere.

Case inconsistency in “Damaged”. Nine rows say Damaged and one says damaged. In a case-sensitive tool this produces two rows, 9 and 1, instead of one row of 10.
Case inconsistency in “Quality issue”. Five rows say Quality issue and one says Quality Issue. This would split into 5 and 1 instead of 6.
Case inconsistency in “Not as described”. Five rows say Not as described and one says Not As Described. This would split into 5 and 1 instead of 6.
Inconsistent capitalization style across categories. Wrong Size is the only value in title case, and every other value uses sentence case (“Late delivery”, “Gift return”). It’s consistent with itself in this sample (both rows match), so it isn’t splitting today. But it suggests the values weren’t generated by one rule, and the next person to type Wrong size would create a new pivot row.
Whitespace: none visible, but I can’t rule it out. Leading and trailing spaces are invisible and are a classic cause of two identical-looking rows in a pivot. Pasting text into a chat often strips them, so I can’t confirm the sample is clean. To check the real column, compare LEN(cell) with LEN(TRIM(cell)), and any row where they differ has stray spaces.

Net effect: The sample has 10 distinct strings but only 7 real reasons, so a case-sensitive pivot would show three extra rows (the three variants above) with small counts.

Suggested fix: Standardize with TRIM plus a consistent case rule (for example, lowercase everything, then capitalize the first letter), or map values through a small lookup table. A lookup table is safer for long-term use because it also handles typos you haven’t seen yet. If the dropdown is the source of the entries, the mixed casing suggests some rows were free-typed, so tightening the dropdown would prevent the problem going forward.

**Verification**:
The issues with this data are easy to spot with extra spaces, characters, and capitalizations present in many rows. On simple visual review this is a valid suggestion 

**Decision**: Accepted the suggestion, created a return_reason_clean column to address formatting issues in user generated text responses

## Interaction 7

**Task**: Write a power query column for a custom expression

**Tool**: Claude (claude.ai), accessed 10-12-2026.

**Prompt**:
Role: You're a Power Query expert.

Task: Write a Power Query M expression for a custom column.

Context: I have a Power Query table with columns refund_amount and
gross_revenue (both numeric). I want to add a custom column called
"high_refund_ratio_flag" that returns "High" if refund_amount /
gross_revenue is greater than 0.5, "Standard" otherwise. Handle
the case where gross_revenue is zero (return "Zero Revenue" in
that case).

Constraints: M code suitable for paste into Power Query's Custom
Column dialog. Just the formula, no surrounding "let...in" block.

Output format: Just the M expression.

**Original output**:
if [gross_revenue] = 0 then "Zero Revenue" else if [refund_amount] / [gross_revenue] > 0.5 then "High" else "Standard"

**Verification**:
References all checked out, table output the requested data

**Decision**: Accepted the formula as-is. Produced the table in Power Query

## Interaction 8

**Task**: Interpret a T-Test and explain terms in both the learning material and the answer

**Tool**: Claude (claude.ai), accessed 10-12-2026.

**Prompt**:
Role: You're a statistician advising a working analyst.

Task: Help me interpret a t-test result correctly.

Context: I ran a two-sample t-test (Welch's, unequal variances)
comparing the average order value of VIP customers (n = 800,
mean = $187) and Regular customers (n = 3200, mean = $164). The
t-statistic was about 2.5 and the two-tailed p-value was 0.012. I'm
writing a memo for a non-technical VP of Marketing.

Constraints: I want a precise interpretation that doesn't overstate
what the p-value tells us. I also want a recommended phrasing for
the memo.

Output format: Two paragraphs. First: precise interpretation of
the test result. Second: a one-to-two-sentence recommended memo
phrasing.

**Original output**:
Welch’s t-test gives t ≈ 2.5 and p = 0.012. Read precisely, that means: if VIP and Regular customers truly had the same mean order value, a difference as large as the observed $23 ($187 vs. $164), or larger in either direction, would turn up in only about 1.2% of samples like this one. That is reasonably strong evidence against “no difference in average order value,” so the difference is unlikely to be sampling noise alone. It does not say there is a 98.8% chance the groups differ, it does not give the probability the null is true, and it says nothing about how large or important the difference is. Nor does it establish that VIP status causes higher spend, since VIP customers are self-selected or chosen on past behavior, which probably builds in higher spend from the start. Also note that with n = 800 and 3,200, even modest differences can reach significance, so the more useful numbers are the effect size and the confidence interval. Working back from your figures, the standard error is about $9.2, so a 95% CI for the difference is roughly $5 to $41. That is a wide range, which signals the true gap could be small or fairly large. (Reconstructed from your t and means, so please confirm against your software’s output.)

Recommended memo phrasing: “VIP customers spent about $23 more per order on average than Regular customers ($187 vs. $164), a difference unlikely to be due to chance alone (p = 0.012); the plausible range for the true gap is roughly $5 to $41. This shows the two groups differ, but not that VIP status itself drives the higher spend.”

**Verification**:
The calculations match what was shown in the workbook. The explanation follows the format shown in the learning material. 

**Decision**: Accepted the analysis and the explanations of terms. 

## Interaction 9

**Task**: Critique Talking Points on a memo

**Tool**: Claude (claude.ai), accessed 10-12-2026.

**Prompt**:
Role: You're a senior analyst coaching a junior analyst on how to
present findings to a non-technical stakeholder.

Task: Critique my draft talking points for clarity, accuracy, and
business framing.

Context: I'm presenting the results of an email-campaign A/B test
to a non-technical VP of Marketing. The audience cares about
practical impact and what to do next, not statistical method.

Constraints: My talking points should follow this structure:
(1) answer first, (2) effect size in business terms, (3) confidence
in plain language, (4) recommended action, (5) anticipated follow-up.

Common failure modes to flag: leading with methodology, speaking
in p-values, overstating precision, hedging when not needed, missing
recommendation, conflating statistical and practical significance.

Output format: For each of my five points, note (a) what's working
and (b) what should change, with a specific rewrite if a change is
needed. Then give an overall verdict.

My draft:

Variant B drove about 25 more purchases per 10,000 emails compared to variant A, a roughly 13% lift on conversion rate. At your normal campaign send volume, that's an extra 70 purchases per quarterly send, which translates to about $10,977 in additional revenue. The result is unlikely to be due to chance: a statistical test showed a p-value of 0.0335, with a 95% confidence interval for the lift of 0.0195 to 0.4805 percentage points. My recommendation is to make variant B the default subject line for the next quarterly campaign. If you want extra confidence before changing the default, I can rerun the test with the next campaign send to confirm.

**Original output**:
Your arithmetic holds together. The confidence interval is centered on 0.25 percentage points (25 per 10,000), the p-value matches the interval, and the numbers imply about 28,000 emails per send and roughly $157 per purchase. Please confirm those two assumptions match reality, because my rewrites lean on them. The problems are in the framing, not the math.

1. Answer first

(a) Working: You open with the result, not the method, and “purchases per 10,000 emails” is a business unit the VP can picture.

(b) Change: You never say that B won, so the VP has to infer it. You also offer two metrics at once (25 per 10,000 and 13%) without saying which matters, and “conversion rate” is undefined.

Rewrite: “Variant B won. It generated about 13% more purchases than A, which works out to roughly 25 extra purchases for every 10,000 emails.”

2. Effect size in business terms

(a) Working: Translating the lift into purchases and dollars at the VP’s real send volume is the most important move in the whole script. It answers “so what?”

(b) Change: $10,977 is false precision. It implies you know the number to the dollar, but your own interval says the true value could be anywhere from about $900 to $21,000. State the assumption behind the dollars too, so the number is checkable.

Rewrite: “At our usual send size, that’s about 70 extra purchases, or roughly $11,000 in extra revenue per quarterly send, assuming our typical order value of about $157 holds.”

3. Confidence in plain language

(a) Working: You put the conclusion (“unlikely to be due to chance”) before the statistics, which is the right instinct.

(b) Change: This is your biggest failure mode.

Jargon: The p-value and the interval in percentage points are method talk. The units also clash with the relative “13%” you gave earlier.
Loose wording: “Unlikely to be due to chance” is a common shorthand, but a p-value doesn’t measure the probability that the result is a fluke. It says how surprising a gap this size would be if the two subject lines were truly identical. For your result, that’s about 1 time in 30.
Missing message: The lower end of your interval is almost zero. The honest takeaway is “confident B is better, less sure by how much.” Say that explicitly rather than hiding it in a decimal.

Rewrite: “I’m fairly confident B is genuinely better. A gap this big would show up by luck only about 1 time in 30 if the two were really equal. What I’m less sure about is how much better. My best estimate is $11,000 per send, but the plausible range runs from under $1,000 to about $21,000.”

The principle is to be firm about direction and honest about magnitude. That is not hedging, because you’re telling the VP exactly what you do and don’t know.

4. Recommended action

(a) Working: It’s specific, scoped (next quarterly campaign), and comes before any caveat.

(b) Change: Add the why. The VP will feel safer acting if they hear that the decision is cheap and reversible.

Rewrite: “I recommend making B the default subject line for the next quarterly campaign. It costs nothing to switch, it’s easy to reverse, and even the pessimistic end of our range is a small gain, not a loss.”

5. Anticipated follow-up

(a) Working: You’re anticipating the “should we be surer?” question, which is the right one to prepare for.

(b) Change: As written, it’s an open offer to rerun the test, which reads as hedging and undercuts your recommendation. It also isn’t free. If half the list gets the weaker subject line again, you give up about 35 purchases (roughly $5,500 in expected revenue) to confirm something you can already act on. A better option is to ship B and keep a small slice on A, so you keep measuring at almost no cost.

Rewrite: “If you want more certainty, you don’t have to pay for it. We send B to most of the list and keep a small slice on A, so we keep tracking whether the lift holds. The question I’d expect next is whether this carries over to other campaigns. Honestly, this test covers this audience and this send, so I’d treat it as a strong hint, not a rule.”

Overall verdict

This is a strong draft. The structure is right, the numbers are consistent, and you avoided the worst trap of leading with methodology. In priority order, fix these:

Point 3: Remove the p-value and interval, and turn the range into dollars.
Point 2: Round to about $11K and state the order-value assumption.
Point 5: Replace the open rerun offer with the low-cost holdout.

Points 1 and 4 need only small edits.

Stitched together

“Variant B won. It generated about 13% more purchases than A, roughly 25 extra per 10,000 emails. At our usual send size, that’s about 70 extra purchases, or around $11,000 per quarterly send, assuming our typical order value holds. I’m fairly confident B is genuinely better, since a gap this big would show up by luck only about 1 time in 30 if the two were equal. I’m less sure how much better: the plausible range is under $1,000 to about $21,000. I recommend making B the default for the next campaign. It costs nothing to switch, it’s easy to reverse, and even the low end is a small gain. If you want more certainty, we can keep a small slice on A to keep tracking the lift.”


**Verification**:
The AI critique found inconsistent wording and long winded answers that were not appropriate for this setting. 

**Decision**: Accepted insight from the critique and adjusted wording and how much unnecessary information was in the short memo


