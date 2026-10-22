# Lesson 2.8 Practice Notes

## Audit My Work

Total Revenue comes from sales_2024 and is a SUM function. It is fed by column G, gross_revenue. When compared the numbers are the same

Total Orders comes from sales_2024 and is a COUNT function based on column A, order_id. Manually counting and rerunning the function returns the same result.

Average Order Value is a calculated AVERAGE function from the answers of the previous 2 KPI numbers. It sources back to sales_2024 columns A and G and calculates the same when the data is rerun.

The pivot table on the dashboard for sum of gross_revenue comes from the data in the sales_2024 sheet. The source data hasn't expanded or changed since the creation of the table. 

The sum of spending pivot table will need to be reworked and told to reference the cleaned column for spending types as it has formatting issues that were cleaned up in the edited column.

The refund pivot table also needs to be addressed as it has row labels that needed to be cleaned and were later in the module.

The revenue by category chart is connected to a current pivot

The customer segment trends chart was built as instructed but I think that it would better show what we were trying to show flipping the x/y axis to make the lines the categories and not months.

I was unable to find any mismatches in the A/B analysis, but I also struggled to to the analysis so I redid it multiple times in the process of calculation. 

## Second Pair of Eyes

I don't have someone else to look at the work so I went ahead and took a day off and came back and looked at it with fresh eyes. I know it's not as effective but it's the option that I have at the time being.

The questions I asked were why is this chart showing lines by month instead of category on the customer segment trends and where did the average order value actually come from. The chart I would change the formatting on to swap the x and y axis to make the lines represent the categories and not the months. The average order value came from dividing the total revenue number by the number of orders(SUM gross_revenue and COUNT order_id).

### Data Quality Memo

Beatrix,

I've completed an audit of the data that we recieved for q4 of 2024. In doing so I checked for data integrity in all of the imported fields and ran into a couple of things that are creating challenges. I have a couple of suggestions for the data team to make our numbers a little easier to work with and read going forward. The SKU numbers that imported for inventory need to be preserved as text when the CSV is imported to prevent issues with SKU's that look like dates. We should make sure to also import anything with a date field in a manner that preserves the contents as a date and validate that the date formats are all the same (10/15/2026 vs 15/10/2026 vs Oct 15 2026 will cause mismatches and more time in the analasys stage). This issue caught us on the customer_segments import this time but it could make a mess of any of our imports. Having a consistent format would save you headaches later. Another place where a little work on the front end could improve the response time on analysis would be inconsistencies in things like campaign types from the marketing_spend tab and return reasons on the returns tab. Both had a lot of things that showed up as different types/responses that were actually the same like " Email" and "Email" in the marketing_spend and "late delivery." vs "Late delivery" vs "Late Delivery" in returns. This could be handled in the import if the data team was to use PowerQuery to import and standardize the formatting. I've done those edits on this round of data and cleaned it up but if we import it clean going forward it could definitely make analysis cleaner. It might take the data team a couple more minutes on the import but it would prevent some issues in the future if we address it on the front end instead of cleaning up afterwards. I'd be happy to work with the data team directly if you would like. Please advise.

## AI Critique of Memo

### Prompt Used

Role: You're a senior analyst coaching a junior analyst on how to present findings of a data audit to a non-technical stakeholder.

Task: Critique my draft for clarity, accuracy, and business framing

Context: I'm presenting my results of a data audit to a non-technical VP of marketing. The audience cares about practical input and how to move forward and not statistical method.

Output format: for each point made, note (a) what's working and (b) what i should change with a specific rewrite if a change is needed. Then give an overall verdict.

My Draft: 

Beatrix,

I've completed an audit of the data that we recieved for q4 of 2024. In doing so I checked for data integrity in all of the imported fields and ran into a couple of things that are creating challenges. I have a couple of suggestions for the data team to make our numbers a little easier to work with and read going forward. The SKU numbers that imported for inventory need to be preserved as text when the CSV is imported to prevent issues with SKU's that look like dates. We should make sure to also import anything with a date field in a manner that preserves the contents as a date and validate that the date formats are all the same (10/15/2026 vs 15/10/2026 vs Oct 15 2026 will cause mismatches and more time in the analasys stage). This issue caught us on the customer_segments import this time but it could make a mess of any of our imports. Having a consistent format would save you headaches later. Another place where a little work on the front end could improve the response time on analysis would be inconsistencies in things like campaign types from the marketing_spend tab and return reasons on the returns tab. Both had a lot of things that showed up as different types/responses that were actually the same like " Email" and "Email" in the marketing_spend and "late delivery." vs "Late delivery" vs "Late Delivery" in returns. This could be handled in the import if the data team was to use PowerQuery to import and standardize the formatting. I've done those edits on this round of data and cleaned it up but if we import it clean going forward it could definitely make analysis cleaner. It might take the data team a couple more minutes on the import but it would prevent some issues in the future if we address it on the front end instead of cleaning up afterwards. I'd be happy to work with the data team directly if you would like. Please advise.

### Response

# Critique of your data audit email

I'll go through the draft in order, then give a verdict and a full rewrite.

## 1. Opening (audit completed, "a couple of things creating challenges")

**(a) Working:** You state what you did and that you found issues. The tone is professional and collaborative.

**(b) Change:** Beatrix has to read about 300 words before she learns what she's being asked to do. "A couple of things creating challenges" and "a little easier to work with" are also vague and understate the problem. The usual rule for executives is bottom line up front: what you found, why it matters, what you need from her.

Also check the date. The draft says "Q4 of 2024," but today is October 2026 and your examples use 2026 dates. If you mean a different quarter, fix it, because a wrong period in the first line makes a VP doubt everything after it.

**Rewrite:**
> Beatrix, I audited the Q4 data we received and found three formatting issues that could cause errors in our reporting. I've already corrected them for this round, so the numbers I'll give you are reliable. I'd like your OK to work with the data team on preventing them going forward.

## 2. The SKU issue

**(a) Working:** You identified a real, specific problem and the right fix (treat SKUs as text).

**(b) Change:** "Preserved as text when the CSV is imported" is technical language Beatrix doesn't need. The consequence is what she cares about, and you never state it. Spreadsheet tools can turn a code like "3-12" into a date, which means inventory could be matched to the wrong product. Also, "SKU's" shouldn't have an apostrophe.

**Rewrite:**
> **Product codes (SKUs) being misread as dates.** Some inventory codes look like dates, so the software converts them (e.g., "3-12" becomes "March 12"). That can attach inventory numbers to the wrong product.

## 3. The date format issue

**(a) Working:** You correctly identified inconsistent date formats as a recurring risk, and you showed examples, which helps.

**(b) Change:** Your example undersells the danger. "10/15/2026 vs 15/10/2026" looks like a simple mismatch, but the real risk is dates that can be read two ways. 03/04/2026 could be March 4 or April 3, and the software guesses silently. That means wrong numbers with no error message, which is a much stronger point than "more time in the analysis stage."

"This caught us on customer_segments but could make a mess of any import" is vague. What happened? Say how it affected the work. And "would save you headaches" frames the benefit as personal convenience instead of business accuracy.

**Rewrite:**
> **Inconsistent date formats.** Dates arrive in mixed styles, and some can be read two ways (03/04/2026 is March 4 in the US and April 3 elsewhere). The software guesses without warning, so revenue can land in the wrong month. This affected the customer_segments file this time, and I corrected it.

## 4. Inconsistent labels (campaign types and return reasons)

**(a) Working:** Your examples are concrete and well chosen. This is the clearest part of the draft because the reader can picture the problem.

**(b) Change:** A non-technical reader may not see the difference between " Email" and "Email," because the difference is an invisible extra space. Explain that. Then connect it to a business consequence: one campaign gets counted as two, so the totals for each look smaller than they are, which could affect decisions about where to spend. Also, "late delivery." with a period inside the quotes is confusing, so write the variants cleanly.

**Rewrite:**
> **The same label typed different ways.** "Email" appeared as "Email" and " Email" (with a hidden extra space), so email spend was split into two lines. Return reasons had the same problem ("Late delivery," "late delivery," "Late Delivery" counted separately). Left uncorrected, the top return reasons and campaign totals would be understated.

## 5. The proposed fix and effort claim ("Power Query," "a couple more minutes")

**(a) Working:** Fixing problems at the source rather than cleaning afterwards is the right principle, and you explain the tradeoff reasonably well.

**(b) Change:** "PowerQuery" is a tool name, so it belongs in a note to the data team, not in an email to a VP. The bigger issue is accuracy. "A couple more minutes" is a claim about the data team's workload that you can't back up yet, and "definitely" is overconfident. If it turns out to take days to set up, you've damaged your credibility. Frame the cost as something to confirm.

**Rewrite:**
> **My recommendation:** have the data team standardize these fields as the data comes in, instead of fixing them afterward. I expect the extra effort per import to be small, and I'll confirm with them before we commit.

## 6. The close ("I'd be happy to work with the data team... Please advise.")

**(a) Working:** Offering to collaborate is the right instinct.

**(b) Change:** "Please advise" hands the decision back without saying what the decision is. Make the ask specific and easy to say yes to, with a timeframe.

**Rewrite:**
> **What I need from you:** your OK to meet with the data team this week to set this up. I'll bring a one-page checklist so it takes 30 minutes or less.

## 7. Writing mechanics and structure

**(a) Working:** The tone is polite and not defensive.

**(b) Change:** Fix "recieved," "analasys," and "SKU's." The bigger issue is that it's one long block of text. A busy VP will skim it, so use a short subject line and three short labeled sections. Keep file names and tool names out of the main body, or put them in a brief "details for the data team" line at the end.

## Overall verdict

The content is accurate and the instincts are good: you found real problems, picked sensible fixes, and cleaned the data yourself. Right now, though, it reads as a technical to-do list for the data team, not as a message to a VP. The biggest improvement is to shift from how things are being fixed to what could have gone wrong in the numbers and what you need from her. Quantifying the impact where you can (even a rough "about 5% of return records") would make it much stronger. Also drop the "a little" and "a couple" softeners, which understate a legitimate risk.

## Suggested full rewrite

> **Subject: Q4 data audit: 3 issues fixed, one decision needed**
>
> Beatrix,
>
> I audited the Q4 data we received and found three formatting problems that could have caused errors in our reports. I've corrected all three, so the numbers I'm giving you are reliable. To keep them from recurring, I'd like your OK to work with the data team on a fix at the source.
>
> **What I found**
> 1. **Product codes read as dates.** Some inventory codes look like dates, so the software converted them, which can attach inventory to the wrong product.
> 2. **Mixed date formats.** Some dates can be read two ways (03/04/2026), and the software guesses silently, so revenue could land in the wrong month. This affected the customer_segments file.
> 3. **Same label, typed differently.** "Email" and " Email" (extra space) were counted as separate campaigns, and "Late delivery" appeared in three spellings in returns. Totals for each were understated.
>
> **Recommendation**
> Have the data team standardize these fields as data comes in, instead of fixing them afterward. I expect the added effort per import to be small and will confirm with them first.
>
> **What I need from you**
> Your OK to meet with the data team this week. I'll bring a one-page checklist, and it should take about 30 minutes.
>
> Thanks,
> [Name]

I don't know whether the issues affected the final numbers, so confirm that before sending. If they did, say by how much. If they didn't because you caught everything, say that too, since it's the reassurance she most wants to hear.


### Rewrite of Draft with edits

Beatrix,

I have audited the Q4 data we recieved and found three formatting problems that could have caused errors/issues in our reports. I went back and corrected all three so we can press with the numbers I'm giving you as reliable. To prevent this from happening in the future, I'd be happy to work with the data team to make a fix at the time of import if that's OK.

What I found:

Product Sku's read as dates: Some of the inventory codes look like dates so when they were imported Excel converted them as such. 

Same label typed differently: Because of text input with extra spaces and characters in some of the text fields, certain categories would count seperately and cause the totals to be understated without deep cleaning the data. 

Mixed date formats: Dates appeared in multiple formats including text and number formats throughout the data. When imported the software takes a guess at what the cell means and could guess wrong. If it does, revenue might appear very different than reality. Consistent formatting and import would prevent this issue entirely.


Recommendation: 

I would suggest that the data team standardize the data on import as opposed to cleaning up the mismatches later. I expect the time increase on the import to be minor but in the long run it could save a lot of time on the analysis side. 

What I need from you:

With your permission, I would like to meet with the data team to go ahead and implement the formatting changes that we need on the imports. I will bring a short checklist of the changes and I estimate the meeting would take about 30-45 minutes to get those things into place. 

## Deliverables

I audited all fields across all of the data tables for missing rows/columns, date mismatches, formatting, and auto-conversion.

I did not find errors in my work, but I also reworked the numbers multiple times as I had struggles in the process, so I believe i caught any errors I had before I submitted the initial analysis. 

I was unable to have a peer review the workbook so I don't have peer responses, but my responses to the review are above in this document.

See above for the AI critique and my drafts of the memo.

## AI Use Disclosure

I used Claude to critique my memo for the audit process. It suggested that I was too wordy in my memo, which I agreed on and reworded all parts. It also suggested some formatting changes to make it easier to catch the pieces of the memo, which I took into account as well. It led me to completely rewrite my draft as I was not happy with it when I saw the suggestions and wanted to start fresh.