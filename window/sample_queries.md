# Sample Queries for Window Functions
Sample queries for using Window Functions in relational databases using SQL.

## Obtain the Sample Data
You should have permissions to use these queries as-is under my GCP project. However, you can copy the data to your own project by following the [instructions provided here](../gcp/bq_dataset_copy.md).

## Basic Aggregation Window Function
```
-- Find the average sales price for every record in the table
SELECT 
    *, 
    AVG(sale_price) OVER () AS avg_sale
FROM 
    `elliott-purdue-development.class_demos.home_sales`;
```

Note that the `OVER ()` clause of the query did not include any information. Therefore the window was not defined. You must add instructions to the `OVER ()` clause to ensure you are clearly defining the window you're looking for.

```
-- Find the average sales price for every record in the table, grouped by state
SELECT 
    *, 
    AVG(sale_price) OVER (PARTITION BY state) AS avg_sale
FROM 
    `elliott-purdue-development.class_demos.home_sales`;
```

## MAX() Aggregation Window Function
```
-- Find the maximum sales price within a rolling window of the last 3 sales for each state. 
SELECT 
    address,
    city,
    state,
    sale_date,
    sale_price,
    MAX(sale_price) OVER (PARTITION BY state ORDER BY sale_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS rolling_max_sale_price
FROM 
    `elliott-purdue-development.class_demos.home_sales`;
```

## Ranking Window Function
```
-- Suppose you have a table of real estate sales and you want to identify the top 3 sales in each state based on the sales price.
WITH ranked_sales AS (
    SELECT 
        address,
        city,
        state,
        sale_date,
        sale_price,
        ROW_NUMBER() OVER (PARTITION BY state ORDER BY sale_price DESC) AS state_rank
    FROM 
    `elliott-purdue-development.class_demos.home_sales`
)
SELECT 
    state_rank,
    address,
    city,
    state,
    sale_date,
    sale_price
FROM 
    ranked_sales
WHERE 
    state_rank <= 3;
```

## Value Window Function
```
-- Suppose you have a table of daily stock prices and you want to calculate the day-to-day change in stock price.

SELECT 
    close_date,
    stock_price,
    LAG(stock_price, 1) OVER (ORDER BY close_date) AS previous_price,
    stock_price - LAG(stock_price, 1) OVER (ORDER BY close_date) AS price_change
FROM 
    `elliott-purdue-development.class_demos.stock_prices`;
```

```{warning}
Notice that the results of the previous query are sorted only by `close_date`. Is the data in the output correct?

What's missing?
```

```
-- UPDATED: Suppose you have a table of daily stock prices and you want to calculate the day-to-day change in stock price.
SELECT 
ticker,
close_date,
stock_price,
    LAG(stock_price, 1) OVER (PARTITION BY ticker ORDER BY close_date) AS previous_price,
    stock_price - LAG(stock_price, 1) OVER (PARTITION BY ticker ORDER BY close_date) AS price_change
FROM 
    `elliott-purdue-development.class_demos.stock_prices`
ORDER BY 
ticker, close_date
```

Because you added the `PARTITION BY ticker` statement, the results are now correctly grouped by `ticker` and ordered by `close_date`. Therefore, the results are more meaningful.