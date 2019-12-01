---
layout: post
title: Execution plan in SQL Server
---
![Execution plan](http://blog.teamtreehouse.com/wp-content/uploads/2013/10/idea-execution.png)

[Courtesy](http://blog.teamtreehouse.com/working-in-a-flat-company)

The first step in optimizing a query is looking at it's execution plan. An execution plan is a visual representation of the operations performed by the database engine in order to return the data required by your query.

The execution plan for a query is your view into the SQL Server query optimizer and query engine. It will reveal which **objects a query uses**, object like:

 - tables 
 - indexes 
 - etc.

type of uses:

 - in which order
 - how they were accessed (seek or scan)
 - types of joins
 - data size
 - filtering
 - sorting
 - aggregations
 - calculated columns derivation
 - foreign keys access
 - etc.

within the database, and how it uses them.

There are 3 types of execution plans:
 - Estimated
 - Actual
 - Cached

# Estimated execution plan:
To get a query's estimated execution plan:
 - Switch to the database in concern
 - highlight the query in concern
 - click **Query**
 - click **Display Estimated Execution Plan**

![Estimated execution plan](https://lh3.googleusercontent.com/SbQqqs2NaKllY9Ez9-3RbqXilnUFzYaeF1UcILDWhfhBrDW8ABohAklCTlP3M6kt3NTIz9fnPu_030uulgjq_ire8DySlL_V1FGoEMLyAMOVbWbHswCOHE3o9WP98YwV8-6iWGzHpCEauzjkZpmFJoW49NLeXC1Eg5lfpVP6iVYVTrwS5zTIBnGX4mI17ZA4xcqTo-ae_HxpNhWovqxMkLpFRXpbHkCgwPdWTpVfgaavcLPxuZsVTZwfwgQXaGEAloH6fCQrEMQ3Dy0WegA7tBbjcYmxBAoQ5vrpV5yWamfhkOZjDxj9hDIUsO7feMNm6v0bi_ogmFSuzAn3_T6lG_jbSyH1Xd405ui1j-_Q5444jMyG33OnHnmqOOiS9AoY4k4IRN8rygWYqbxXP8bnTk7q9YxO9b9F6310f2p16nEIVo1IM8BmHeoA_pYXWG3Bv8sHi5vc8kgI-WGVGJryjvPGilvHG7XQPhozsx7-b0QIdsJ-G-JceFZHgrSFa0phIj9DRawJyfZEmOIaJwEpGZUxQfRF6TY2Mloa65R5wsMTnKbTBwtBTpxnPSDujHnJOwLICpJdp0eAj-mJCxY0VqWYKFBAWmoq5Q6QYlZH__ugDKdC4rFE=w286-h132-no)

The shortcut for this is <kbd>Ctrl</kbd>+ <kbd>L</kbd>. When you get this plan, some sections of the query might show a very high percentage as cost. 

![Estimated execution plan](https://lh3.googleusercontent.com/D2YV45Mwz09QBApfL1J4_WmrivdI6LKGcH3Ox6stm0_I83MknL29ylMDGneesmIG4LjJdsCj6LW0XoE3TTlu-o8D5JLAscq5hZCBxbvGcS-U-6pqmkA-BcrmQ1puhUwvcKj3sdCidNClf5cU-DdhTUPZdF7i46Js0pVbNLa0c9BulwcAEIT3LuiDtpa3J377zAJhjezPAw7C_CXfs1Usp6_hU-gVsnNq-msIPGM-yDnCryyv-ioDOJzrKfo6LTqGNV2MSrppeOCjELeqR0QQgRlx00x0yztzSMLmu6i9e1aRCfubYup-H5jIpn8IXNesaEAfmqfoM5BslLyNoW61w6Hpj_M_9_uPXrz6qPmWKRzr20sHkzi1iIeUcd_IV6oNtHdihtSAXkDAOWshPRPGNQMMbyyCEREAwekHTRIjA-zMBbmtnZIefs07wvTfZIEsoAKQOP5uP9X3TUZqU0-n-IqeADulRPp6TowbprHMZL4casC6aYvZSpYxXt5V6HJZTbPv6aTuhZ_eaQFtlpopzy0zcxj0UjFOyYM6dzxqVJ1zzZgREtOnW4OCxTfGfSSn46amFfV0PSrYHInPQW5D6gNHW4dPfoj83fogEruO7nKPRlNfekDz=w673-h263-no)

Remember that this is just an estimate, and many a times what we see as the most expensive section comes up as the most cheapest or cheap.

Btw, each symbol in the execution plan is an operator, and each operator has additional information within its properties that define the work performed by that operator.

# Actual execution plan:
To get a query's actual execution plan:
 - Switch to the database in concern
 - highlight the query in concern
 - click **Query**
 - click **Include Actual Execution Plan**

![Actual execution plan](https://lh3.googleusercontent.com/QWUMsAa0SfH_VXLGdmF7WBU-pg25yAd2zQi6a7EO_JRuuS8QzlhNsxbOmx4QTz1JwkzU46JUcV6y6x4YUGaJpJIzGAywauz73gYsbm0EoqOpYjWHt3_UWsgVpiX4yOIAieayU4caNO-6_5zx1euGWGDPn2j8sGnBd_Ul4ErIS_iqTGGZS12jShwjV0JlyWYzHvqs4KybTy6GBkSEUEaphevuQ29n-E_qZOcKJXdMEEzfAPrwvRzF4tbub2ugC6pNWIxIJpgTP4p8Bx9Sa7ojfIfIjbPj6n0d6xXNvZF4G1ITWbYKqu9dBe-DPkwF_WM2s0VSKoZgCooA5bsXBPR1hrhtgx-e9Uwnwvo0fWKUmpHN6gmaS3c_sDnm4ntSQLD0Gbr0sX2SuZtUuynI_2uvbPSvngPSr7NvAsJE6Sfa4V-OCb5K9D700LKSv94vVr4nKgzHqouElhxzAEg_PEI1ORiD0Zp2ga8AHKKNAisFwyrnfC6VP2epRJZngJ9_RLPkVmedkTuwJswsN4QKRevgsoZ0F49dzITBoBCfixD-cURa4Cq9m7yFfvgz58ZV6urJtxYNIQFdpTOByGptMMPBHLC6dfprW7F9YbqF-jqKAj9RQQaAfPwy=w285-h207-no)

The shortcut for this is <kbd>Ctrl</kbd>+ <kbd>M</kbd>. One of the queries gave this actual execution plan. 

![Actual execution plan](https://lh3.googleusercontent.com/ro-K9foM9sygQWYFmSVblyPCEyVx1BpXT6t1n3bgGw-Z7fWgl7kDye4Le4rBQsaATXmlXZ0gp7cGWiJYNU_MgAMua01WMEKgPDFjc7M6ntJgtf8yVcTMTOAb1fSPR3B9Nq3csGY_dt8sFuPa_jzzKMSLR8iTGj5bP50kai6cTFVbilzuJHJH-GM4c-5O-NY7eXcvzWU5XtZOAE7triwJcm91_0NbTwiary1J9r1bdXhZSKky-hbo8jvDPVVMhmqQkusHF-NJG6pnnqe7t63kXos9-wxYWNRJ-ir9hcriSM74W4_Dm6qOvC-1W82AFB6njBEwBe03AqK8Na0T3Ae-gs1x1c7kikc11yHEHFzPKucXAa6NR4I8G-6Ptd_trVwl8e854DKGsA5OVg-tlb5ZRzhOvOGWfPM0VVH52rJ4U_7vWIxLcrYKASpCcZB9ne8OOqXzJqbEV0Gcg-dfgKbu9W0bWsqH-vDVZyCp2xF2VTk5lRf5Utaw7v-ym2pNWbwjNKTUlT7qmBK1lqwjxS7K9_1S4Knr5sChOp6BOJbXvnGnm10cxlfUTds33LxHrir42PXq5D-o1pHmfSBZMt0Zt2QUVb21lyS7rqogLDfjJPsWagN3p_hH=w447-h509-no)

Look at the actual vs estimated numbers, looks like the estimate is good enough. One of other queries gave this execution plan:

![Actual execution plan](https://lh3.googleusercontent.com/Co9T6YKSW-e0C4jv_LvIcKFlShabw-z-J2NtZyG7HEAF4trM29OtAY9pbM2ljcIAOAs0wsTqF9kcQRDop2KKmM86KDgh9LQKFTStVt7VylgYcx1rxIMSdCFH3xy4TpOdEcwKA3xoEFL58e-Oa113GbfMQXGHd6Xx4t0NvQA0JmIeWu1rikpNz9dcRxZ4QctArPK28EHuMBL7-AcT1yCBg7yVCM7_K6_Kma4NcPxJ57S5K3Ibmibh0sExGrsFfiB4h1DoXOiu-PffD1HWC3rN3ZWgh3BwUojrTdaJUiB_YR8xut1I87Kjyhhf1KSXSLVHppVPSNUu2eSeRbYaPFS1geubE6AZzSkoFkZdRZtX8mAaaOPdq-IvC86w2e21cY3DWmCljNgJ_oINISPm0Q3gqjObt2XxvXhdxOq2e1jeA5rMFzXPMnlLLVc4JC4FT0E8bQxQA1GDlHhNraf5D_uY54YxAcKH2xFz0mJ6wMKlhGT_Dy_NRZE7wIQtSbJVym4wtEVMdfu3NhY0gv9g3Nf7z4frYYLLOJFaMgxlc-NwZmP5GvKQPY0xkTdPXcDTa77FLfrsLtjh9E5xyUGTwhtccnA3QgKqQdgsBA7fZ6EZumo1spC3KyUI=w414-h495-no)

Looks like the estimates and actuals are far different.

This proves that **actual execution plan are always good to tune compared to estimates**. Btw, we read execution plans from left to right and top to bottom.

The estimated percentage costs at the front level are **still estimates**. So to tune the queries, it looks like we need to go through each of the blocks one-by-one. This looks like a lot of pain. This is where the 3<sup>rd</sup> type of execution plans comes into the picture - the **cached execution plan**.

# Cached execution plan:

There is a [free cool utility](http://xameeramir.github.io/BlitzKrieg-SQL-Server-diagnosis/) to find out which queries we actually need to tune. Just hit [http://www.brentozar.com/blitzcache](http://www.brentozar.com/blitzcache) and grab <code>sp_BlitzCache</code>.

Just execute this <code>EXEC sp_BlitzCache @top=10, @sort_order='duration'</code>. This query will give the top 10 queries with the most execution time. In a column it also shows the possible problems like missing indexes, downlevel cardinality estimates and implicit conversions in the **Warnings** column. In the **Query Plan** column, it gives the actual execution plan map link which can be clicked upon.

# Query Tuning:

The single largest use for execution plans is query tuning. It’s the most common tool for understanding what you want to tune. It’s invaluable for identifying and fixing poorly performing code. I can’t run through every potential cause of poor query performance here, or even close, but we can look briefly at a few of the common culprits and the warning signs you’ll find in the execution plan.

**Poorly Designed Queries**

Like with any language, there are common code smells within T-SQL. I’ll list out a few of them as well as what you might see in the execution plan.

**Search Conditions with Functions**

Placing a function on a column in the <code>ON</code>, <code>HAVING</code> or <code>WHERE</code> clause (e.g. <code>WHERE  SomeFunction(Column) = @Value )</code> can lead to very poor performance because it renders the predicate non-SARGable, which means that SQL Server cannot use it in an index seek operation. Instead, it will be forced to read the entire table or index. In the execution plan, look out for a Scan operator against a table or index where you expected a Seek operation, i.e. a single or small set of lookups within an index.

**Nesting Views**

Having a view that calls to other views or has <code>JOIN</code> operations to other views can lead to very poor performance. The query optimizer goes through a process called simplification, where it attempts to eliminate tables that are not needed to fulfil the query, helping to make it faster. For simple queries involving views or functions, the optimizer will simply access the underlying base tables, and perform table elimination in the usual fashion. However, use of nested views and functions will lead quickly to a very complex query within SQL Server, even if the query looks simple in the T-SQL code. The problem is that beyond a certain point, SQL Server can’t perform the usual simplification process, and you’ll end up with large complex plans with lots of operators referencing the tables more than once, and so causing unnecessary work.

**Incorrect Data Type Use**

Of course, to do this it must apply the conversion function to the column, in the <code>ON</code>, <code>HAVING</code> or <code>WHERE</code> clause and we are back in the situation of having a non-SARGable predicate, leading to scans where you should see seeks. You may also see a warning indicating an implicit conversion is occurring.

**Row-by-row Processing**

Row-by-row approach is expressed via cursors and sometimes as <code>WHILE</code> loops that often lead to extremely poor performance. In such cases, rather than a single execution plan, you’ll see one plan for each pass through of the loop, and SQL Server essentially generates the same plan over and over, to process each row.

# Common Warning Signs in the Execution Plan

**Warnings**

These are red crosses or yellow exclamation marks superimposed on an operator. There are sometimes false positives, but most of the time, these indicate an issue to investigate.
Costly Operations – the operation costs are estimated values, not actual measures, but they are the one number provided to us so we’re going to use them. The most costly operation is frequently an indication of where to start troubleshooting

**Fat Pipes**

Within an execution plan, the arrows connecting one operator to the next are called pipes, and represent data flow. Fat pipes indicate lots of data being processed. Of course, this is inevitable if the query simply has to process a large amount of data, but it can often be an indication of a problem. Look out for transitions from very fat pipes to very thin ones, indicating late filtering and that possibly a different index is needed. Transitions from very thin pipes to fat ones indicates multiplication of data, i.e. some operation within the T-SQL is causing more and more data to be generated.

**Extra Operators**

Over time you’ll start to recognize operators and understand quickly both what each one is doing and why. Any time that you see an operator and you don’t understand what it is, or, you don’t understand why it’s there, then that’s an indicator of a potential problem.

**Scans**

We say this all the time, scans are not necessarily a bad thing. They’re just an indication of the scan of an index or table. If your query is <code>SELECT * FROM TableName</code>, with no <code>WHERE</code> clause then a scan is the best way to retrieve that data. In other circumstances, a scan can be an indication of a problem such as implicit data conversions, or functions on a column in the <code>WHERE</code> clause.

Let’s take a look at a few of the warning signs that can appear, and what we can do in response. 

<pre> <code>
DECLARE @LocationName AS NVARCHAR(50);
 
SET @LocationName = 'Paint';
 
SELECT  p.Name AS ProductName ,
        pi.Shelf ,
        l.Name AS LocationName
FROM    Production.Product AS p
        JOIN Production.ProductInventory AS pi ON pi.ProductID = p.ProductID
        JOIN Production.Location AS l ON l.LocationID = pi.LocationID
WHERE   LTRIM(RTRIM(l.Name)) = @LocationName;
GO
</code> </pre> 

![Execution plan with problems](https://www.simple-talk.com/wp-content/uploads/imported/2123-1-1bdb2f5d-54d0-423b-ad5f-788271507ef2.png)

And the problems are as follows:


1. The INDEX SCAN on the <code>Location.Name</code> column – there’s an index on that column a SEEK is expected - culrit: <code>LTRIM(RTRIM(l.Name))</code>, in the <code>WHERE</code> clause
2. The FAT PIPE coming out of the Clustered Index Scan on the ProductInventory table – in this example, it’s processing over 1000 rows at this stage, and eventually only returning 9 rows. - culprit: missing index on the column.
3. The HASH MATCH join – for the number of rows returned I’m expecting a NESTED LOOPS join - culprit: bad or missing indexes.

**Poor Indexing**

At the top of some execution plans, you may even see an explicit **Missing Index** suggestion, indicating that the optimizer recognized that if it had a certain index, it might be able to come up with a better plan. Note these, but do not assume they’re accurate. Test them before applying them.

**Nesting Views**

A view is just a query that the optimizer resolves just like any other query. However, if you decide to JOIN a view to a view, or nest views inside of each other, it causes problems for SQL Server. Firstly, as the number of referenced objects increases, due to deep nesting, the optimizer, which only has so much time to try to optimize the query, will give up on simplification and just build a query for the objects defined. For each object, the optimizer must estimate the number of rows returned and, based on that, the most efficient operation to use to return those rows. However, once we go beyond **three** levels deep on obfuscation, the optimizer stops assigning costs and just assumes one row returned. All of this can result in very poor choices of plan and a lot of avoidable work.

To illustrate how nesting views can hurt the server, consider this:

<pre> <code>
SELECT  pa.PersonName,
        pa.City,
        cea.EmailAddress,
        cs.DueDate
FROM    dbo.PersonAddress AS pa
JOIN    dbo.CustomerSales AS cs
        ON cs.CustomerPersonID = pa.PersonID
LEFT JOIN dbo.ContactEmailAddress AS cea
        ON cea.ContactPersonID = pa.PersonID
WHERE   pa.City = 'Redmond';
</code> </pre> 

All the 3 referenced objects are views. And the execution plan will be so complex like this:

![Nested views execution plan](https://www.simple-talk.com/iwritefor/articlefiles/2123-executionplans%20image10.png)

The simplication of the above query can be done by actually accessing the underlying tables like this:

<pre> <code>
SELECT  p.LastName + ', ' + p.FirstName AS PersonName ,
        a.City ,
        ea.EmailAddress ,
        soh.DueDate
FROM    Person.Person AS p
        JOIN Person.EmailAddress AS ea
              ON ea.BusinessEntityID = p.BusinessEntityID
        JOIN Person.BusinessEntityAddress AS bea
              ON bea.BusinessEntityID = p.BusinessEntityID
        JOIN Person.Address AS a
              ON a.AddressID = bea.AddressID
        LEFT JOIN Person.BusinessEntityContact AS bec
              ON bec.PersonID = p.BusinessEntityID
        JOIN Sales.Customer AS c
              ON c.PersonID = p.BusinessEntityID
        JOIN Sales.SalesOrderHeader AS soh
              ON soh.CustomerID = c.CustomerID
WHERE   a.City = 'Redmond';
</code> </pre>

The execution plan is much simplified now:

![Avoiding views to simplify execution plan](https://www.simple-talk.com/iwritefor/articlefiles/2123-executionplans%20image11.png)

**Lack of Database Constraints**

Consider this query:

<pre> <code>
SELECT  soh.OrderDate ,
        soh.ShipDate ,
        sod.OrderQty ,
        sod.UnitPrice ,
        p.Name AS ProductName
FROM    Sales.SalesOrderHeader AS soh
        JOIN Sales.SalesOrderDetail AS sod
              ON sod.SalesOrderID = soh.SalesOrderID
        JOIN Production.Product AS p 
              ON p.ProductID = sod.ProductID
WHERE   p.Name = 'Water Bottle - 30 oz.'
        AND sod.UnitPrice < $0.0;
</code> </pre>

With no constraints in place, the execution plan for this query will look as shown:

![Simplify execution plan by using constraints](https://www.simple-talk.com/iwritefor/articlefiles/2123-executionplans%20image12.png)

This query returns zero rows, since there are no products with a price less than $0, and yet SQL Server still performs an index scan, two index seeks and a couple of nested loop joins. The reason is that it has no way to know they query will return zero rows.

However, what if we have a constraint in place on the SalesOrderDetail table that requires that the UnitPrice for any row be greater than zero (this constraint already exists in the AdventureWorks database).

<pre> <code>
ALTER TABLE Sales.SalesOrderDetail  WITH CHECK
  ADD  CONSTRAINT CK_SalesOrderDetail_UnitPrice CHECK  ((UnitPrice>=(0.00)));
</code> </pre>

If we rerun the above code with this constraint in place, then the execution plan is interesting:

![Simplify execution plan by using constraints](https://www.simple-talk.com/wp-content/uploads/imported/2123-1-6205d3e8-1153-41d4-926a-9132a38e807b.png)

**Missing or out-of-date Database Statistics**

The statistics can be turned off or on by the following command:

<pre> <code>
SET AUTO_UPDATE_STATISTICS OFF | ON;
</code> </pre>

It is recommended to not set them off to avoid stale statistics.

**Maybe it’s not the Database?**

It's also possible that the database is not the culprit, the application can cause performance problems. So, profile the application code as well.

**Sources:**

 - [Execution plan benefits](https://www.simple-talk.com/sql/performance/why-developers-need-to-understand-execution-plans)
 - [Types of execution plans](https://www.youtube.com/watch?v=XKghrpVSbc0)
 - [Photos](https://goo.gl/photos/jJ1Da5nMAUMmCZr87)