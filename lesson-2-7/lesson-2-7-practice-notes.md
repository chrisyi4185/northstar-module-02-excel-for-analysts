# Lesson 2.7 Practice Exercise Notes

## Purchase Results
In comparison to the results from the email campaign in regards to purchases, the results for click through rate are much less significant. While variant B does have a higher click through rate than variant A, the difference is minute but it is indeed consistent with variant B having more purchases and a higher click through rate. 

## Draft Talking Points

Variant B did drive a small increase in click through rate (2% lift). At normal campaign send rates, that's an extra 17 purchases per 10,000 emails. At normal campaign send volume, that would be 47 additional purchases per quarterly send, translating to approximately $7,000 in additional revenue. The result is likely due to random chance as the p-value of 0.47 indicates that the chance of seeing a difference at least as extreme would be 47% in either direction. This is confirmed with the confidence interval containing both 0 change and negative change. While the click rate and the conversion rate both point to variant B being the way to go, I wouldn't expect to see as large of a change in click rate on implementation as we would see in conversion rate alone. My recommendation would be to move forward with Variant B as the standard for the next campaign, but if we would like some extra confidence in the continued effect of the change, we can keep a small test group with variant A and rerun the test once those results come back.  

## Deliverables

### Click-rate Result

Effect Size: small to negligible
CI: -0.29% to 0.64%
p-value: 0.47

### Result Alignment

While the results align that variant B is the more effective option in both the click through and conversion rates, the difference on click through rate is negligible and not statistically significant. The confidence interval including 0 and negative results indicates that the chance of variant B having a positive effect on purchases is almost completely negligible. 

### Final Talking Points

Variant B was slightly ahead on clicks, but the difference is small enough that we can't tell it apart from luck. B's click rate was 8.7% versus 8.5% for A. On a send this size that's approximately 48 extra clicks. I'm not convinced that the lift is real here. If the two emails were identical, we would see a gap this big about half the time. Realistically we are looking at a range of 80 less clicks to 180 more clicks per send. I'd rather plan on the lower end to be safe. I would recommend making B the default going forward. There is no change in cost, there's no indication that it's a worse option, and from both tests we have run, the upside looks plausible. If you want a result we can trust more confidently, I would look at bigger changes like different offers or subject lines as a bolder test would tell us more. 

### Recommendation if outcomes Disagreed

If the outcomes disagreed, I would recommend additional testing and reviews of other metrics to figure out which was the correct causation and to eliminate confounding. 

### AI Critique Exchange

#### Prompt Used

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

Variant B did drive a small increase in click through rate (2% lift). At normal campaign send rates, that's an extra 17 purchases per 10,000 emails. At normal campaign send volume, that would be 47 additional purchases per quarterly send, translating to approximately $7,000 in additional revenue. The result is likely due to random chance as the p-value of 0.47 indicates that the chance of seeing a difference at least as extreme would be 47% in either direction. This is confirmed with the confidence interval containing both 0 change and negative change. While the click rate and the conversion rate both point to variant B being the way to go, I wouldn't expect to see as large of a change in click rate on implementation as we would see in conversion rate alone. My recommendation would be to move forward with Variant B as the standard for the next campaign, but if we would like some extra confidence in the continued effect of the change, we can keep a small test group with variant A and rerun the test once those results come back.

#### Claude Response

# Critique of your talking points

Your instincts are good: you quantified the impact, you were honest about uncertainty, and you made a recommendation. The main problem is that the draft contradicts itself. It opens by saying B "did drive" an increase, then says the result is "likely due to random chance." A VP will hear the first sentence and stop listening to the rest.

Your draft doesn't map one-to-one onto your five-part structure, so I've sorted it into the five slots.

---

## 1. Answer first

**(a) Working:** You lead with the result, not the method.

**(b) Change:** "Did drive" claims causation, which your own later evidence doesn't support. "2% lift" is also ambiguous: is it 2 percentage points or 2% relative? A VP will hear "2 points" and badly overestimate the win.

**Rewrite:**
> "Variant B came out slightly ahead, but not by enough for us to be confident the improvement is real. Its click rate was about 2% higher in relative terms (from [X%] to [Y%])."

---

## 2. Effect size in business terms

**(a) Working:** Translating into purchases and dollars is exactly right. This is what the VP cares about.

**(b) Change:**
- The first two sentences say the same thing twice ("normal send rates" / "normal send volume"). Pick one.
- The 17-per-10,000 figure is a lot of arithmetic to say out loud. Lead with the quarterly number and the dollars.
- There's a hidden jump from click rate to purchases. Say that the purchase estimate comes from the conversion data.
- Check your arithmetic. 17 per 10,000 becoming 47 per send implies about 27,600 emails per send, and $7,000 across 47 purchases implies about $149 per purchase. Make sure both match your actual send size and average order value.
- Frame $7,000 as a best guess, not a forecast.

**Rewrite:**
> "If the lift is real, that's roughly 47 extra purchases per quarterly send, or about $7,000 in additional revenue. That's our best single estimate, not a promise."

---

## 3. Confidence in plain language

**(a) Working:** You didn't hide the uncertainty, which is the right instinct.

**(b) Change:** This is the weakest part, and it hits two of your failure modes at once.

- **P-value speak.** The VP doesn't need "p = 0.47" or "at least as extreme."
- **A common misreading.** "Likely due to random chance" sounds like the p-value is the probability that chance caused the result. It isn't. A p-value answers a narrower question: *if A and B were truly identical, how often would we still see a gap this big?* Here the answer is about 47% of the time, which is nearly a coin flip. So the accurate message is "this result is indistinguishable from luck," not "this result was probably luck."
- **"Confirmed."** The confidence interval doesn't confirm the p-value. They're two views of the same evidence. Say "the range of plausible outcomes runs from a small loss to a small gain."
- **The "click rate vs. conversion rate" sentence** is muddled and belongs here, not near the recommendation. I think you mean that early winners usually shrink once rolled out, so expect less than what we measured. That's a good point, but say it plainly. Also be careful with "both point to B." When neither result is solid, agreement between them is only mildly encouraging.

**Rewrite:**
> "My confidence that this is a real improvement is low. If the two emails were actually identical, we'd still see a gap this size about half the time just by luck. The realistic range runs from a small loss to a small gain. Click rate and purchases both leaned toward B, which is mildly encouraging, but early leads like this usually shrink once rolled out, so I'd plan on the low end of that range."

---

## 4. Recommended action

**(a) Working:** You make a clear call, which many analysts skip.

**(b) Change:**
- You gave two recommendations ("move forward with B" *or* "keep a test group"). That reads as hedging. Give one recommendation with the holdout built in.
- You haven't said *why* adopting B is reasonable when the evidence is weak. The reason is a business one: switching is cheap and low-risk, and there's no sign B is worse. Say that explicitly, and confirm it's true (no extra production cost, no brand risk).
- A "small" holdout group can't answer the question. The test already couldn't detect this difference at its current size, and a smaller group will do worse. Specify the holdout size and how many sends you'll run.

**Rewrite:**
> "I recommend making B the default for the next campaign. It costs nothing extra, there's no sign it's worse, and the upside is plausible. I'd keep [X%] of the list on A for the next [N] sends so we can confirm the gain with real evidence instead of guessing."

---

## 5. Anticipated follow-up

**(a) Working:** Nothing yet. This section is missing entirely.

**(b) Change:** Add it. The VP will almost certainly ask one of these:

| Likely question | Your prepared answer |
|---|---|
| "So did B win or not?" | "It's ahead, but we can't call it a win yet. The next few sends will settle it." |
| "Is $7K even worth the effort?" | "It's modest, which is why I'm recommending a no-cost switch, not a big investment." |
| "Why not just wait and test more first?" | "We can, but switching now costs nothing, and we keep learning either way." |
| "When will we know?" | "After [N] sends, roughly [timeframe]." |

Pick the one or two you think are likeliest and put them in the talking points.

---

## Overall verdict

**Good bones, needs one more pass.** You have the right ingredients: a quantified impact, honest uncertainty, and a recommendation. Before you present:

1. Fix the opening so it doesn't contradict the confidence section.
2. Cut the p-value and "confirmed by the confidence interval" language.
3. Collapse your two recommendations into one, with the reason it's low-risk.
4. Add the missing follow-up section.
5. Double-check the arithmetic and whether "2%" is relative or absolute.

Done well, the whole thing should be speakable in about a minute. If you send me the underlying numbers (click rates, send size, order value), I can verify the figures and tighten the full script.


## AI Use Disclosure

Claude was used to critique and review the talking points for clarity and completeness. Claude suggested keeping the two tests seperate as opposed to using conversion rate and click through rate in the same memo which i agreed on. It also suggested fixing a few contradictions which I addressed and adding a missing follow-up section which I also addressed. 