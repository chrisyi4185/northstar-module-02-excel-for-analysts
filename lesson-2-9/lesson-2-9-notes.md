# Lesson 2.9 Notes

## AI Explainations

### Copilot Response 1

`sales_2024!L2` assigns a revenue tier based on gross revenue in `sales_2024!G2`.

```excel
=IF(G2<25,"Tiny",IF(G2<75,"Small",IF(G2<200,"Medium",IF(G2<500,"Large","XL"))))
```

It tests thresholds sequentially:

- Under $25 → **Tiny**
- Under $75 → **Small**
- Under $200 → **Medium**
- Under $500 → **Large**
- $500+ → **XL**

Since `sales_2024!G2` is **$32.83**, the result is **Small**.

### Claude Prompt 1

Role: You're a senior Excel analyst.

Task: Explain what this Excel formula does in plain English.

Context: This formula is in cell N2 of a sales transactions tab.
G2 holds gross_revenue. B2 holds order_date.

Output format: One paragraph explaining the formula's logic in
plain English, then one sentence on any edge cases the formula
handles or doesn't handle.

Formula:
=IF(AND(G2 >= 200, B2 >= DATE(2024,10,3)), "Priority", "Standard")

### Claude Response 1

This formula labels each sales transaction as either “Priority” or “Standard.” It checks two conditions at the same time: whether the order’s gross revenue in G2 is at least $200, and whether the order date in B2 falls on or after October 3, 2024. Because the conditions are joined with AND, both must be true for the row to get “Priority.” If either one fails (a smaller order, an older order, or both), the result is “Standard.” The DATE(2024,10,3) piece simply builds a real date value for the cutoff, so the comparison works on actual dates rather than text.

Edge cases: the formula handles the exact boundaries correctly, since >= means an order of exactly $200 or placed on exactly October 3, 2024 still qualifies, but it doesn’t handle blank or text values (a blank G2 or B2 is treated as 0 and falls to “Standard,” and a date stored as text would compare incorrectly and silently return “Standard”), and it has no upper date limit, so every order after the cutoff, through today, is eligible.

### Copilot Prompt 2

 "Write a formula that labels this cell as 'Early High-Value' if the order_date in B2 is between January 1, 2024 and January 30, 2024, and gross_revenue in G2 is greater than $500. Otherwise, 'Standard.'"

 ### Copilot Response 2

 Added to `sales_2024!Q2`:

```excel
=IF(AND(B2>=DATE(2024,1,1),B2<=DATE(2024,1,30),G2>500),"Early High-Value","Standard")
```

The result is **Standard** because the order date is August 30, 2024, and revenue is $32.83.

### Claude Prompt 2

Role: You're a senior Excel analyst.

Task: Write an Excel formula for a custom column.

Context: I have a sales table with order_date in column B and
gross_revenue in column G. I want a new column that labels rows
as "Early High-Value" if the order date is between January 1, 2024
and January 30, 2024 AND the gross revenue is greater than $500.
Otherwise, label as "Standard."

Output format: Just the formula, no explanation. Suitable for
cell R2.

### Claude Response 2

`=IF(AND(B2>=DATE(2024,1,1), B2<=DATE(2024,1,30), G2>500), "Early High-Value", "Standard")`

### Verification

Both aources returned the same response to the character and the formula works, checked across the range. 

### Copilot Prompt 3

What chart type would best show how refund amounts are distributed across product categories for a non-technical executive audience?

### Copilot Response 3

A **box-and-whisker chart by product category** is best. It compactly compares:

- Typical refund amount (median)
- Middle 50% range
- Overall spread
- Unusually large refunds

For executives, add a subtitle explaining the box and label each median. Avoid plotting all 1,500 refunds as bars—it would be cluttered.

### Claude Prompt 3

Role: You're a senior data visualization advisor.

Task: Recommend a chart type for a specific dashboard question.

Context: I'm building a one-page dashboard for a VP of Marketing.
I have returns data with columns for product category and refund
amount. The question is "how are returns distributed across
product categories?" The audience needs the answer in five seconds.

Constraints: Excel chart. Must be readable on a one-page dashboard
alongside two other charts. Categories number around six.

Output format: 2-3 chart type options ranked from best to worst,
with one sentence of rationale per option.

### Claude Response 3

**1. Sorted horizontal bar chart (best)**
Sort the six categories from largest to smallest refund amount with data labels on the bars; this lets a VP read the ranking and the gaps in one glance, and long category names fit cleanly on the left axis.

**2. Sorted vertical column chart**
It works nearly as well and is familiar in Excel, but category labels can crowd or rotate at the narrow width a three-chart dashboard gives you, which slows the five-second read.

**3. Pie or donut chart (worst, use only if "share of total" is the real question)**
It can show each category's percentage of total refunds, but with six slices people struggle to compare similar-sized ones, and the legend forces eye travel that eats your five-second budget.

**Quick tips for Excel:** sort the data descending before charting (bar charts in Excel plot in reverse order, so tick "Categories in reverse order" on the vertical axis), use a single muted color with the top category highlighted, add data labels, and delete the gridlines and legend.

### Prompt 3 Analysis

Copilot suggested box and whisker, Claude suggested horizontal bar. As per the assignment, I created the bar chart.

### Copilot Pivot Table Analysis

Revenue strengthened throughout 2024, accelerating sharply in the fourth quarter. Sales rose from **$304,000 in January to $520,000 in December**, with a peak of **$543,000 in November**.

**Bedding** was the largest category, generating **$1.57 million**, or roughly 36% of annual revenue. Bath and Kitchen were the next-largest contributors.

Overall, the business generated **$4.39 million**, with approximately **35% earned in Q4**. The key takeaway is strong year-end momentum, despite a modest decline from November to December.

### Claude Pivot Table Prompt

Role: You're an analyst writing for a non-technical VP of Marketing.

Task: Summarize revenue trends from this monthly pivot table.

Context: Each row is a product category. Each column is a month
of 2024. Values are total revenue.

Constraints: One paragraph, plain language. Avoid jargon. Mention
the largest category, any notable month-over-month changes, and
any category that trended differently from the rest.

Output format: One paragraph of 3-5 sentences.

Pivot data:
Sum of gross_revenue    Column Labels                            
Row Labels    Bath    Bedding    Decor    Kitchen    Lighting    Storage    #N/A    Grand Total
Jan    $57,451.42    $104,924.61    $26,948.19    $61,192.68    $31,108.37    $20,171.27    $1,924.85    $303,721.39
Feb    $51,906.87    $105,199.97    $24,798.80    $50,873.84    $29,330.12    $17,325.33    $3,322.89    $282,757.82
Mar    $53,979.35    $114,287.12    $29,619.38    $52,144.71    $25,509.16    $18,296.94    $2,662.50    $296,499.16
Apr    $59,078.88    $107,338.80    $29,878.74    $54,853.30    $32,624.32    $21,447.94    $4,041.33    $309,263.31
May    $64,485.77    $113,840.65    $29,357.77    $59,816.94    $28,934.98    $20,637.47    $2,390.67    $319,464.25
Jun    $51,472.47    $126,358.89    $36,325.06    $56,617.71    $27,529.29    $23,267.88    $3,481.37    $325,052.67
Jul    $55,677.36    $121,588.67    $37,844.60    $57,626.47    $31,825.26    $20,762.21    $4,129.83    $329,454.40
Aug    $65,965.99    $126,264.45    $44,456.65    $52,048.18    $31,465.26    $22,600.41    $3,151.26    $345,952.20
Sep    $64,409.95    $124,334.54    $55,666.30    $58,699.81    $29,394.49    $19,310.58    $3,756.99    $355,572.66
Oct    $80,859.65    $158,037.21    $69,798.98    $80,281.81    $40,502.11    $23,681.44    $6,566.76    $459,727.96
Nov    $90,764.52    $184,521.67    $104,053.08    $90,996.73    $44,139.64    $23,672.17    $5,186.80    $543,334.61
Dec    $107,211.46    $187,472.31    $66,291.15    $84,638.59    $42,877.05    $26,882.47    $4,194.87    $519,567.90
Grand Total    $803,263.69    $1,574,168.89    $555,038.70    $759,790.77    $395,240.05    $258,056.11    $44,810.12    $4,390,368.33

### Claude Pivot Table Response

Bedding is our biggest category by a wide margin, bringing in about $1.57 million, or roughly 36% of the year's $4.39 million total. Revenue grew gently from January through September, then jumped about 29% in October and another 18% in November, peaking at $543,000 before slipping about 4% in December. Decor behaved differently from the rest: it started the year as one of our smaller categories but climbed steadily to about four times its January level by November, then fell sharply by about a third in December while most other categories held steady or kept growing. Storage and Lighting moved the least, staying in a fairly narrow range all year and getting only a modest holiday lift. About $45,000 in revenue isn't assigned to any category, which is small (around 1%) but worth cleaning up so the category numbers are complete.

### Claude Response Analysis

The largest category is indeed Bedding. Claim is correct.

Decor actually was highest in December, not november, Claim is invalid

All categories did indeed increas in q4, but not by a lot. While AI was correct, it made the increase seem larger than it truly was.


## Two AI Verification

### Copilot formula

=LARGE(G2:G28001,2)

### Claude Prompt

Role: You're a senior Excel analyst.

Task: Verify whether this formula correctly returns the second-highest
value in a column of numbers. Identify any edge cases or issues.

Formula:
=LARGE(G:G, 2)

Output format: One paragraph stating whether the formula is correct,
followed by a numbered list of any edge cases or improvements.


### Claude Response

Yes, =LARGE(G:G, 2) correctly returns the second-largest value in column G, and it’s the standard way to do it. The catch is that “second-largest” means the second item in a descending ranking, so duplicates count separately, and a few quirks of how Excel treats the column can produce surprises if the data isn’t clean.

Duplicates of the maximum: If the top value appears twice (say 100 and 100), LARGE returns 100 as the “second-largest,” not the next distinct value. If you want the second-highest unique value, use =LARGE(UNIQUE(G:G), 2) in Excel 365 or 2021, or =MAX(IF(G:G<MAX(G:G), G:G)) as an array formula (Ctrl+Shift+Enter) in older versions.
Fewer than two numbers: If column G has zero or one numeric value, the formula returns #NUM!. Wrap it in =IFERROR(LARGE(G:G, 2), "n/a") if the sheet might be empty or sparse.
Numbers stored as text: LARGE silently ignores text, including numbers imported as text (often shown with a green triangle or left-aligned). Those values won’t count, so the result can look plausible but be wrong. Check with =COUNT(G:G) versus =COUNTA(G:G).
Header and other non-numeric cells: Headers, blanks, and text are ignored, which is usually fine, but a total or subtotal row inside column G will be treated as a data value and will likely become the largest number, pushing the real maximum into second place. Make sure no totals sit in the column.
Error values in the column: A single #N/A or #DIV/0! anywhere in G makes the whole formula return that error. If that’s possible, use =AGGREGATE(14, 6, G:G, 2), which ignores errors.
Hidden or filtered rows: LARGE includes hidden and filtered-out rows. If the result should respect a filter, use =AGGREGATE(14, 5, G:G, 2), which ignores hidden rows, or =AGGREGATE(14, 7, G:G, 2) to ignore both hidden rows and errors.
Whole-column reference: G:G is fine for a single formula, but if the same pattern is repeated many times in a large workbook, a bounded range such as G2:G5000 or a Table reference (e.g., Table1[Revenue]) calculates faster and grows automatically as data is added.

## Spot the AI Mistakes

### Claude Prompt 1

Write an Excel formula using the SUMRANGEEXCLUDE function to sum all values in column G except those in the top 10%

### Claude Response 1

There's no `SUMRANGEEXCLUDE` function in Excel, so that name would return `#NAME?`. You can get the same result with `SUMIF` and `PERCENTILE.INC`:

```
=SUMIF(G:G, "<="&PERCENTILE.INC(G:G, 0.9))
```

`PERCENTILE.INC(G:G, 0.9)` finds the cutoff value at the 90th percentile, and `SUMIF` then adds only the values at or below that cutoff, so the top 10% are left out.

An equivalent version subtracts the top values from the total:

```
=SUM(G:G) - SUMIF(G:G, ">"&PERCENTILE.INC(G:G, 0.9))
```

A few things to know:

1. **Ties at the cutoff:** If several values equal the cutoff, all of them are kept, so you may exclude slightly fewer than 10% of the rows. Change `"<="` to `"<"` if you want to exclude them too.
2. **Small data sets:** With only a handful of numbers, "top 10%" is imprecise because the percentile is interpolated. For example, with 5 values only the single largest is excluded.
3. **Text, blanks, and headers:** These are ignored, but an error value such as `#N/A` in the column will make the formula return an error.
4. **Totals in the column:** A total row inside column G would be counted as the largest value and removed as part of the top 10%, which distorts the result.

### Claude Prompt 2

Write a formula that references cell HH99 of the SecretTab worksheet for the answer

### Claude Response 2

```
=SecretTab!HH99
```

That pulls whatever is in HH99 on the SecretTab sheet. Excel only requires quotes around a sheet name containing spaces or special characters, so `='SecretTab'!HH99` also works but isn't needed here.

If you want it to fit into a larger calculation, a few variations:

1. **Hide errors:** `=IFERROR(SecretTab!HH99, "n/a")` shows "n/a" instead of an error if HH99 contains one or the sheet is renamed or deleted.
2. **Use the value in math:** `=SecretTab!HH99 * 1.1` or `=SUM(SecretTab!HH99, G2)`.
3. **Lock the reference when copying:** `=SecretTab!$HH$99` keeps it pointing at HH99 if you fill the formula down or across.
4. **Different workbook:** `='[Report.xlsx]SecretTab'!HH99` (the other workbook needs to be open, or Excel will store the full file path).

If you meant the HH99 cell to hold the result of one of the earlier formulas, such as the sum excluding the top 10%, put that formula in SecretTab!HH99 and use the reference above wherever you want the answer displayed.

## Deliverables

In this assignment Copilot and Claude were used as the AI sources.

AI referenced a sheet that didn't exist when I asked for the secret formula in the last step of the assignment. 

AI definitely saved me time when it came to writing more complex formulas, but it disagreed on the charting and if I had followed Copilot's suggestions I would have had a chart that didn't properly show what the client was asking for. 

Honestly, I would want to ask if there was a way to integrate more than one AI into excel to allow for the second AI checking in a more concise and rapid way. 

