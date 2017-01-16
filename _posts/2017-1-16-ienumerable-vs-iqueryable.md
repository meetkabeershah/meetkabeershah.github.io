---
layout: post
title: IEnumerable VS IQueryable
---

The difference between IEnumerable VS IQueryable is:

<table>
<tr>
<th>
IEnumerable
</th>
<th>
IQueryable
</th>
</tr>

<tr>
<td>
exists in System.Collections Namespace
</td>
<td>
exists in System.Linq Namespace
</td>
</tr>

<tr>
<td>
can move forward only over a collection, it can’t move backward and between the items
</td>
<td>
can move forward only over a collection, it can’t move backward and between the items
</td>
</tr>

<tr>
<td>
best to query data from in-memory collections like List, Array etc
</td>
<td>
best to query data from out-memory (like remote database, service) collections
</td>
</tr>

<tr>
<td>
While query data from database, IEnumerable execute select query on server side, load data in-memory on client side and then filter data
</td>
<td>
While query data from database, IQueryable execute select query on server side with all filters
</td>
</tr>

<tr>
<td>
suitable for LINQ to Object and LINQ to XML queries
</td>
<td>
suitable for LINQ to SQL queries
</td>
</tr>

<tr>
<td>
supports deferred execution
</td>
<td>
supports deferred execution
</td>
</tr>

<tr>
<td>
doesn’t supports custom query
</td>
<td>
supports custom query using CreateQuery and Execute methods
</td>
</tr>

<tr>
<td>
doesn’t support lazy loading. Hence not suitable for paging like scenarios
</td>
<td>
support lazy loading. Hence it is suitable for paging like scenarios
</td>
</tr>

<tr>
<td>
methods supports by IEnumerable takes functional objects
</td>
<td>
IQueryable takes expression objects means expression tree
</td>
</tr>

<tr>
<td>
<pre>
<code>
MyDataContext dc = new MyDataContext ();
IEnumerable<Employee> list = dc.Employees.Where(p => p.Name.StartsWith("S"));
list = list.Take<Employee>(10);
</code>
</pre>
</td>
<td>
<pre>
<code>
MyDataContext dc = new MyDataContext ();
IQueryable<Employee> list = dc.Employees.Where(p => p.Name.StartsWith("S"));
list = list.Take<Employee>(10); 
</code>
</pre>
</td>
</tr>

<tr>
<td>
<pre>
<code>
SELECT [t0].[EmpID], [t0].[EmpName], [t0].[Salary] FROM [Employee] AS [t0]
WHERE [t0].[EmpName] LIKE @p0
</code>
</pre>

Notice that in this query "top 10" is missing since IEnumerable filters records on client side
</td>
<td>
<pre>
<code>
SELECT TOP 10 [t0].[EmpID], [t0].[EmpName], [t0].[Salary] FROM [Employee] AS [t0]
WHERE [t0].[EmpName] LIKE @p0
</code>
</pre>

Notice that in this query "top 10" is exist since IQueryable executes query in SQL server with all filters.
</td>
</tr>

</table>

[Source](http://www.dotnettricks.com/learn/linq/ienumerable-vs-iqueryable)
