---
layout: post
title: BlitzKrieg SQL Server diagnosis
---

![BlitzKrieg](https://s-media-cache-ak0.pinimg.com/736x/25/fc/94/25fc94b2bd5c96e67912534644f3856e.jpg)

[courtesy](https://www.pinterest.com/pin/253749760225683004/)

Found a few cool tools for disgnosing the SQL Server issues. Here is the share for you:

# Using sp_BlitzCache to Find Your Worst-Performing Queries

<code>sp_BlitzCache</code> is [a free tool](https://www.brentozar.com/blitzcache/) that help analyze which queries are consuming most resources like CPU, disk, time etc.

To learn about this tool, use the help parameter <code>sp_BlitzCache @help=1</code>
When ran without parameters, it returns top 10 most CPU expensive queries: <code>sp_BlitzCache</code>

It results in all the diagnosis information like which database and stored procedures are taking the most time. It has a column named <code>Query Plan</code> which links to the actual execution plan. This execution can be shared through [pastetheplan.com](https://www.brentozar.com/pastetheplan/)

To narrow down the results to a single database use the parameter <code>sp_BlitzCache @DatabaseName='DBName'</code>

To sort the results by number of reads, pass the <code>SortOrder</code> parameter <code>sp_BlitzCache @SortOrder='reads'</code>. Other options include CPU, duration, executions, XPM, memory grant, or recent compilations.

To limit the number of results use the <code>@Top</code> parameter. Remember that the more queries you analyze, the slower it goes <code>sp_BlitzCache @DatabaseName='DBName', @Top=50 </code>

To do an expert level analysis and see more info, use <code>@ExpertMode</code> parameter <code>sp_BlitzCache @ExpertMode = 1 </code>

For an export to excel friendly result, use <code>@ExportToExcel</code> parameter <code>sp_BlitzCache @ExportToExcel = 1 </code>

To write the results to a separate database, use the new db entity parameters <code>sp_BlitzCache @OutputDatabaseName = 'NewDB', @OutputSchemaName = 'dbo',  @OutputTableName = 'OutputTable' </code>

# sp_Blitz – Free SQL Server Health Check Script

<code>sp_Blitz</code> is an easy to use [free simple health check tool](https://www.brentozar.com/blitz/) for SQL Server. Shows stuff like non-backuped databases etc.

To learn about this tool, use the help parameter <code>sp_Blitz @help=1</code>

When executed without parameters, gives the list of suspicous things. Notice that issues upto priority **50** are urgent issues. So to see only the urgent issues use the priorities parmeter <code>sp_Blitz @IgnorePrioritiesAbove = 50</code>

Writing the results is also possible like this <code>sp_Blitz @OutputDatabaseName = 'DBName', @OutputSchemaName = 'dbo' , @OutputTableName = 'SomeTable'</code>

# sp_BlitzFirst Helps Troubleshoot Slow SQL Servers

<code> sp_BlitzFirst </code> when executed on it's own gives all the stuff which are causing the server to run slow like ongoing backup execution, high CPU utilization.

To see the detiled wait stats use the expert mode <code> sp_BlitzFirst @ExpertMode = 1 </code> and gives 3 resultsets:

 - Result set 1 : queries currently executing
 - Result set 2 : the troubleshooting info like that of without any params
 - Result set 3 : WAIT STATS (read below for the description of the same)
 - Result set 4 : FILE STATS (read and write speeds for each database file – both data and log file)
 - Result set 5 : Perfmon counters (statistics from the [performance monitor](http://xameeramir.github.io/Setting-Up-Perfmon-for-SQL-Server-Tuning/))
 - Last result set : gives the currently executing queries

To see the results since SQL Server started, use since startup param <code> sp_BlitzFirst @SinceStartup = 1 </code>

The results can be stored in an output database as well.

# sp_BlitzIndex – SQL Server’s Index Sanity Test

To run the index tests on all of the databases on the server use the parameter <code> @GetAllDatabases = 1 </code> like so <code> sp_BlitzIndex @GetAllDatabases = 1 </code>

If you’ve got more than 50 databases on the server, this only works if you also pass in @BringThePain = 1, because it’s gonna be slow.

To get the database specific details set mode to 4 as <code> sp_BlitzIndex @Mode = 4 </code>

# WAIT STATS

Whenever SQL Server is running queries, it’s tracking how much time it spends waiting on bottlenecks. These wait statistics are the easiest way to identify your bottleneck and in general called **wait stats** or **waits and queues**.

These statistics are tracked automatically in every version/edition of SQL Server, and they’re easy to query.

[Source](https://github.com/BrentOzarULTD/SQL-Server-First-Responder-Kit)
