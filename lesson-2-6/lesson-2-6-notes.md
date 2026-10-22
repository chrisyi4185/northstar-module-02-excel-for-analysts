# Lesson 2.6 Applied Statistics in Excel

## Step 5 Verification

### Prompt Used

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

### Claude response

Welch’s t-test gives t ≈ 2.5 and p = 0.012. Read precisely, that means: if VIP and Regular customers truly had the same mean order value, a difference as large as the observed $23 ($187 vs. $164), or larger in either direction, would turn up in only about 1.2% of samples like this one. That is reasonably strong evidence against “no difference in average order value,” so the difference is unlikely to be sampling noise alone. It does not say there is a 98.8% chance the groups differ, it does not give the probability the null is true, and it says nothing about how large or important the difference is. Nor does it establish that VIP status causes higher spend, since VIP customers are self-selected or chosen on past behavior, which probably builds in higher spend from the start. Also note that with n = 800 and 3,200, even modest differences can reach significance, so the more useful numbers are the effect size and the confidence interval. Working back from your figures, the standard error is about $9.2, so a 95% CI for the difference is roughly $5 to $41. That is a wide range, which signals the true gap could be small or fairly large. (Reconstructed from your t and means, so please confirm against your software’s output.)

Recommended memo phrasing: “VIP customers spent about $23 more per order on average than Regular customers ($187 vs. $164), a difference unlikely to be due to chance alone (p = 0.012); the plausible range for the true gap is roughly $5 to $41. This shows the two groups differ, but not that VIP status itself drives the higher spend.”

## Deliverables

### Stats Computed
    Calculated:
        mean
        variance
        count
        one and two tailed P values
        standard deviation
        half width
        95% confidence interval upper and lower
        IQR
        Max and Min

### Histogram shape and distribution
 The histogram is strongly right skewed and unimodal with a peak in the bin with $58.95 to $83.95. 

### T-Test

Completes a 2-sample t-test assuming unequal variances using the Excel Data Analysis ToolPak to compare VIP and Regular customer categories. The VIP group averages $187 and the Regular group averages $164, showing the difference of $23 that Beatrix was looking into. The standard deviation is approximately $231, which fits the histogram result showing a strong right skew as it is larger than either mean. The 2-tailed p-value of 0.012 is valid as we asked a neutral question not looking for a specific direction. 


### Memo for the T-Test

In the 2024 data, VIP customers spent $23 more on average than Regular customers($187 vs. $164). This data was confirmed by a statistical test, showing the difference is unlikely to be due to chance alone (p=0.012). Per the confidence interval calculated, the real gap could be anywhere from $5 to $41. While this shows that two groups differ, it does not indicate that VIP status alone is causal to the higher spending.  

## AI Use Disclosure

"Used Claude to draft and verify a t-test interpretation. The interpretation correctly stated p-value semantics. I verified each statement against the textbook definition. I added a note about practical-vs-statistical significance the AI didn't include, since it matters for our specific use case."