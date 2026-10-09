# LinenLane Workbook First-Look Notes
Date: 2026-10-06
Reviewer: A. Chris Yi

## Tab: Sales_2024
- Row count: 28001
- Column headers (with brief description)
    order_id : an order number, individual per order
    order_date : the date of the order
    customer_id : customer identifier for the order, per customer
    sku : sku number for the item sold in the order
    units : number of units sold in the order
    unit_price: price per unit sold
    gross_revenue : revenue from the units sold
- Date range: 2024-01-01 to 2024-12-31
- Suspicious or unclear: nothing looks suspicious or unclear, this tab looks clear cut. 
- Questions for follow-up: need to keep an eye on duplicate orders and duplicate entries for single customers on different dates to keep real and noise seperate

## Tab: Inventory
- Row count: 281
- Column headers (with brief description):
    sku : product identifier sku number, specific to each item
    product_name : description of the item
    category : what category does the item fall into 
    current_stock : count of inventory on hand for the specific sku
    unit_cost : price per unit
    supplier : where the item came from
- Date range: no dates present on this sheet
- Suspicious or unclear: what exactly is the unit cost field?
- Questions for follow-up: is unit cost the purchase cost of the item for the business or the sale price of the item?

## Tab: marketing_spend
- Row count: 61
- Column headers (with brief description):
    month : month of the marketing event
    channel : where the marketing event takes place
    spend : cost of the marketing event
    campaigns_count : count of how many campaigns
- Date range: january to december, no year present on this sheet
- Suspicious or unclear: dates are month only
- Questions for follow-up: what is the count of campaigns counting? 

## Tab: customer_segments
- Row count: 7491
- Column headers (with brief description):
    customer_id : customer identifier, per customer
    segment : what kind of customer is this
    lifetime_value : total lifetime spend
    first_order_date : date of first order
    email_subscribed : does the customer have an email subscribed for marketing
- Date range: no clear date range. 
- Suspicious or unclear: first order date field is supposed to be a date but it showing a numerical value
- Questions for follow-up: are the dates a conversion issue or a missing value or an error?

## Tab: retrns
- Row count: 1501
- Column headers (with brief description):
    return_id : identifier for specific return, one per return
    order_id : identifier for order number, one per order
    sku : item identifier for returned item
    return_reason : reason for the return
    refund_amount : amount refunded to the customer
    return_date : date of the return event
    units_returned : how many units were returned
- Date range: 2024-01-01 to 2024-12-31
- Suspicious or unclear: missing values in refund amount, one code on the sku doesn't match formatting for the others 
- Questions for follow-up: is missing data missing or no data exists? are all skus supposed to be the same format?

