# Lesson 2.8 Audit Findings

## Finding 1
**Tab/Cell**: _README
**Category**: possible date and auto-corrected errors noted
**Description**: Some Sku's dont match the pattern and may have imported unclearly. Return reason was input by hand and not consistent. Date columns don't always have the same format.
**Impact on analysis**: could throw errors or completely invalidate results
**Recommended fix**: scrub all tabs for all 7 errors. They have been seen, they need to be addressed.

## Finding 2
**Tab/Cell**: sales_2024
**Category**: auto-conversion
**Description**: SKU codes that have a naming pattern similar to dates
**Impact on analysis**: not all sku numbers are going to populate as text, would cause mismatches and errors in calculation, broken index references. Approx 305 rows effected 
**Recommended fix**: explicit text formatting and powerquery

## Finding 3
**Tab/Cell**: customer_segments 
**Category**: Date
**Description**: first order date is showing as a number not a date value
**Impact on analysis**: hasn't impacted it yet, but could cause a mismatch in future analysis
**Recommended fix**: powerquery set type on date column to date


## Finding 4
**Tab/Cell**: inventory
**Category**:auto conversion
**Description**: some SKU numbers imported as dates as they are not in the same format as the other sku numbers 
**Impact on analysis**: caused blanks in the sales_2024 sheet when referenced, can cause errors moving forward
**Recommended fix**: import SKU column as text not general or use powerquery

## Finding 5
**Tab/Cell**: unknown
**Category**: hidden content
**Description**: unable to find the hidden content in the sheet
**Impact on analysis**: unsure. Not happy about this one.
**Recommended fix**: scrolled every sheet, ran a macro to find hidden rows and columns and got no results. 


## Cross Tab Consistency

There are many values in the customer_id field that returned unknown in the customer_segment field. SKUs with numbers that look like dates also throw the N/A error


## Recompute from scratch

The total revenue number matched exactly. Starting to wonder if I managed to unhide the hidden content from the beginning

## AI Verification

### Prompt Used

Role: You're a senior analyst auditing an Excel workbook.

Task: Identify potential data quality issues in this sample of
columns from a multi-tab workbook.

Context: This is a workbook from a home-goods e-commerce client.
Below are representative rows from five tabs. The data has known
issues (auto-conversions, floating-point drift, date inconsistencies),
but it also has plenty of clean data. I'm preparing for a stakeholder
handoff and want to catch any issues before reporting findings.

Constraints: Focus on issues a working analyst would worry about:
type mismatches, suspicious values, format inconsistencies. Don't
flag stylistic preferences.

Output format: A numbered list of findings. For each, name the
column or cell, describe the concern, and rate the severity (Low /
Medium / High).

Data sample:
ORD-34357    8/9/2024    CUST-2066    LL-1203    2    47.80    95.60    Terry Wreath in Sage    Terry Wreath in Sage    Decor    Small    Medium    Medium    Standard    New    Medium                
ORD-17931    9/5/2024    CUST-2735    LL-1265    1    72.96    72.96    Jute Under-Bed Box in Sage    Jute Under-Bed Box in Sage    Storage    Small    Small    Small    Standard    New    Small                
ORD-30542    9/4/2024    CUST-9296    LL-1087    1    303.66    303.66    Herringbone Shower Curtain in Rust    Herringbone Shower Curtain in Rust    Bath    Large    Large    Large    Standard    Unknown    Large                
ORD-12118    12/13/2024    CUST-7367    LL-1088    2    38.26    76.52    Chambray Hand Towel in Moss    Chambray Hand Towel in Moss    Bath    Small    Medium    Medium    Standard    Lapsed    Medium                
ORD-20881    4/8/2024    CUST-5150    LL-1129    4    64.44    257.76    Flannel Bath Mat in Sand    Flannel Bath Mat in Sand    Bath    Large    Large    Large    Standard    New    Large                
ORD-13200    9/1/2024    CUST-6453    LL-1044    1    117.72    117.72    Waffle Sheet Set in Moss    Waffle Sheet Set in Moss    Bedding    Large    Medium    Medium    Standard    Unknown    Medium                
ORD-30370    2/2/2024    CUST-6037    LL-1111    4    42.54    170.16    Sateen Bath Towel in Bone    Sateen Bath Towel in Bone    Bath    Large    Medium    Medium    Standard    Unknown    Medium                
ORD-35288    2/15/2024    CUST-6613    LL-1153    1    54.06    54.06    Terry Oven Mitt in Moss    Terry Oven Mitt in Moss    Kitchen    Small    Small    Small    Standard    Regular    Small                
ORD-12365    8/12/2024    CUST-8546    LL-1042    3    71.26    213.78    Flannel Sheet Set in Sage    Flannel Sheet Set in Sage    Bedding    Large    Large    Large    Standard    New    Large                
ORD-26850    7/1/2024    CUST-3706    LL-1254    3    19.14    57.42    Percale Closet Organizer in Slate    Percale Closet Organizer in Slate    Storage    Small    Small    Small    Standard    Lapsed    Small                

LL-1249    Herringbone String Lights in Oat    Lighting    844    29.26    Bellhouse Weavers    Lowell    MA
LL-1120    Sateen Robe in Rust    Bath    680    24.47    Cedarline Textiles    Greensboro    NC
LL-1145    Jute Oven Mitt in Moss    Kitchen    278    24.94    Windward Linen    Providence    RI
LL-1086    Linen Hand Towel in Bone    Bath    218    22.97    Fieldstone Imports    Elkhart    IN
LL-1045    Terry Duvet Cover in Slate    Bedding    106    32.13    Windward Linen    Providence    RI
LL-1169    Percale Table Runner in Slate    Kitchen    523    30.07    Bellhouse Weavers    Lowell    MA
LL-1065    Terry Mattress Pad in Clay    Bedding    719    30.12    Windward Linen    Providence    RI
LL-1039    Herringbone Quilt in Oat    Bedding    234    41.93    Bellhouse Weavers    Lowell    MA
LL-1213    Jute Wall Hanging in Bone    Decor    389    31.09    Northbank Home    Portland    OR
LL-1134    Jute Table Runner in Sage    Kitchen    350    28.20    Trellis Goods Co    Kannapolis    NC

January    paid social    23331.02    2    Paid Social
January    Search     25716.88    4    Search
January    display    10276.24    1    Display
January    Affiliates    6682.26    1    Affiliates
February     Email    7364.04    1    Email
February    Paid social    18272.79    4    Paid Social
February    Search     23841.22    1    Search
February    display    10324.59    4    Display
February    Affiliates    4833.73    5    Affiliates
March    Email    7672.38    5    Email

CUST-5510    Regular    890.85    45571    TRUE
CUST-1553    New    229.96    44548    TRUE
CUST-6580    New    60.66    44758    FALSE
CUST-1175    New    109.94    45490    FALSE
CUST-4172    Lapsed    476.05    44440    FALSE
CUST-2265    New    111.85    45213    FALSE
CUST-7101    Lapsed    301.29    45527    FALSE
CUST-8875    Regular    500.38    44786    TRUE
CUST-4011    New    311.15    44908    TRUE
CUST-3088    New    162.18    45035    TRUE

### Response

Note: You didn’t include headers, so I’ve inferred what each column means. Please confirm my guesses before these go in the handoff.

Findings

Orders tab, the three size-like columns (right after Category): High. They disagree in 4 of 10 rows. ORD-34357 and ORD-12118 show Small / Medium / Medium. ORD-13200 and ORD-30370 show Large / Medium / Medium. A sheet set labeled “Medium” in two columns and “Large” in another can’t all be right. The last “size” column also matches the third in every row, so it’s redundant. Anyone reporting by size will get different answers depending on which column they pick, so find the source of truth and drop the others.
Orders tab, Product Name appears twice (columns 8 and 9): Low. The two are identical in all 10 rows, which usually means a lookup or join was pasted next to the original. It’s harmless until someone edits one copy and not the other.
Orders tab, customer segment column: Medium. “Unknown” appears in 3 of 10 rows (30%), and the Customers tab only has New, Regular and Lapsed. That suggests a failed lookup or a placeholder fill. Check whether those customer IDs exist on the Customers tab at all. Also confirm whether the segment is as of the order date or as of today, because the two give different answers.
Orders tab, Unit Price for LL-1087 (Herringbone Shower Curtain, $303.66): Medium. It’s about 3x the next-highest price in the sample (the $117.72 sheet set). It may be a legitimate premium item, but it’s the kind of value that comes from a decimal slip or a bulk price. Verify it against the product price list. The Terry Oven Mitt at $54.06 is also worth a glance, since the Jute Oven Mitt on the product tab costs $24.94.
Customers tab, date column (values like 45571, 44548): Medium. These are Excel serial numbers that lost their date formatting. Excel counts days from a fixed start date, so 45571 is October 6, 2024. They’re correct underneath but unreadable on a report. Reapply a date format, and confirm they’re numbers rather than text.
Customers tab, segment vs. date: Medium. If that date is a signup or first-order date, six “New” customers have dates from 2021 to 2023, which contradicts the label. If it’s a last-order date, it conflicts with how “Lapsed” and “Regular” are defined (CUST-7101 is Lapsed with a 2024-08-23 date, but CUST-5510 is Regular with 2024-10-06). Either way, you need a definition of the date and the segment rules.
Marketing tab, raw channel column (column 2): Medium. It has case variants (“paid social” vs “Paid social”), trailing whitespace (“Search “), a leading space (” Email”), and lowercase “display”. A pivot on this column would split one channel into several buckets. Column 5 cleans them up correctly in this sample, but make sure that column is a formula or mapping that covers all rows. Hide or remove the raw column so nobody pivots on it by accident.
Marketing tab, January Email row: Medium (High if confirmed). February has five channels with Email first, but January has only four and no Email row. Either Email spend was zero and nobody entered it, or a row was dropped. If it’s a dropped row, spend totals for the quarter are understated.
Marketing tab, Month column: Medium. It holds month names with no year, as text. You can’t join it to the 2024 order dates, and it sorts alphabetically. If the data ever spans more than one year, the periods will merge silently. Use a real date or add a year column.
Marketing tab, unlabeled integer column (values 1 to 5): Medium. I can’t tell what it measures. It swings widely for the same channel (Search goes from 4 to 1, Affiliates from 1 to 5). If it’s a ratio such as ROAS, whole numbers suggest rounding. If it’s a campaign count, that’s fine. Either way, a stakeholder will ask what it is.
Dates across tabs, and order ID vs. date: Low. Orders use M/D/YYYY, Customers use serial numbers, and Marketing uses month names. The M/D/YYYY ordering is confirmed by 12/13/2024 and 2/15/2024, but 8 of 10 order dates are ambiguous on their own (e.g., 9/5, 4/8). Order IDs also don’t follow date order (ORD-35288 is 2/15 but ORD-12118 is 12/13). That’s fine if the IDs are random, but if they’re sequential, the dates may have been altered.
Cross-tab keys: Low (can’t verify from this sample). None of the 10 order customer IDs or SKUs appear in the Customers or Products samples. That’s expected with samples, but a full lookup test should be part of the audit.
Orders tab, four trailing empty columns: Low. These are leftover columns from deleted or never-populated data. Remove them so they don’t affect imports or the used range.
Money columns, floating-point drift: Low (can’t rule out from this view). Every Qty × Unit Price equals Line Total at 2 decimals. But Excel displays rounded values, so drift like 95.60000000000001 would be hidden. Test with =ROUND(F2*E2,2)=G2 or =F2*E2=G2, or compare against a rounded copy.

Checked and clean in this sample

All 10 line totals reconcile exactly.
Order, customer and SKU IDs show no signs of auto-conversion (no scientific notation or stripped prefixes).
Supplier, city and state are consistent across all 10 product rows (e.g., Windward Linen is always Providence, RI).
Customer IDs are unique, and the TRUE/FALSE values look like real booleans, though you should confirm they aren’t text.

If you can share the headers, I can tighten findings 1, 6 and 10.

### Verification

1.  those columns were calculated to show different ways to get the result with different formulas. They should be hidden to prevent issues in future analysis. 

2.  duplicate column in sales_2024 for product name. Keep one or the other?

## Data Quality Notes

Looking at the data in terms of quality, we have a lot of formatting issues and some blank fields that we need to either remove from the data or fill in with the correct information. It might help to go ahead and re-import the inveotory, customer_segments, and sales_2024 datasets with PowerQuery to make sure that we aren't having formatting issues and checking for blanks and assessing each one for if we have the data and it just didn't transfer or if it is missing entirely. 