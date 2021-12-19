# SQL practice queries on the Parch & Posey Dataset

### 1. Write a query to return the 10 earliest orders in the orders table. Include the id, occurred_at, and total_amt_usd

``` sql
SELECT id,
       occurred_at,
       total_amt_usd
FROM orders
ORDER BY occurred_at
LIMIT 10;
```

<hr>

### 2. Write a query to return the top 5 orders in terms of the largest total_amt_usd. Include the id, account_id, and total_amt_usd.

``` sql
SELECT id,
       account_id,
       total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5;
```

<hr>

### 3. Write a query to return the lowest 20 orders in terms of the smallest total_amt_usd. Include the id, account_id, and total_amt_usd.

``` sql
SELECT id,
       account_id,
       total_amt_usd
FROM orders
ORDER BY total_amt_usd
LIMIT 20;
```

<hr>

### 4. Write a query that displays the order ID, account ID, and total dollar amount for all the orders, sorted first by the account ID (in ascending order), and then by the total dollar amount (in descending order).

``` sql
SELECT id,
       account_id,
       total_amt_usd
FROM orders
ORDER BY account_id,
         total_amt_usd DESC
```

<hr>

### 5. Now write a query that again displays order ID, account ID, and total dollar amount for each order, but this time sorted first by total dollar amount (in descending order), and then by account ID (in ascending order)

``` sql
SELECT id,
       account_id,
       total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC,
         account_id
```

<hr>

### 6. Write a query that pulls the first 5 rows and all columns from the orders table that have a dollar amount of gloss_amt_usd greater than or equal to 1000.

``` sql
SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
```

<hr>

### 7. Write a query that pulls the first 10 rows and all columns from the orders table that have a total_amt_usd less than 500.

``` sql
SELECT *
FROM orders
WHERE total_amt_usd < 500
LIMIT 10;
```

<hr>

### 8. Write a query that filters the accounts table to include the company name, website, and the primary point of contact (primary_poc) just for the Exxon Mobil company in the accounts table.

``` sql
SELECT name,
       website,
       primary_poc
FROM accounts
WHERE name = 'Exxon Mobil'
```

<hr>

### 9. Create a column that divides the standard_amt_usd by the standard_qty to find the unit price for standard paper for each order. Limit the results to the first 10 orders, and include the id and account_id fields

``` sql
SELECT id,
       account_id,
       (standard_amt_usd / standard_qty) AS unit_price
FROM orders
LIMIT 10;
```

<hr>

### 10. Write a query that finds the percentage of revenue that comes from poster paper for each order. You will need to use only the columns that end with _usd. (Try to do this without using the total column.) -- Display the id and account_id fields also

``` sql
SELECT id,
       account_id,
       poster_amt_usd / (standard_amt_usd + gloss_amt_usd + poster_amt_usd) AS revenue_prcnt
FROM orders
LIMIT 10;
```

<hr>

### 11. Write a query to find all the companies whose names start with 'C'

``` sql
SELECT name
FROM accounts
WHERE name LIKE 'C%'
```

<hr>

### 12. Write a query to find all companies whose names contain the string 'one' somewhere in the name

``` sql
SELECT name
FROM accounts
WHERE name LIKE '%one%';
```

<hr>

### 13. Write a query that finds all companies whose names end with 's'

``` sql
SELECT name
FROM accounts
WHERE name LIKE '%s';
```

<hr>

### 14. Use the accounts table to find the account name, primary_poc, and sales_rep_id for Walmart, Target, and Nordstrom.

``` sql
SELECT name,
       primary_poc,
       sales_rep_id
FROM accounts
WHERE name IN ('Walmart',
               'Target',
               'Nordstrom')
```

<hr>

### 15. Use the web_events table to find all information regarding individuals who were contacted via the channel of organic or adwords

``` sql
SELECT *
FROM web_events
WHERE channel IN ('organic',
                  'adwords')
```

<hr>

### 16. Use the accounts table to find the account name, primary poc, and sales rep id for all stores except Walmart, Target, and Nordstrom.

``` sql
SELECT name,
       primary_poc,
       sales_rep_id
FROM accounts
WHERE name NOT IN ('Walmart',
                   'Target',
                   'Nordstrom')
```

<hr>

### 17. Use the web_events table to find all information regarding individuals who were contacted via any method except using organic or adwords methods

``` sql
SELECT *
FROM web_events
WHERE channel NOT IN ('organic',
                      'adwords')
```

<hr>

### 18. All the companies whose names do not start with 'C'

``` sql
SELECT name
FROM accounts
WHERE name NOT LIKE 'C%';
```

<hr>

### 19. All companies whose names do not contain the string 'one' somewhere in the name

``` sql
SELECT name
FROM accounts
WHERE name NOT LIKE '%one%';
```

<hr>

### 20. All companies whose names do not end with 's'.

``` sql
SELECT name
FROM accounts
WHERE name NOT LIKE '%s';
```

<hr>

### 21. Write a query that returns all the orders where the standard_qty is over 1000, the poster_qty is 0, and the gloss_qty is 0.

``` sql
SELECT *
FROM orders
WHERE standard_qty > 1000
  AND poster_qty = 0
  AND gloss_qty = 0
```

<hr>

### 22. Using the accounts table, find all the companies whose names do not start with 'C' and end with 's'.

``` sql
SELECT *
FROM accounts
WHERE name NOT LIKE '%C'
  AND name LIKE '%s';
```

<hr>

### 23. Use the web_events table to find all information regarding individuals who were contacted via the organic or adwords channels, and started their account at any point in 2016, sorted from newest to oldest.

``` sql
SELECT *
FROM web_events
WHERE channel IN ('organic',
                  'adwords')
  AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC
```

<hr>

### 24. Find list of orders ids where either gloss_qty or poster_qty is greater than 4000. Only include the id field in the resulting table

``` sql
SELECT id
FROM orders
WHERE gloss_qty > 4000
  OR poster_qty > 4000
```

<hr>

### 25. Write a query that returns a list of orders where the standard_qty is zero and either the gloss_qty or poster_qty is over 1000

``` sql
SELECT *
FROM orders
WHERE standard_qty = 0
  AND (gloss_qty > 1000
       OR poster_qty > 1000)
```

<hr>

### 26. Find all the company names that start with a 'C' or 'W', and the primary contact contains 'ana' or 'Ana', but it doesn't contain 'eana'

``` sql
SELECT *
FROM accounts
WHERE (name LIKE 'C%'
       OR name LIKE 'W%')
  AND ((primary_poc LIKE '%ana%'
        OR primary_poc LIKE '%Ana%')
       AND primary_poc NOT LIKE '%eana%');
```

<hr>

### 27. Try pulling all the data from the accounts table, and all the data from the orders table 

``` sql
SELECT accounts.*,
       orders.*
FROM accounts
JOIN orders ON orders.id = accounts.id
```

<hr>

### 28. Try pulling standard_qty, gloss_qty, and poster_qty from the orders table, and the website and the primary_poc from the accounts table. 

``` sql
SELECT orders.standard_qty,
       orders.gloss_qty,
       orders.poster_qty,
       accounts.website,
       accounts.primary_poc
FROM orders
JOIN accounts ON accounts.id = orders.id
```

<hr>

### 29. Provide a table for all web_events associated with the account name of Walmart. There should be three columns. Be sure to include the primary_poc, time of the event, and the channel for each event. Additionally, you might choose to add a fourth column to assure only Walmart events were chosen 

``` sql
SELECT acct.name,
       acct.primary_poc,
       events.channel,
       events.occurred_at
FROM accounts AS acct
JOIN web_events AS EVENTS ON events.account_id = acct.id
WHERE acct.name = 'Walmart'
```

<hr>

### 30. Provide a table that provides the region for each sales_rep along with their associated accounts. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to the account name. 

``` sql
SELECT rep.name AS rept_name,
       acct.name AS account_name,
       r.name AS region_name
FROM sales_reps AS rep
JOIN accounts AS acct ON rep.id = acct.sales_rep_id
JOIN region AS r ON rep.region_id = r.id
ORDER BY acct.name
```

<hr>

### 31. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. Your final table should have 3 columns: region name, account name, and unit price. A few accounts have 0 for total, so I divided by (total + 0.01) to assure not dividing by zero. 

``` sql
SELECT r.name AS region_name,
       acct.name AS account_name,
       o.total_amt_usd/(o.total + 0.01) AS unit_price
FROM region AS r
JOIN sales_reps AS reps ON reps.region_id = r.id
JOIN accounts AS acct ON acct.sales_rep_id = reps.id
JOIN orders AS o ON o.account_id = acct.id
```

<hr>

### 32. Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to the account name 

``` sql
SELECT region.name AS region_name,
       reps.name AS rep_name,
       acct.name AS account_name
FROM region
JOIN sales_reps AS reps ON region.id = reps.region_id
JOIN accounts AS acct ON acct.sales_rep_id = reps.id
AND region.name = 'Midwest'
ORDER BY acct.name
```

<hr>

### 33. Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for accounts where the sales rep has a first name starting with S and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to the account name. 

``` sql
SELECT region.name AS region_name,
       reps.name AS reps_name,
       acct.name AS account_name
FROM region
JOIN sales_reps AS reps ON region.id = reps.region_id
AND region.name = 'Midwest'
AND reps.name LIKE 'S%'
JOIN accounts AS acct ON acct.sales_rep_id = reps.id
ORDER BY acct.name
```

<hr>

### 34. Find the total amount of poster_qty paper ordered in the orders table. 

``` sql
SELECT SUM(poster_qty) AS total_poster
FROM orders
```

<hr>

### 35. Find the total amount of standard_qty paper ordered in the orders table.  

``` sql
SELECT SUM(standard_qty) AS standard_total
FROM orders
```

<hr>

### 36. Find the total dollar amount of sales using the total_amt_usd in the orders table. 

``` sql
SELECT SUM(total_amt_usd) AS usd_total
FROM orders
```

<hr>

### 37. Find the total amount spent on standard_amt_usd and gloss_amt_usd paper for each order in the orders table. This should give a dollar amount for each order in the table. 

``` sql
SELECT standard_amt_usd + gloss_amt_usd AS standard_total_gloss
FROM orders
```

<hr>

### 38. Find the standard_amt_usd per unit of standard_qty paper. Your solution should use both aggregation and a mathematical operator

``` sql
SELECT SUM(standard_amt_usd)/SUM(standard_qty) AS standard_price_per_unit
FROM orders;
```

<hr>

### 39. When was the earliest order ever placed? You only need to return the date. 

``` sql
SELECT MIN(occurred_at)
FROM orders
```

<hr>

### 40. When was the earliest order ever placed? You only need to return the date. Do NOT use aggregation function

``` sql
SELECT occurred_at
FROM orders
ORDER BY occurred_at ASC
LIMIT 1;
```

<hr>

### 41. When did the most recent (latest) web_event occur? 

``` sql
SELECT MAX(occurred_at)
FROM web_events
```

<hr>

### 42. When did the most recent (latest) web_event occur? Do NOT use an aggregation function 

``` sql
SELECT occurred_at
FROM web_events
ORDER BY occurred_at DESC
LIMIT 1
```

<hr>

### 43. Find the mean (AVERAGE) amount spent per order on each paper type, as well as the mean amount of each paper type purchased per order. Your final answer should have 6 values - one for each paper type for the average number of sales, as well as the average amount 

``` sql
SELECT AVG(standard_qty) mean_standard,
       AVG(gloss_qty) mean_gloss,
       AVG(poster_qty) mean_poster,
       AVG(standard_amt_usd) mean_standard_usd,
       AVG(gloss_amt_usd) mean_gloss_usd,
       AVG(poster_amt_usd) mean_poster_usd
FROM orders;
```

<hr>

### 44. Which account (by name) placed the earliest order? Your solution should have the account name and the date of the order 

``` sql
SELECT acct.name AS account_name,
       o.occurred_at AS date_placed
FROM accounts AS acct
JOIN orders AS o ON o.account_id = acct.id
ORDER BY date_placed
LIMIT 1;
```

<hr>

### 45. Find the total sales in usd for each account. You should include two columns - the total sales for each company's orders in usd and the company name 

``` sql
SELECT acct.name AS account_name,
       SUM(o.total_amt_usd) AS total_sales
FROM accounts AS acct
JOIN orders AS o ON o.account_id = acct.id
GROUP BY acct.name
ORDER BY total_sales DESC
```

<hr>

### 46. Via what channel did the most recent (latest) web_event occur, which account was associated with this web_event? Your query should return only three values - the date, channel, and account name 

``` sql
SELECT acct.name,
       events.channel,
       events.occurred_at
FROM accounts AS acct
JOIN web_events AS EVENTS ON events.account_id = acct.id
ORDER BY events.occurred_at DESC
LIMIT 1;
```

<hr>

### 47. Find the total number of times each type of channel from the web_events was used. Your final table should have two columns - the channel and the number of times the channel was used 

``` sql
SELECT web_events.channel,
       COUNT(*)
FROM web_events
GROUP BY web_events.channel
```

<hr>

### 48. Who was the primary contact associated with the earliest web_event? 

``` sql
SELECT accounts.primary_poc,
       web_events.occurred_at
FROM accounts
JOIN web_events ON accounts.id = web_events.account_id
ORDER BY web_events.occurred_at
LIMIT 1;
```

<hr>

### 49. What was the smallest order placed by each account in terms of total usd. Provide only two columns - the account name and the total usd. Order from smallest dollar amounts to largest 

``` sql
SELECT accounts.name,
       MIN(orders.total_amt_usd) AS minimum_order
FROM accounts
JOIN orders ON accounts.id = orders.account_id
GROUP BY accounts.name
ORDER BY minimum_order
```

<hr>

### 50. Find the number of sales reps in each region. Your final table should have two columns - the region and the number of sales_reps. Order from the fewest reps to most reps 

``` sql
SELECT region.name,
       COUNT(sales_reps.id) AS number_of_reps
FROM region
JOIN sales_reps ON sales_reps.region_id = region.id
GROUP BY region.name
ORDER BY number_of_reps
```

<hr>

### 51. For each account, determine the average amount of each type of paper they purchased across their orders. Your result should have four columns - one for the account name and one for the average spent on each of the paper types. 

``` sql
SELECT accounts.name,
       AVG(standard_qty) AS standard_avg,
       AVG(gloss_qty) AS gloss_avg,
       AVG(poster_qty) AS poster_qty
FROM accounts
JOIN orders ON orders.account_id = accounts.id
GROUP BY accounts.name
```

<hr>

### 52. For each account, determine the average amount spent per order on each paper type. Your result should have four columns - one for the account name and one for the average amount spent on each paper type 

``` sql
SELECT accounts.name,
       AVG(standard_amt_usd) AS standard_usd_avg,
       AVG(gloss_amt_usd) AS gloss_usd_avg,
       AVG(poster_amt_usd) AS poster_usd_avg
FROM accounts
JOIN orders ON orders.account_id = accounts.id
GROUP BY accounts.name
```

<hr>

### 53. Determine the number of times a particular channel was used in the web_events table for each sales rep. Your final table should have three columns - the name of the sales rep, the channel, and the number of occurrences. Order your table with the highest number of occurrences first 

``` sql
SELECT sales_reps.name rep_name,
       web_events.channel,
       COUNT(web_events.channel) channel_count
FROM accounts
JOIN web_events ON accounts.id = web_events.account_id
JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
GROUP BY sales_reps.name,
         web_events.channel
ORDER BY channel_count DESC
```

<hr>

### 54. Determine the number of times a particular channel was used in the web_events table for each region. Your final table should have three columns - the region name, the channel, and the number of occurrences. Order your table with the highest number of occurrences first 

``` sql
SELECT region.name region_name,
       web_events.channel channel,
       COUNT(web_events.channel) AS num_channel
FROM accounts
JOIN web_events ON web_events.account_id = accounts.id
JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
JOIN region ON region.id = sales_reps.region_id
GROUP BY region_name,
         channel
ORDER BY num_channel DESC
```

<hr>

### 55. Use DISTINCT to test if there are any accounts associated with more than one region.

``` sql
SELECT accounts.id,
       region.id,
       accounts.name,
       region.name
FROM accounts
JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
JOIN region ON region.id = sales_reps.region_id
SELECT DISTINCT id,
                name
FROM accounts;
```

<hr>

### 56. How many of the sales reps have more than 5 accounts that they manage? 

``` sql
SELECT sales_reps.name,
       COUNT(accounts.id) AS num_of_accounts
FROM sales_reps
JOIN accounts ON accounts.sales_rep_id = sales_reps.id
GROUP BY sales_reps.name
HAVING COUNT(accounts.id) > 5
```

<hr>

### 57. How many accounts have more than 20 orders? 

``` sql
SELECT accounts.id account_id,
       accounts.name account_name,
       COUNT(*) total_orders
FROM accounts
JOIN orders ON accounts.id = orders.account_id
GROUP BY accounts.id,
         accounts.name
HAVING COUNT(*) > 20
```

<hr>

### 58. Which account has the most orders? 

``` sql
SELECT accounts.id,
       accounts.name,
       COUNT(*) total_orders
FROM accounts
JOIN orders ON accounts.id = orders.account_id
GROUP BY accounts.id,
         accounts.name
ORDER BY total_orders DESC
LIMIT 1;
```

<hr>

### 59. How many accounts spent more than 30,000 usd total across all orders?

``` sql
SELECT a.id,
       a.name,
       SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o ON a.id = o.account_id
GROUP BY a.id,
         a.name
HAVING SUM(o.total_amt_usd) > 30000
ORDER BY total_spent;
```

<hr>

### 60. How many accounts spent less than 1,000 usd total across all orders?

``` sql
SELECT a.id,
       a.name,
       SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o ON a.id = o.account_id
GROUP BY a.id,
         a.name
HAVING SUM(o.total_amt_usd) < 1000
ORDER BY total_spent;
```

<hr>

### 61. Which account has spent the most with us?

``` sql
SELECT a.id,
       a.name,
       SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o ON a.id = o.account_id
GROUP BY a.id,
         a.name
ORDER BY total_spent DESC
LIMIT 1;
```

<hr>

### 62. Which account has spent the least with us?

``` sql
SELECT a.id,
       a.name,
       SUM(o.total_amt_usd) total_spent
FROM accounts a
JOIN orders o ON a.id = o.account_id
GROUP BY a.id,
         a.name
ORDER BY total_spent
LIMIT 1;
```

<hr>

### 63. Which accounts used facebook as a channel to contact customers more than 6 times?

``` sql
SELECT a.id,
       a.name,
       w.channel,
       COUNT(*) use_of_channel
FROM accounts a
JOIN web_events w ON a.id = w.account_id
GROUP BY a.id,
         a.name,
         w.channel
HAVING COUNT(*) > 6
AND w.channel = 'facebook'
ORDER BY use_of_channel;
```

<hr>

### 64. Which account used facebook most as a channel?

``` sql
SELECT a.id,
       a.name,
       w.channel,
       COUNT(*) use_of_channel
FROM accounts a
JOIN web_events w ON a.id = w.account_id
WHERE w.channel = 'facebook'
GROUP BY a.id,
         a.name,
         w.channel
ORDER BY use_of_channel DESC
LIMIT 1;
```

<hr>

### 65. Which channel was most frequently used by most accounts?

``` sql
SELECT a.id,
       a.name,
       w.channel,
       COUNT(*) use_of_channel
FROM accounts a
JOIN web_events w ON a.id = w.account_id
GROUP BY a.id,
         a.name,
         w.channel
ORDER BY use_of_channel DESC
LIMIT 10;
```

<hr>

### 66. Find the sales in terms of total dollars for all orders in each year, ordered from greatest to least. Do you notice any trends in the yearly sales totals? 

``` sql
SELECT DATE_PART('year', orders.occurred_at) AS order_year,
       SUM(orders.total_amt_usd) AS total_usd
FROM orders
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 67. Which month did Parch & Posey have the greatest sales in terms of total dollars? Are all months evenly represented by the dataset? 

``` sql
SELECT DATE_PART('month', orders.occurred_at) AS order_month,
       SUM(orders.total_amt_usd) AS total_usd
FROM orders
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 68. Which year did Parch & Posey have the greatest sales in terms of the total number of orders? Are all years evenly represented by the dataset? 

``` sql
SELECT DATE_PART('year', orders.occurred_at) AS order_year,
       COUNT(orders.total) AS total_orders
FROM orders
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 69. Which year did Parch & Posey have the greatest sales in terms of the total number of orders? Are all years evenly represented by the dataset? 

``` sql
SELECT DATE_PART('month', orders.occurred_at) AS order_month,
       COUNT(orders.total) AS total_orders
FROM orders
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 70. In which month of which year did Walmart spend the most on gloss paper in terms of dollars 

``` sql
SELECT accounts.name,
       DATE_TRUNC('month', orders.occurred_at) AS order_month,
       SUM(orders.gloss_amt_usd) AS gloss_total_usd
FROM orders
JOIN accounts ON accounts.id = orders.account_id
AND accounts.name = 'Walmart'
GROUP BY 1,
         2
ORDER BY 3 DESC
LIMIT 1;
```

<hr>


### 71. Write a query to display for each order, the account ID, the total amount of the order, and the level of the order - ‘Large’ or ’Small’ - depending on if the order is $3000 or more, or smaller than $3000. 

``` sql
SELECT accounts.id account_id,
       orders.total_amt_usd total_amount,
       CASE
           WHEN orders.total_amt_usd > 3000 THEN 'Large'
           ELSE 'Small'
       END AS order_level
FROM accounts
JOIN orders ON orders.account_id = accounts.id
```

<hr>

### 72. Write a query to display the number of orders in each of three categories, based on the total number of items in each order. The three categories are: 'At Least 2000', 'Between 1000 and 2000' and 'Less than 1000'. 

``` sql
SELECT CASE
           WHEN total >= 2000 THEN 'At Least 2000'
           WHEN total BETWEEN 1000 AND 2000 THEN 'Between 1000 and 2000'
           WHEN total < 1000 THEN 'Less than 1000'
       END AS Order_Category,
       COUNT(*) AS total_orders
FROM orders
GROUP BY 1
```

<hr>

### 73. We would like to understand 3 different branches of customers based on the amount associated with their purchases. The top branch includes anyone with a Lifetime Value (total sales of all orders) greater than 200,000 usd. The second branch is between 200,000 and 100,000 usd. The lowest branch is anyone under 100,000 usd. Provide a table that includes the level associated with each account. You should provide the account name, the total sales of all orders for the customer, and the level. Order with the top spending customers listed first. 

``` sql
SELECT accounts.name customer_name,
       SUM(orders.total_amt_usd) cst_total,
       CASE
           WHEN SUM(orders.total_amt_usd) > 200000 THEN 'First Class'
           WHEN SUM(orders.total_amt_usd) BETWEEN 100000 AND 200000 THEN 'Second Class'
           WHEN SUM(orders.total_amt_usd) < 100000 THEN 'Third Class'
       END AS Consumer_Class
FROM accounts
JOIN orders ON orders.account_id = accounts.id
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 74. We would now like to perform a similar calculation to the first, but we want to obtain the total amount spent by customers only in 2016 and 2017. Keep the same levels as in the previous question. Order with the top spending customers listed first. 

``` sql
SELECT accounts.name customer_name,
       SUM(orders.total_amt_usd) cst_total,
       CASE
           WHEN SUM(orders.total_amt_usd) > 200000 THEN 'First Class'
           WHEN SUM(orders.total_amt_usd) BETWEEN 100000 AND 200000 THEN 'Second Class'
           WHEN SUM(orders.total_amt_usd) < 100000 THEN 'Third Class'
       END AS Consumer_Class
FROM accounts
JOIN orders ON orders.account_id = accounts.id
WHERE orders.occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
GROUP BY 1
ORDER BY 2 DESC
```

<hr>

### 75. We would like to identify top-performing sales reps, which are sales reps associated with more than 200 orders. Create a table with the sales rep name, the total number of orders, and a column with top or not depending on if they have more than 200 orders. Place the top salespeople first in your final table. It is worth mentioning that this assumes each name is unique - which has been done a few times. We otherwise would want to break by the name and the id of the table. 

``` sql
SELECT sales_reps.name rep_name,
       COUNT(*) total_orders,
       CASE
           WHEN COUNT(*) > 200 THEN 'Top Achiever'
           ELSE 'Normal'
       END AS rep_performance
FROM sales_reps
JOIN accounts ON accounts.sales_rep_id = sales_reps.id
JOIN orders ON orders.account_id = accounts.id
GROUP BY 1
ORDER BY 2 DESC
```

<hr>


### 76. The previous didn't account for the middle, nor the dollar amount associated with the sales. Management decides they want to see these characteristics represented as well. We would like to identify top-performing sales reps, which are sales reps associated with more than 200 orders or more than 750000 in total sales. The middle group has any rep with more than 150 orders or 500000 in sales. Create a table with the sales rep name, the total number of orders, total sales across all orders, and a column with top, middle, or low depending on these criteria. Place the top salespeople based on the dollar amount of sales first in your final table. You might see a few upset salespeople by this criteria! 

``` sql
SELECT sales_reps.name rep_name,
       COUNT(*) total_orders,
       SUM(orders.total_amt_usd) total_sales,
       CASE
           WHEN COUNT(*) > 200
                OR SUM(orders.total_amt_usd) > 750000 THEN 'Top'
           WHEN COUNT(*) > 150
                OR SUM(orders.total_amt_usd) > 500000 THEN 'Middle'
           ELSE 'Low'
       END AS rep_performance
FROM sales_reps
JOIN accounts ON accounts.sales_rep_id = sales_reps.id
JOIN orders ON orders.account_id = accounts.id
GROUP BY 1
ORDER BY 3 DESC
```

<hr>


### 77. Find the number of events that occur for each day for each channel 

``` sql
SELECT web_events.channel,
       DATE_TRUNC('day', web_events.occurred_at) AS DAY,
       COUNT(*) AS num_of_events
FROM web_events
GROUP BY 1,
         2
ORDER BY 3 DESC
```

<hr>

### 78. Find the average number of events for each channel. Since you broke out by day earlier, this is giving you an average per day. 

``` sql
SELECT channel,
       AVG(num_of_events)
FROM
  (SELECT web_events.channel,
          DATE_TRUNC('day', web_events.occurred_at) AS DAY,
          COUNT(*) AS num_of_events
   FROM web_events
   GROUP BY 1,
            2) AS subquery
GROUP BY 1
```

<hr>

### 79. Provide the name of the sales_rep in each region with the largest amount of total_amt_usd sales, using WITH 

``` sql
WITH table1 AS
  (SELECT sales_reps.name AS rep_name,
          region.name AS region_name,
          SUM(orders.total_amt_usd) AS sales_total
   FROM accounts
   JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
   JOIN region ON region.id = sales_reps.region_id
   JOIN orders ON orders.account_id = accounts.id
   GROUP BY 1,
            2
   ORDER BY 3 DESC),
     table2 AS
  (SELECT region_name,
          MAX(sales_total) sales_total
   FROM table1
   GROUP BY 1)
SELECT table1.rep_name,
       table1.region_name,
       table1.sales_total
FROM table1
JOIN table2 ON table1.region_name = table2.region_name
```

<hr>

### 80. For the region with the largest (sum) of sales total_amt_usd, how many total (count) orders were placed? Using subqueries 

``` sql
WITH sales_by_region AS
  (SELECT region.name,
          SUM(orders.total_amt_usd) AS total_sales_amount
   FROM accounts
   JOIN orders ON orders.account_id = accounts.id
   JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
   JOIN region ON region.id = sales_reps.region_id
   GROUP BY region.name),
     most_orders_region AS
  (SELECT MAX(total_sales_amount)
   FROM sales_by_region)
SELECT region.name region_name,
       COUNT(orders.total) AS total_sales
FROM accounts
JOIN orders ON orders.account_id = accounts.id
JOIN sales_reps ON sales_reps.id = accounts.sales_rep_id
JOIN region ON region.id = sales_reps.region_id
GROUP BY region_name
HAVING SUM(orders.total_amt_usd) =
  (SELECT *
   FROM most_orders_region)
```

<hr>

### 81. How many accounts had more total purchases than the account name which has bought the most standard_qty paper throughout their lifetime as a customer? 

``` sql
WITH most_qty_sales AS
  (SELECT accounts.name,
          SUM(orders.standard_qty) AS total_std_qty,
          SUM(orders.total) total_orders
   FROM accounts
   JOIN orders ON orders.account_id = accounts.id
   GROUP BY 1
   ORDER BY 2 DESC
   LIMIT 1)
SELECT COUNT(*)
FROM
  (SELECT accounts.name,
          COUNT(orders.total)
   FROM accounts
   JOIN orders ON orders.account_id = accounts.id
   GROUP BY 1
   HAVING SUM(orders.total) >
     (SELECT total_orders
      FROM most_qty_sales)) AS t1
```

<hr>

### 82. For the customer that spent the most (in total over their lifetime as a customer) total_amt_usd, how many web_events did they have for each channel? 

``` sql
SELECT accounts.id,
       accounts.name,
       web_events.channel,
       COUNT(*)
FROM web_events
JOIN accounts ON accounts.id = web_events.account_id
GROUP BY 1,
         2,
         3
HAVING accounts.id =
  (SELECT acc_id
   FROM
     (SELECT accounts.id acc_id,
             accounts.name,
             SUM(orders.total_amt_usd) AS total_sales
      FROM accounts
      JOIN orders ON accounts.id = orders.account_id
      GROUP BY 1,
               2
      ORDER BY 3 DESC
      LIMIT 1) AS t1)
ORDER BY 4 DESC
```

