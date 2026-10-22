# Lesson 2.7 Notes

## Draft talking points

Variant B drove about 25 more purchases per 10,000 emails compared to variant A, a roughly 13% lift on conversion rate. At your normal campaign send volume, that's an extra 70 purchases per quarterly send, which translates to about $10,977 in additional revenue. The result is unlikely to be due to chance: a statistical test showed a p-value of 0.0335, with a 95% confidence interval for the lift of 0.0195 to 0.4805 percentage points. My recommendation is to make variant B the default subject line for the next quarterly campaign. If you want extra confidence before changing the default, I can rerun the test with the next campaign send to confirm.

## AI Demonstration

### Prompt Used

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

### Claude Response

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

## Results Found
Effect Size = 
CI = 
p-value = 0.033

## Result Significance

The result is both statistically and practically significant

## Final Recommendation for Beatrix

Variant B is your winner. It brought in 13% more purchases than A, about 25 extra per 10,000 emails. Assuming our regular group size, that's approximately 70 more purchases or about $11,000 per quarterly send, assuming order value remains the same as the current average. I'm relatively confident that B is truly the better option because a gap this large would only appear once in 30 samples if the two were the same. I'm not as confident in how much better B is as the range is relatively large (under $1,000 to $21,000). I would recommend making B your go to default in the next campaign. Even on the lowest end it would still be a small increase. For more certainty, we can always run additional testing by keeping a small population recieving A to keep an eye on the lift going forward. 

## AI Disclosure Statement

Used Claude to critique mt draft of talking points. I kept many of the edits because they were more clearly explained than when I tried to explain them, but made sure to include more options on tracking going forward as there are more options available than just keeping some of A as a control.