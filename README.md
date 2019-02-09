![ScreenShot](images/quantum.jpg)
<h1>WELCOME TO QUANTUM</h1>

<h2>An Engine For Fast Time Series Data Aggregation</h2>

All analytics, whether looking back in time or attempting to predict the future, requires the ability to observe trends in data collected over time.
The tools we use today to slice, dice and aggregate time-series data are mainly SQL-based and are too cumbersome to craft or too slow to return the
desired results especially when querying very large data sets.

Quantum was created to address the problems above. It leverages data-streaming and in-memory caching to produce aggregated time-series data that can
be queried in O(1) time complexity. Quantum consists of a multi-dimensional aggregation engine and a query language called QL. 

<h3>Simple Example</h3>

Suppose we have purchase transaction records like so collected over a time period.
For this example, the records are stored in transactions.csv (in real-world usage, the records might be streamed).

|DateTime|CustomerId|ProductId|Quantity|TotalPrice|
|------- |----------|---------|--------|----------|
|2018-04-11 21:41:33|C1|P1|2|10.0|
|2018-04-11 22:41:33|C2|P1|5|7.0|
|2018-04-12 01:08:04|C6|P2|3|44.0|
|2018-04-12 01:12:12|C3|P2|3|15.0|
|2018-04-12 01:14:11|C2|P2|8|135.0|
|2018-04-12 02:00:22|C3|P4|3|23.0|
|2018-04-12 03:12:17|C1|P7|3|45.0|
|2018-04-12 05:06:09|C7|P1|3|88.0|
|2018-04-12 11:02:14|C5|P6|3|19.0|
|2018-04-12 14:07:16|C5|P5|3|11.0|
|2018-04-13 04:03:12|C4|P2|3|10.0|

We would like to ask questions such as:

1. How much dollar volume did product, P1 produce in the last n months, n days, n hours, n minutes?
2. What was the total quantity purchased for product, P1 on 2018-04-11 bewteen 21:00 and 23:00?

We will first define Quantum's DDL stored in a file 'myagg.yml' to process our data set as shown below:
```
   myagg:
      data_source:
         type: csv
         path: transactions.csv
      data_type: transaction
      dimensions:
         - ProductId      time:
         - year
         - month
         - day
         - hour
         - min
      measures:
         - Quantity
         - TotalPrice
      datetime_field_name: DateTime
      datetime_field_format: YYYY-mm-dd HH:MM:SS
```

Explanation of the fields:

* data_source - specifies where the data records will come from. In the example, it's a csv file called 'transactions.csv'. 
* data_type - the type of our record and we've called it, 'transaction'.
* dimensions - the dimensions in our record that we want to aggregate, in this case ProductId
* time - the time dimensions which we want to aggregate (Quantum supports year, month, week, day, day_of_week, hour, min, sec)
* measures - the numeric columns which we want to aggregate over (Quantum supports sum and average)
* datetime_field_name - the name of the date/time field in the data set
* datetime_field_format - the format of the date/time field

We then run quantum like so:

    quantum myagg.yml




