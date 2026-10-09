## Scenario 1: Your CFO asks: "If we increase our enterprise tier price by 8% and lose 2% of enterprise customers as a result, what's the net revenue impact this year?" She needs an answer in 30 minutes for board prep.
**Tool recommended:** i would use either excel or python
**Justification:** If the dataset was small enough to use excel effectively, it would produce the answer reasonbly fast, but python would most likely be the best fit because it could handle something of an unknown dataset size and calculate those numbers rapidly. If the dataset was bigger it would definitely be a python solution. 

## Scenario 2: Your Customer Success team wants a daily dashboard showing each region's churn rate against target. The dashboard will be checked every morning by 30 people across the org.
**Tool recommended:** a BI tool
**Justification:** because it's a dashboard and multiple people will interact with it over time, a BI tool is your best bet

## Scenario 3: You've been asked to identify which of your 14,000 customer support tickets from Q3 mention "shipping delay" and categorize each by sentiment.
**Tool recommended:** Python
**Justification:** While excel could handle the dataset size, python handles text data the fastest. If the audience was not technical, I would switch to a BI tool.

## Scenario 4: Your colleague hands you a CSV of 1,200 rows showing transactions from a partner integration over the last week. They want a quick view of which products were most popular and a back-of-envelope revenue estimate.
**Tool recommended:** Excel
**Justification:** With a small dataset and one time work, excel is the fastest and most simple to understand tool for the job. If the dataset was larger this would be a python situation

## Scenario 5: The data engineering team is restructuring the warehouse. They've asked you to build a reusable layer of transformations that other analysts in the company will query. The transformations need to run nightly and be tested.
**Tool recommended:** a BI tool
**Justification:** Because multiple people need to interact with this tool, it is best written in a BI tool

## Scenario 6: Your VP Marketing wants to know whether the average order value differs meaningfully between users who arrived from email vs. paid social over the last 90 days. She wants the result with a confidence interval.
**Tool recommended:** python
**Justification:** these calculations would be easy to calculate no matter the dataset size in python. If the audience was non-technical I would consider a BI tool to make the output more readable 

## Scenario 7: A regional manager asks you to produce a one-page printable summary of last quarter's performance for 15 store locations: top products, total revenue, target attainment. The format will be reused next quarter.
**Tool recommended:** python, and a BI tool
**Justification:** Statistics are needed and its a printable summary but visual quality is needed and it will be reused so multiple people may be running it or interacting with it in the future

## Scenario 8: The product team has access to a new event-stream warehouse with about 600 million rows of click-level data per month. They need a recurring funnel analysis that updates each Monday morning.
**Tool recommended:** dbt
**Justification:** With this much data excel would bog down. Since it's a data warehouse, most likely dbt would be the best place to go. 