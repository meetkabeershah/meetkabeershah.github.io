---
layout: post
title: SQL Server Index Tuning
---
![Index](http://www.clipartsfree.net/vector/large/19673-divider-cards-vector.png)

[courtesy](http://www.clipartsfree.net/search.php?load=divider%20cards)

A few reasons why people don’t tune their indexes:

>“We can’t make this change until we know exactly how much it will improve, and how it will scale.”

----------

>“There’s no good time to change indexes.”

----------

>“It’s too risky.”

----------

>“Our indexes are in perfect order.”

# How to Master SQL Server Index Tuning in One Step

**Here’s that one step:** stop thinking index tuning is a problem for Future You, because it may always be a problem...

# Indexing Dos and Dont's

Indexing is such a large subject that getting a handle on what to do and what not to do when you're developing your indexing strategies can be difficult. You create indexes to improve query response time. But indexing is a balancing act.

We try to enhance query response by creating indexes—but doing so decreases performance of inserts, updates, and deletes.

 - Do Index the Primary and Unique Key Columns
 - Do Index the 1:1 and 1 side of 1:m Foreign Key Columns
 - Do Consider Using a Covering Index for Queries That Return Few Columns
 - Do Consider Using a Clustered Index for Large Tables and Range-of-Values Queries
 - Do Index Sorting, Grouping, and Aggregating Columns
 - Do Consider a DSS (decision support system to balance speed of query results plus speed of inserts, updates and deletes)
 - Don't Over-Index Transactional Tables with Heavy I/O Activity
 - Don't Index Wide Columns (to avoid a large number of data pages)

Index tuning isn’t something we do once a year. It’s something that we need to do iteratively– that means every month. Over time, data sizes change, user activity changes, and the SQL Server optimizer changes. Each of these things mean that indexes that are best for an application will also change. As we tune indexes, the query plans will change and it's very likely to see more opportunities to add, drop, and combine indexes emerge. Because of this, we want to do a few changes every month.

Sources:
 - [How to Master SQL Server Index Tuning in One Step](https://www.brentozar.com/archive/2013/08/how-to-master-sql-server-index-tuning/)
 - [Indexing Dos and Dont's](http://sqlmag.com/database-performance-tuning/indexing-dos-and-don-ts)