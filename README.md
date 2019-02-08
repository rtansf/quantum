![ScreenShot](images/quantum.jpg)
<h1>WELCOME TO QUANTUM</h1>

<h2>An Engine For Fast Time Series Data Aggregation</h2>

All analytics, whether looking back in time or attempting to predict the future, requires the ability to observe trends in data collected over time.
The tools we use today to slice, dice and aggregate time-series data are mainly SQL-based and are too cumbersome to craft or too slow to return the
desired results especially when querying very large data sets.

Quantum was created to address the problems above. It leverages data-streaming and in-memory caching to produce aggregated time-series data that can
be queried in O(1) time complexity. Quantum consists of a multi-dimensional aggregation engine and a simple query language called QQL. 

<h3>Example</h3>

Suppose we have purchase transaction records with the following fields:

   DateTime
   CustomerID
   ProductID
   Quantity
   TotalPrice

And we have the data set below:

|DateTime|CustomerId|ProductId|Quantityy|TotalPrice|
|------- |----------|---------|---------|----------|
|2018-04-11T22:41:33Z|C1|P1|2|10.0|
|2018-04-11T23:41:33Z|C2|P1|5|7.0|
|2018-04-12T01:12:12Z|C3|P2|3|15.0|
|2018-04-12T01:14:11Z|C2|P2|8|135.0|
|2018-04-13T04:03:12Z|C4|P2|3|10.0|
|2018-04-12T02:00:22Z|C3|P4|3|23.0|
|2018-04-12T11:02:14Z|C5|P6|3|19.0|
|2018-04-12T03:12:17Z|C1|P7|3|45.0|
|2018-04-12T01:08:04Z|C6|P2|3|44.0|
|2018-04-12T05:06:09Z|C7|P1|3|88.0|
|2018-04-12T14:07:16Z|C5|P5|3|11.0|
