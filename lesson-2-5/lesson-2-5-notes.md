# Lesson 2.5 Notes

## Intro to PowerQuery

Table naming is standardized
Used:
trim 
capitalize
replace values functions
renamed columns
filtered numbers
filtered blanks
removed duplicates
added column
reordered columns

## AI Demo and Verification

### Prompt used

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

### Claude Response

if [gross_revenue] = 0 then "Zero Revenue" else if [refund_amount] / [gross_revenue] > 0.5 then "High" else "Standard"

## PowerQuery thoughts

Everything seems a little easier in powerquery, or at least more intuitive. Either way it takes a lot of attention to detail, but powerquery just makes more sense to my brain. 

## AI Use Disclosure

"Used Claude on 2026-10-12 to write an M expression for a custom column flagging high refund ratios. Verified the if/else logic and tested on three rows. Worked as expected."

## Lesson 2.5 Deliverable

### Applied Steps
1.  Trimmed text with transform>text column>format>trim to remove extra spaces or invisible characters
2.  Capitalized each word with transform>text column?format>capitalize each word for consistency 
3.  replaced value for "-" with " " using transform>replace value
4.  filtered rows for values of 0 or lower using the dropdown filter on the column. 

### Comparison

The manual cleaning took about 3x longer than the powerquery practice took. It was literally a third of the time and can be reused when data is updated and take less than a minute to do. 

### Harder in Powerquery

I didn't find anything harder in powerquery. The only challenge is learning the icons and options which will come with time. It's much faster and more intuitive than manual cleaning

### Exception from manual

The query handled the removal of 0 value rows more easily. It could have been done manually but it wasn't covered in the manual exercise. 