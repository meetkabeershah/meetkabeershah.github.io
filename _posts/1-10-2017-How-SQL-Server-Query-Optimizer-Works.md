---
layout : post
title: How does the SQL Server Query Optimizer Works
---

![Optimization](http://emotimo.com/wp-content/uploads/2015/12/SPEED.jpg)

[Courtesy](https://www.keyword-suggestions.com/c3BlZWQ/)

At the core of the SQL Server Database Engine are two major components: the **Storage Engine** and the **Query Processor**, also called the Relational Engine.

 - Storage Engine: takes care of reading data between the disk and memory in a manner that optimizes concurrency while maintaining data integrity
 - Query Processor: 1. takes care of devising a query plan (what algorithms/operators to implement) by **Query Optimizer** 2. execute the query according to that plan by **Execution Engine**

The query processor does the following things:

 1. Query parsing
 2. Binding query to objects
 3. Generate possible execution plans
 4. Cost-assessment of each plan

The Execution Engine does the following things:
 1. Query execution
 2. Plan caching

Parsing translates the SQL query into an initial tree representation. Binding is mostly concerned with name resolution.

# Search Space 

We define the search space for a given query as the set of all the possible execution plans for that query, and any possible plan in this search space returns the same results.

# Generating Candidate Execution Plans

As discussed, the basic purpose of the Query Optimizer is to find an efficient execution plan for your query. Even for relatively simple queries, there may be a large number of different ways to access the data to produce the same end result. As such, the Query Optimizer has to select the best possible plan from what may be a very large number of candidate execution plans, and it’s important that it makes a wise choice, as the time it takes to return the results to the user can vary wildly, depending on which plan is selected.

The Query Optimizer must strike a balance between optimization time and plan quality. SQL Server does not do an exhaustive search, but instead tries to find a suitably efficient plan as quickly as possible.

# Assessing the Cost of each Plan

The Query Optimizer needs to estimate the cost of these plans and select the least expensive one. To estimate the cost of a plan, it estimates the cost of each physical operator in that plan using costing formulas that consider the use of resources such as I/O, CPU, and memory.

**Cardinality estimation** : a query plan's cost estimation depends mostly on the algorithm used by the physical operator, as well as the estimated number of records that will need to be processed; this estimate of the number of records is known as the cardinality estimation.

# Query Execution and Plan Caching

Once the query is optimized, the resulting plan is used by the Execution Engine to retrieve the desired data. The generated execution plan may be stored in memory, in the plan cache (known as the procedure cache in previous versions of SQL Server) in order that it might be reused if the same query is executed again.

However, reuse of an existing plan may not always be the best solution for a given query. Depending on the distribution of data within a table, the optimal execution plan for a given query may differ greatly depending on the parameters provided in said query, and a behavior known as [parameter sniffing](https://www.brentozar.com/archive/2013/06/the-elephant-and-the-mouse-or-parameter-sniffing-in-sql-server/) may result in a suboptimal plan being chosen.

Even when an execution plan is available in the plan cache, some metadata changes, such as removing an index or a constraint, or significant enough changes made to the contents of the database, may render an existing plan invalid or suboptimal, and thus cause it to be discarded from the plan cache and a new optimization to be generated.

# Recompiling

You can force SQL Server to recompile the stored procedure each time it is run. The benefit here is that the best query plan will be created each time it is run. However, recompiling is a CPU-intensive operation. This may not be an ideal solution for stored procedures that are run frequently, or on a server that is constrained by CPU resources already. Another thing to remember is that the plans won’t be stored in the cache, which makes them harder to find if they are problematic.

<pre> <code>
ALTER PROCEDURE Get_OrderID_OrderQty
@ProductID INT
WITH RECOMPILE
AS
SELECT SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE ProductID = @ProductID;
</code> </pre>

# Hinting

Another option is to use the OPTIMIZE FOR query hint. This tells SQL Server to use a specified value when compiling the plan. If, through testing, you can find a value that produces a “good enough” plan each time, and the performance is acceptable for both mice and elephants, this is a good option for you.

However, understand that you are bossing the query optimizer around. You are telling it what you think is best. The biggest drawback with OPTIMIZE FOR is on tables where the distribution of data changes. The faster it changes, the more out of date this hint could become. What if the value you provide is not optimal in a month, or a year? You need to have a method in place to regularly review and revise this.

<pre> <code>
ALTER PROCEDURE Get_OrderID_OrderQty
@ProductID INT
AS
SELECT SalesOrderDetailID, OrderQty
FROM Sales.SalesOrderDetail
WHERE ProductID = @ProductID
OPTION (OPTIMIZE FOR (@ProductID=945));
</code> </pre>

> The reality is that, even after more than 30 years of research, query optimizers are highly complex pieces of software which still face some technical challenges. As a result, there may be cases when, even after you’ve provided the Query Optimizer with all the information it needs and there doesn’t seem to be any apparent problem, you are still not getting an efficient plan.

Sources:

 - [The Elephant and the Mouse, or, Parameter Sniffing in SQL Server](https://www.brentozar.com/archive/2013/06/the-elephant-and-the-mouse-or-parameter-sniffing-in-sql-server/)
 - [The SQL Server Query Optimizer](https://www.simple-talk.com/sql/sql-training/the-sql-server-query-optimizer/)
