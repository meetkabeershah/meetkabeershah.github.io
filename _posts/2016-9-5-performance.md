---
layout: post
title: Indexes and Performance
---

![Performance](http://www.socialbullets.com/blog/wp-content/uploads/2014/08/Mobile-website-Performance.png)

[courtesy](http://www.socialbullets.com/blog/mobile-website-performance/)

# Storage Engines: Introduction

Okey, let's talk about sharding. Sharding is distributing database queries across multiple servers. Before we do that, let's get the idea of storage engines. New in `MongoDB` 3.0 is that they offer pluggable storage engines. A storage engine is the interface between the persistent storage, which will call the disks which might be a solid state disk, and the database itself.

![database talks to the persistent storage through a storage engine](https://lh3.googleusercontent.com/L6OeW3bF-IqdrJhk7qje_PLdfPgExIdmAZuTI1IGEqZ3ENb6rzZVGiSLWTLnw-sl656NqppFIf8RzythG3PQpMnXYY_InEaY92ulAyMEoXQbIWRdJS5IL09emKJEhXXYhGYg3AyX7h5DAoyN8jJ4grqbu_XeGG5R_QSK66I1ni3308EUuN57loWQGtyKuz0mdKbAQctB8nMQjVZwZ_5GqdN9SvNY0G32cGAfxtvaHhioPE5-h6cICRp6xofwW2Ob-3BhTprJmtCs_ZbC8Vnz7KbdmwT1Htv0Iio5mYmWJuXt6BrMoN7QcTR-lCmkfb6Tr64nVWCD1OJqfH2klKiQp3S8RG0lgPkJ_AoJK-wXMV1bnC9JoJtjrFLGo3YyYk4aFbXvp7BeRZD2YfVHXKIrVyHAOy1q_Ybf1bX0mZE_p14Hph7_TREbQjLbTH0amPIfYO7IJ1kAeNDEa4tSj1ffsetYtb3ip9rMoIYJgSBPeILOWow30UDtFkVPOY3_F-EMWX-x3c_a_4Ln0TtHxHkypetO0StsVGXh2aaltsccLDWuwixno20Zzubo9ent9VLKUfAhAEZ7sedqbXXDk5J2wG-nfvCVy-EMKLAiJtrBHlLf5pAS=w629-h323-no)

So, the database talks to the persistent storage through a storage engine. Now, it may be the case that the storage engine itself decides to use the memory to optimize the process. So, in other words disk is very slow. Since the idea of databases is to store stuff persistently, what happens is the storage engine has control of memory on the computer. And it can decide what to put in memory and what to take out of memory and what to persist to disk and when. So the database server itself defers the handling of the memory on the server as well as the disk itself to the store engine. `MongoDB` provides pluggable storage engine where we can use more than one. With different storage engines, we get different performance characteristics. For `MongoDB`, there're 2 storage engines shipped with:

 - MMAP - the older default storage engine
 - WiredTiger - it came into picture when [MongoDB](https://www.mongodb.com) acquired [WiredTiger](http://www.wiredtiger.com/) in 2014. The team had worked at [SleepyCat](https://en.wikipedia.org/wiki/Sleepycat_Software) and built [Barkeley DB](https://www.oracle.com/database/berkeley-db/db.html).

 **What a storage engine is not?**

If we have a bunch of `MongoDB` servers all running in a cluster, the storage engine doesn't affect the communication between those different `MongoDB` servers. The storage engine doesn't affect the API that the database presents to the programmer. The storage engine directly determines the data file format and format of indexes

# Storage Engines: MMAPv1

We call it MMAPv1 - the original storage engine of `MongoDB` because it internally uses the `mmap` call under the covers in order to implement storage management. Let's look at what the [MMAP](http://www.tutorialspoint.com/unix_system_calls/mmap.htm) system call looks like. On Linux, it talks about memory allocation, or mapping files or devices into memory. Causes the pages starting address and continuing for at most length bytes to be mapped from the object described by the file descriptor at an offset. So, what does that really practically mean?

Well, `MongoDB` practically needs a place to put documents. And it puts the documents inside files. And to do that it initially allocates, let's say a large file. Let's say it allocates a 100GB file on disk. So, we wind up with 100GB file on disk. The disk may or may not be physically contiguous on the actual disk, because there are some algorithms that occur beneath that layer that control the actual allocation of space on a disk. But from our point, it's a 100GB contiguous file. If `MongoDB` calls `mmap` system call, it can map this 100GB file into 100GB of virtual memory. To get this big virtual memory, we need to be on a x64 machine. And these are all [page-sized](http://www.computerhope.com/jargon/p/pagesize.htm). So pages on an OS or either 4k or 16k large. So, there is lot of them inside the 100GB virtual memory. And the operating system is going to decide what can fit in the memory. So, the actual physical memory of the box is let's say 32GB, then if we go to access one of the pages in this memory space, it may not be in memory at any given time. The operating system decides which of these pages are going to be in memory. We're showing the ones available in memory as green ones. So, when we go to read the document, if it hits a page that's in memory, then we get it. If it hits a page that's not in memory (the white ones), the OS has to bring it from the disk.

![Storage Engines: MMAPv1](https://lh3.googleusercontent.com/BWm46PHfwP2IKXbfUWzygkadOYh1vMQVNw-yoPATuLhYWsgLbfah6CDy5RE-1elidVeMsBilwePmodSkB8oH8aM8q3hYxzB853Gc9fATAfbI-R_1ZfvJyqda-hGJye2kng6mKIGetoDcTRY5UP0AnXGznVuC65alMFv5HY7I4xZJ0kp96cQr7nkZNN4PaZmkrATnyirp6BObK4yww9apLVPjh6EQQnFh0IuVWov5H890F0tet8nH-JZlXr8yJbW_wo5Uh6rm3JSwSFluR3fkn8lG3B0yvcYIZetj4yAVhEf8oilsMri7mgXvPW44ZsXj2pPtgLONQm41527tV129twENH2NOqzXnri5O-XgY-G27P3M03GvWWRyEJrtpkR-SQMhyph0FYsxEgpYk2FB1Kq6qJFv4M6DNo50cQtqR_8VoYO8xkWVB4eK5rESzvbFAqMdDCnqHZnTlp4FDzcjBs_4yGkpiyJPMN8he9hNIhOC0XPEhi2B2vo9KxtvojfSywZwlBJYAgCHbyQ9937gz-hG6FjbIWHmbMQPfzNysjIzVoI4AhjGsiknT0vDbG22jn4qmrPzkpYxrLbXLI7Lfr4koISUJcwuXhrEv787e_nCX2Ieg=w851-h466-no)

<sub>[source](https://www.youtube.com/watch?v=os3591KviNM)</sub>

MMAPv1 storage engine provides

 1. **Collection level concurrency (locking)**. Each collection inside `MongoDB` is it's own file (can be seen in `~\data\db`). If multiple `write`s are fired on the same collection, one has to wait for another to finish. It's a multiple reader. Only one write can happen at a time to a particular collection.
 2. **Allows in place updates**. So, if a document is sitting here in one of the available (green) page and we do an update to it, then we'll try to update it right in place. And if we can't update it, then what we'll do is we'll mark it as a whole, and then we'll move it somewhere else where there is some space. And finally we'll update it there. In order to make it possible that we update the document in place without having to move it, we uses
 3. **Power of 2 sizes** when we allocate the initial storage for a document. So, if we try to create a 3bytes document, we'll get 4bytes. 8bytes, if we create 7bytes. 32bytes when creating 19bytes document. In this way, it's possible to grow the document a little bit. And that space that opens up, that we can re-use it more easily.

 Also, notice that since, OS decides what is in memory and what is on disk - we cannot do much about it. The OS is smart enough for memory management.

# Storage Engines: WiredTiger

For a lot of workloads, it's faster. It provides

1. **document level concurrency**. We don't call it document level locking because it's a lock free implementation which has an optimistic concurrency model where the storage assumes that two writes are not going to be the same document, and if they are to the same document, then one of those is unwound and has to try again and it's invisible to the application. But we do get this document level concurrency versus collection level concurrency in the MMAP storage engine and that's a huge win.
2. **Support for compression** of both indexes and data. It's because WiredTiger is maging it's own storage.
3. **No inplace updates** - if we update, it's marked as ***no longer user*** and a new space allocation is done on disk and written there. Eventually, the vacant space is reclaimed. To invoke a WiredTiger storage engine, we would use `mongod --storageEngine wiredTiger`.

# Indexes

An index is an ordered set of things. An index in the database has ordered column(s) with their references (_ids or memory location). Ordered things are faster to search for. This is called b-tree indexes. The indexes works from the left most side. Let's assume that the index is on 3 columns: `A`,`B`, `C`. We can search rapidly from **left side** by
 - `A`,`B`, `C`
 - `A`, `B`
 - `A`

But to search from the right side is not supported by index. The following will not be speeded:
- `C`
- `B`
- etcetra

![index support](https://lh3.googleusercontent.com/vvXH6YnxhfM_X2l3duiE-Iu3-_l_KK07xmIW4JrFbHiQfzGX7UcJLJ3JcTbk_WJexAEHWKarTZnAI0JlWeS2ksEN1iZOfBMIJpn0Y278-MtX6VbEyfDDnOAFeha3dDNOTXtwc7o3Fge2CqkVD3WjblUgQeJOmzv58-vy1lJvzfNEN2HoK8ikSkSlf5VHB2DqkuSS9vTCQJ5ucrTJfuhOBRP5MNLNi8sQYL5jLWvgQ4cbaOEuB5Vw5RR4-Vyr253T26OGDiQ8Ij4uBB1lL1aNb2dWcxsE2IdPFVr2aGu_vlDzMelPFaf4T3Vily0YlIUIfvScGS2ap_g2p3_N1RglXQPo5cJTg1cqh92IIcF0j5L7YiwXn18IMPwEjeqIN4GPMUvDbnyqKFiZAmppq6wHKgWLioknddLqxGPb3s3hP4QOMzOHhFSfaLsWu7cQCoyeoWH3HmfHqHxd5n3_jdio-dfWA2w9N6VSxDzr21nFdXMCXQxbVbcfLj1AIUEp1n-lYaK40g8OnUbrs0GTd3LpGJKmM5GycpzGQ47aJVnr8oz3P0CR0GPCddSEjJYHdEVZxZ1xi-0ohQtJzVGd-XjPuY1AenA_8IIrvtI9nZ6QD_lV0Izx=w148-h194-no)

Indexing is not free because whenever we change anything in the document which affects the index, we're going to have to update the index. It needs to be written on memory and finally on disk. Also, it's nice to know that indexing slows down the writes. Yes, the reads are faster. Creating indexes also takes time even on fast computers, because we have to scan the entire collection. Create new data structures and write them all to disk.

To create a compound index use command `db.collectionName.createIndex({A: 1, B: -1})`. Where `1` means ascending, -1 means descending. To drop the index, use `db.collectionName.dropIndex({A: 1, B: -1})`. Compound indexes cannot have both the columns with array types. If we try to do this, `MongoDB` will tell that it can't index parallel arrays and the reason is that there's an explosion of index points that create it because it has to create index points for the cartesian product of the items in the array and it doesn't permit that. **Multikey indexes** are applied when we have arrays inside documents on indexed keys. To get the currently available indexes, use command `db.collectionName.getIndexes()`. The nested keys can also be indexed, e.g.: `db.collectionName.createIndex({'A.aa': 1})`. Where, `aa` is a sub-key inside key `A`.

# Index Creation Option, Unique

Let's create a collection with duplicate entries:

<pre><code>
db.collectionName.insertOne(thing: 'apple');
db.collectionName.insertOne(thing: 'pear');
db.collectionName.insertOne(thing: 'apple');
</code></pre>

To make sure that the entries are unique, we can apply a unique index. To create a unique index, use `db.collectionName.createIndex({thing:1}, {unique:true})`. This command will give an error because there're multiple apples in the `collectionName`. To remove one, use command `db.collectionName.remove( {thing:'apple'}, {justOne: true} )`.

After this index is in place, any attempts for duplicate inserts will result in `duplicate key error`. To see whether the index is indeed created, use command `db.collectionName.getIndexes()`. One interesting thing to notice is that the index on `_id` is shown as **unique**, although it is.

# Index Creation, Sparse

<pre><code>
{a:1, b:5, c:2}
{a:8, b:15, c:7}
{a:4, b:7}
{a:3, b:10}
</code></pre>

Let's assume that we wish to create an index on the above documents. Creating index on `a` & `b` will not be a problem. But what if we need to create an index on `c`. The unique constraint will not work for `c` keys because **null value is duplicated** for 2 documents. The solution in this case is to use `sparse` option. This option tells the database to not include the documents which misses the key. The command in concern is `db.collectionName.createIndex({thing:1}, {unique:true, sparse:true})`. The sparse index lets us use less space as well.

>Notice that even if we have a `sparse` index, the database performs all documents scan especially when doing sort. This can be seen in the **winning plan** section of `explain`'s result.

# Index Creation, Background

There are multiple indexing options - foreground (default) & background. Foreground is relatively fast and it blocks all writers and readers. Other databases we can still get to. This is supposed to be not done in a production environment.

Background index creation is a bit slower and they don't block readers and writers. With `MongoDB` 2.4 and later, you can create multiple background indexes in parallel even on the same database.

Beginning in `MongoDB` 2.6, creating an index in the background on the primary will cause the indexes to be created in the background on secondaries, as well. The secondaries will begin index creation when the primary completes building its index.

There is another way to create index very efficiently in a production system. That is to create an index on a different server that is being used to serve most queries. Say, in a replica set of multiple database servers working in tandem, one can be taken out and the requests can be routed to the available ones. The foreground index creation can be done on the separated server. After the creation is done successfully, it can be brought back to the cluster.

# Using Explain

The `explain` command shows what action the database takes in executing a query. It returns an explainable object. What indexes it uses, how many documents are scanned. It does almost everything similar to what the actual query would do, but it's not the entire simulation of the query. This command can be used bith from a shell as well as from the driver. It can be used in multiple cases:

 - `db.collectionName.explain().find()`
 - `db.collectionName.explain().update()`
 - `db.collectionName.explain().remove()`
 - `db.collectionName.explain().aggregate()`

 But the following is not allowed:

 - `db.collectionName.explain().insert()`
 - `db.collectionName.remove({a:1, b:2}).exlain()`

To find out which functions can be used in conjunction with `explain`, use `db.collectionName.explain().help()`. In previous versions, it was possible to append this command at last on a cursor (remember that `find()` returns a cursor). e.g.: `db.collectionName.find().explain()`. This was changed to be pre-pended by an explainable object's function. The reason is not all methods return a cursor. e.g.: `count()` will return a scalar.

# Explain: Verbosity

The `explain` command can run in 3 modes:

 - `queryPlanner` - tells mostly what the database would use in terms of indexes
 - `executionStats` - includes the `queryPlanner` mode, also includes what the result of using the indexes will be
 - `allPlansExecution` - includes the `queryPlanner` & `executionStats` mode. It does what the query optimizer does periodically is it runs all the possible indexes that could be used for a particular shape of query, and it runs them in parallel. Then makes a decision about which one is fastest.

<pre><code>
var exp = db.collectionName.explain("executionStats");
exp.find();
</code></pre>

One thing to understand when studying the performance stats is to see the number of returned documents (`nReturned`) and number of documents examined (`docsExamined`). The following data says that The query scanned 999,999 documents, returning 10,000 in 619 milliseconds.

<pre><code>
> exp = db.example.explain("executionStats")
Explainable(test.example)
> exp.find( { a : 7 } )
{
    "queryPlanner" : {
        "plannerVersion" : 1,
        "namespace" : "test.example",
        "indexFilterSet" : false,
        "parsedQuery" : {
            "a" : {
                "$eq" : 7
            }
        },
        "winningPlan" : {
            "stage" : "COLLSCAN",
            "filter" : {
                "a" : {
                    "$eq" : 7
                }
            },
            "direction" : "forward"
        },
        "rejectedPlans" : [ ]
    },
    "executionStats" : {
        "executionSuccess" : true,
        "nReturned" : 10000,
        "executionTimeMillis" : 619,
        "totalKeysExamined" : 0,
        "totalDocsExamined" : 999999,
        "executionStages" : {
            "stage" : "COLLSCAN",
            "filter" : {
                "a" : {
                    "$eq" : 7
                }
            },
            "nReturned" : 10000,
            "executionTimeMillisEstimate" : 520,
            "works" : 1000001,
            "advanced" : 10000,
            "needTime" : 990000,
            "needFetch" : 0,
            "saveState" : 7812,
            "restoreState" : 7812,
            "isEOF" : 1,
            "invalidates" : 0,
            "direction" : "forward",
            "docsExamined" : 999999
        }
    },
    "serverInfo" : {
        "host" : "cross-mb-air.local",
        "port" : 27017,
        "version" : "3.0.1",
        "gitVersion" : "534b5a3f9d10f00cd27737fbcd951032248b5952"
    },
    "ok" : 1
}
</code></pre>

# Covered Queries

Covered query is a query, which can entirely be satisfied by an index. Hence, **zero documents needs to be inspected** to satisfy the query. This makes the query a lot faster. All the projection keys needs to be indexed.

# How Large is the Index?  

Like any other database, it's important to keep **"working set"** in the **memory**. Working set is the data that is frequently being access by the client. This is especially true for indexes. If the index is in the disk, taking it from there for every query is very expensive. Estimating the amount of memory we'll need for a `MongoDB` deployment. This can be found by using command `db.collectionName.stats()`, below is the output in concern:

![size of the index](https://lh3.googleusercontent.com/zyB0RAbjaPn7PnjYOM4WLQE4IottvN6nu6DOaeEl1VS9szoX9M9wb6LqJvfD84rp57tHT2y79LX2gVPu9FW8-fIq5PtSGTMq6zZPRtnXgiHVjOSnqdenXupuBttVx5hc8M4JDzJNEKrIYLQ1uwchFrMz5AITbLRXjJtrTVN_JK_hNbXl6zjGbQEc0jTDGLGEZqT_H26Fsv6eV37WJNQQ6n6i0yICect8CD0EuFBwJBB7PzZrAMiAoZCx5MHPnEDWwPGWVnncDp8H296TpEAHzXAAA3SqoMOa0EoilPieTO8t81A6x062l56OSqs-dBGWDzIFJpLnOwDQ4aFAF8ifXSm8BnZQpn52ijBoGj5ohYJKNLYtc4CGcZ_Br_I5ba3rZoYkj3QTzdvMGKZT8UiI_5ix8Z-zcBsFI4Z_MdI-QxCWlL_qbSbJ_Gtl5LrrQyGWSCTbZ3HZsGWTwLhoNgVWGhhdHAahyCGqfoYSREMZ2CSuLuhwLaDaRw45QPYQcD4ItI1p5wmkdV6UG-P78j6LeUqCSMy-1rCqNe5gdMCHEx6YeuoWc4aSibJJIjCJGGHoh50MYhFcSEKBmd93ch_UW9VEW2pBBHPtvEde1vYung8NZ462=w294-h65-no)

This output changes from one database engine to another. There's also a shortcut `db.collectionName.totalIndexSize()` which gives the required size detail. With WiredTiger storage engine, the sizes of the indexes is much smaller because it supports a technology called prefix compression. But this compression comes at the cost of CPU. The moral of the story is that, we need to always make sure that the index fits into the working set and which in turn needs to fit in the memory.

![index in memory](https://lh3.googleusercontent.com/4NkueuMMGHBCSeMx_gJ07HiRciBPeJfX8032Ccs8KKYFI5JUazpDSBWlkS3wPN7dEtxO9JTbKexpljU-MOq5YBlcge7ElW4nOz94DgI5smktNIo9U26E4Ncnzd_BC_sSU3lbnCqNJ6-zGDZxH8ZF6Wx11pUj3loTGfJkitlaG-7k5sOWj-yrycLBGSgKaIvJ3TjtZmfTHasqM2OLtuf8zIMaV8ABmwoeOagOoHlS2PERW-2b1lG07uQhEp9cSP3d5ytGYcF4FgNKCUoezqPoExh7C39njtvmH0EYlo2cK1DUL-IwqC-1J6hR572hjFumDrtmUfzJpzDS_45qFku9Qv1aYmOiBVJQMxsB7kJ0A0seYEjsq9WsKW06YTWtOtgxMJyTNDqDnAHCOCIGT2ETUSNdc4gm_7LqoIXrjhsASmKT1vo2u0-3yH3GwuiSVisdy8h1nJwvaOoekwSUqGIjDREw320OiLSkbQAMlry8zbZir-tbGRO2XcEoHwipWESW9qR_zJtq0kP7w1NjsWA-pWGo9kKH7FoqYGaPxm6YhHiEXmx1VgElcId1-N2PK7AOVVjs4bLrtB1OjeyFvRIpM1OXEavtGh046h9dbCzYAtWPwYi2=w534-h353-no)

# Number of Index Entries

**Index cardinality:** it refers to the number of index points for each different type of index that `MongoDB` supports.

 1. Regular - for every single key that we put in the index, there's certainly going to be an index point. And in addition, if there is no key, then there's going to be an index point under the null entry. We get 1:1 relative to the number of documents in the collection in terms of index cardinality. That makes the index a certain size. It's proportional to the collection size in terms of it's end pointers to documents
 2. Sparse - when a document is missing a key being indexed, it's not in the index because it's a null and we don't keep nulls in the index for a sparse index. We're going to have index points that could be potentially less than or equal to the number of documents.  
 3. Multikey - this is an index on array values. There'll be multiple index points (for each element of the array) for each document. So, it'll be greater than the number of documents.

![number of index points](https://lh3.googleusercontent.com/eudDYcP4vzZT1LzgUk6E_xXn6znq_DAe5dvs4NpNbxK-J38s3KQDIiPBegredK3-EnHkknn51SEsOPbmzmWx7TVDw7w9tjfRVUCtzQhqzxSS2rDTCAfnSnn8X-WySkCXFBN0P7D_0K6U629ev9wKN5t5UXZMngiZt8rzsTs3mxSYSK4xMXxOP29Ypr9i9EbKkRwueovKNY6pWaafl2d98G0jz2VVZuwgRNfdZuzBJWz41VDWrzeYp51Or4uPIbOSgaN3-Am6Kk1qLH1NqLgrvQjHRf02Dv3x_p6HTH8sAylcWxaP_pCE6h4zJX5j6TMH-8--sJpM__9uxipeEB6RHGDkxfqdTJUGZcABgkNx6A3BZ_SVfjh9S_MTbYM8PBLNCZdkgtMaioG4JSbR3Gbj7jF_07Gdh0kpJRR3y3ht0c-1HjvF_6l5zJySb4c7sWvNT-9qKbyXZWRkMsqNPBaLGKHFBbmAQs4rMjtCeRp0nyo6r4p2kO67GlCKIGOAtKVkD0idB5AMJnqnuvHvu7TSi6MGmPt6PnbgTFsQOl81xKEFByij5EoriaAcKv3lO9901paMBeII-ohwCrBl5kPxKxpX57tSqNf2VF3kIzS0Slxo3NDm=w390-h111-no)

Let's say you update a document with a key called tags and that update causes the document to need to get moved on disk. Assume you are using the MMAPv1 storage engine. If the document has 100 tags in it, and if the tags array is indexed with a multikey index, 100 index points need to be updated in the index to accommodate the move?

# Geospatial Indexes

These indexes allow us to find things based on location. We've 2 options: **2D** & **3D**
 In 2-D, we've a cartesian plane with `x` & `y` coordinates and a bunch of different objects.

 ![2D cartesian plane](https://lh3.googleusercontent.com/k5A_aF5PPl21Fbuoaz3qWkzVcwyBwc_xf5a7avN0oPPr9cM61hhRxUukKWI0GSq1GxkDBv5AxmHcnIypBC4hdpexqfS4sBIvCPyJnAXdT43BOR-dG4Nn4cY9abe4yYr75m56YrmdSNKuzGhcfgzT5AGr-rhhW5oHFCY3A2NARdj6nb_f9fmSohl8kgnIK2Gho9f-CEO7gOOJY_8_qqh-QlsHz4F3FnOufyQK0wus5SLkgGGUictf_M6cJ7Lbx5E7IWWCiW29F2QDR444g_y-CSWHixt0I3AduGU6aGO4mGsjYwyPhW5UAHniM7tyB7iz35zqIdDeIH_KXDLNR-75jIuNvf0TA5Hmr4mYhmfYpkJ9WDf5djKrd_NFK2yOF-at7OL38VOLoJyHRUbXrH-4QwP1__ueXHUmolD_AfnU9wLUejWeSZNPhD3Yj_kXqB3QH67epwu67zAp0WZXzUXxyfL9FXOjzA2gd1-3A_cgdB2F-k-OMPFIC10MBxekpUCs3xSMBbf8r5Vm2tiHwj_wc_QsDEUMWSg7BAvmJAo404sBOJL9U-I64WwEP-m35nBNNcTLREKnHkb1wK1XWn9yJxHjXGI-U_OBE8QChxWIP4V_GD-l=w629-h323-no)

The document needs to store some sort of `x`,`y` location with `createIndex({'location':'2d', 'type':1})`. The type option specifies the direction of the index i.e. ascending or descending (and it's optional). It can be a compound index. To find near locations use command `db.collectionName.find({location: {$near:[x,y]}})`. And practically speaking, the way this is often used is through a `limit`. To limit the results to 20 append `.limit(20)`.

# Geospatial Spherical

The location on the globe are represented using longitude and latitude. Latitude is how far off the equator is. Equator is at zero degrees latitude. We can go from **-90** to **90**. A special type of index called 2d sphere. To specify location of things, we use [GeoJSON](http://geojson.org/geojson-spec.html#examples). The locations can be described using a point or a polygon. The `type` & `coordinates` are reserved words. The values for `type` are reserved words. For this type of data, the indexing will be done using  `createIndex({'location':'2dsphere', 'type':1})`

For collection named "stores" to return the stores that are within 1,000,000 meters of the location latitude=39, longitude=-130? Assuming the stores collection has a 2dsphere index on "loc". Each store record looks like this:

<pre><code>
{
    "_id":{
        "$oid":"535471aaf28b4d8ee1e1c86f"
    },
    "store_id":8,
    "loc":{
        "type":"Point",
        "coordinates":[
            -37.47891236119904,
            4.488667018711567
        ]
    }
}
</code></pre>

The query will be `db.stores.find({ loc:{ $near: { $geometry: { type: "Point", coordinates: [-130, 39]}, $maxDistance:1000000 } } })`.

# Text Indexes

To create a text based index on a key, use command `db.collectionName.ensureIndex({'textColumnName': 'text'})`. After this index is applied, use the search commands to search for a word i.e. `db.collectionName.find({$text: {$search:'your text here'}})`. There is a text score based on which the results are ranked, to see it project it in the score key like this : `db.collectionName.find({$text: {$search:'your text here'}}, {score: {$meta: 'textScore'}}).sort({score: {$meta: 'textScore'}})`.

If we create a text index on the `title` field of the `movies` collection, and then perform the text search `db.movies.find( { $text : { $search : "Big Lebowski" } } )`. The following documents will be returned, assuming they are in the movies collection:

 - `{ "title" : "The Big Lebowski" , star: "Jeff Bridges" }`

 - `{ "title" : "Big" , star : "Tom Hanks" }`

 - `{ "title" : "Big Fish" , star: "Ewan McGregor" }`

This is because, there will be a ***logical OR***ing on `Big` & `Lebowski`.

# When is an Index Used?

Say, `MongoDB` gets a query in. Assume that it has the following indexes:

 1. `b`,`c`
 2. `c`,`b`
 3. `d`,`e`
 4. `e`,`f`
 5. `a`,`b`,`c`

`MongoDB` based on the shape of the query, index selection for executing the query is decided. Let's say **1**, **2** & **5** are selected. Then the execution plan is executed in parallel, with these indexes:

![index race](https://lh3.googleusercontent.com/TC8NKAMt_QZUOwQqV-WNcgzTL6Vaar9k8vHxenzpNt1D3hmHZljixBDI5mFEUQExU5WfYTEkyXFM2gTPfhLRdSabFQNFMWaS5hGmNsk1eqP1wSYP5aM8hHdLDhQ1uVzYUYjpzT1TYkKDykSFFBKdTP1xBBp6Dr5dve6SfGld15bHfupYYYhCZr-f8dJUoI-kMoWYCa-6LPWSqQWGz40IEMd9CGzMIAPz8iyOPmb4JvkABdEC1wXfteX7FeWJVQJlArPxHcCMIrfcirc9AFmpagn7kkkxt9yXVlNjAKuAx9arf0v_IRvbfci1kGvzpQnffWD-zgDMXeq5llbqusTfBwWNuepm_y3bHSvG4zUObgajbudQxwR5Kn26jeIG11DtjXHk1cDQ3EJLsWpsCb23w_wAf96dNEk1o9erVmDSuuii8kBRS3mRCJqFj7-yz78lYV14wD22ORjZGeUb3Hfp9eLX8j-CDUb7zTAroVkBKWmfOTsSmgUrXvUAtllCxK3X17Uvndx2jAyn22qYdlg34twWYe9srmqC-kGjds8Oa5pNhSZPVqUTK_Ij9zvS-EUDSbFK7oT_xj2uzd9R-uV6w9X1EjuTj4zEZ0V9JDwSZJhGr4C5=w489-h305-no)

The one with fastest results for all plans or sorted threshold results wins. This index is cached and used for similar queries in future. This cached index is removed from the cache when the threshold writes happens on the collection, which is 1000 writes as of this writing. If indexes are rebuilt, then also this caching is restructured. Or if the `mongod` process is restarted, this indexing information is removed from the cache.

# Designing / using Indexes

Like for doing anything greater, designing indexes requires some forward thinking. The goal is:

 - Efficiency - fast read / write operations
 - Selectivity - minimize records scanning
 - Other requirements - e.g. how are sorts handled?

Selectivity is the primary factor that determines how efficiently an index can be used. Ideally, the index enables us to select only those records required to complete the result set, without the need to scan a substantially larger number of index keys (or documents) in order to complete the query. Selectivity determines how many records any subsequent operations must work with. Fewer records means less execution time.

Think about what queries will be used most frequently by the application. Use `explain` command and specifically see the `executionStats`:

 - `nReturned`
 - `totalKeysExamined` - if the number of keys examined very large than the returned documents? We need some index to reduce it.

Look at `queryPlanner`, `rejectedPlans`. Look at `winningPlan` which shows the `keyPattern` which shows which keys needed to indexed. Whenever we see `stage:SORT`, it means that the key to sort is not part of the index or the database was not able to sort documents based on the sort order specified in the database. And needed to perform in-memory sort. If we add the key based on which the sort happens, we will see that the `winningPlan`'s' `stage` changes from `SORT` to `FETCH`. The keys in the index needs to be specified based on the range of the data for them. e.g.: the **class** will have lesser volume than **student**. Doing this needs us to have a trade-off. Although the `executionTimeMillis` will be very less but the `docsExamined` and `keysExamined` will be relatively a **little** large. But this trade-off is worth making.

There is also a way to force queries to use a particular index but this is ***not recommended to be a part of deployment***. The command in concern is the `.hint()` which can be chained after `find` or `sort` for sorting etc. It requires the actual index name or the shape of the index.

In general, when building compound indexes for:
 - **equality field**: field on which queries will perform an equality test
 - **sort field**: field on which queries will specify a sort
 - **range field**: field on which queries perform a range test

The following rules of thumb should we keep in mind:

 - Equality fields before range fields
 - Sort fields before range fields
 - Equality fields before sort fields

`MongoDB` automatically logs slow queries with 100+ ms execution.

# Profiling

`MongoDB` has a sophisticated feature of profiling. The logging happens in `system.profile` collection. The logs can be seen from `db.system.profile.find()`. There are 3 logging levels:

 - Level 0 - no logging
 - Level 1 - logs slow queries
 - Level 2 - log all queries, this is much of a debugging feature rather than a performance debugging option

To see what profiling level the database is running in, use `db.getProfilingLevel()` and to see the status `db.getProfilingStatus()`. To change the profiling status, use the command `db.setProfilingLevel(level, milliseconds)` - where `level` refers to the profiling level and `milliseconds` is the ms of which duration the queries needs to be logged. To turn off the logging, use `db.setProfilingLevel(0)`.

The query to look in the system profile collection for all queries that took longer than one second, ordered by timestamp descending will be `db.system.profile.find( { millis : { $gt:1000 } } ).sort( { ts : -1 } )`.

# Mongotop

For performance tuning, we have seen `explain`, `hint` and `profile` options. But what if we want to look at the high level inside a program and figure out where it's spending it's time, how would we do that? We've `Mongotop`, named after `Unix` command `top`. To see the log on the shell use command `mongotop seconds` - where `seconds` is the number of seconds after which the next log entry shall be printed.

e.g.: `mongotop 3`

# Mongostat

`Mongostat` is similar to `iostat` command from the `Unix`. It gives the database stats in the intervals of 1 seconds. It shows what operations happened during that 1 second. Output may vary depending upon what storage engine is being used. The results of it also shows `getmore` is how many `getmore` command we're running every seconds. It's the way we get more from a cursor, if we're doing a query that has a large result. The getmore column concerns the number of requests per time interval to get additional data from a cursor. `command` shows the number of commands running per second. `flushes` refers to the number of times the disk is flushed out per second. `mapped` is the amount of mapped memory. `res` refers to the resident memory. `faults` refers to the number of page faults that we're causing every second. It's an important number because page faults mean we're getting more I/O and more I/O means slower database. `qr` and `qw` are the queues length for a number of sockets that are requested or waiting for read and write. `ar` and `aw` are the number of active readers and writers. `netIn` & `netOut` refers to the amount that was sent into and out of the database during this time frame. `dirty` refers to the amount of cache `WiredTiger` storage engine has written to and needs to be written back to the disk. `used` is the total cache size we're using.  

# Sharding

Sharding is a technique of splitting up a large collection amongst multiple servers. When we shard, we deploy multiple `mongod` servers. And in the front, `mongos` which is a router. The application talks to this router. This router then talks to various servers, the `mongod`s. The application and the `mongos` are usually co-located on the same server. We can have multiple `mongos` services running on the same machine. It's also recommended to keep set of multiple `mongod`s (together called **replica set**), instead of one single `mongod` on each server. A replica set keeps the data in sync across several different instances so that if one of them goes down, we won't lose any data. Logically, each replica set can be seen as a **shard**. It's transparent to the application, the way `MongoDB` chooses to shard is we choose a **shard key**.

![MongoDB sharding](https://lh3.googleusercontent.com/8mQlJAlaLupNLIIPzjRAowZ2tiMx_EHE54Ssvf_Ph2bp553MLZ6Xsf_Qz6dUDW6zsX2Cb2etBt1hi-_OHW8dNOfj-A6tm3i8dLcq5dj_1B-ZeO6qJuAKLwaq9IoCdiwIz-VndrxHJ0h7A8sXhlxIathRNf2Bj8qrWiaAZpgfOWfznV84IKmxIKYPMgpW2ooAEU41cMNoYSUhlzih64qKgrWm0gGfFBnvaLIqHFIGuLwkMHBkp2QwqUE_uT9NWGS2HV9fZMqMdADZzGWRZu_GNmn0Gw9kmlfrcZfO355tT1wzI37fET-GlnDiVFEhZLa02MUiNewPihV-PkqxK3OpsGUthcZMmY-YwerOr2V-uUiNoh7wdhQjpYf5aA7ygkvcqxtNH6fs7vHsn7KqFjBV_JlWnSZo4cM_USqmW1jjpG00WNEYu_z0S_8n1RNg7BDT7ALzlVI6ceq0QtyV_2VbK-UrgZSoNRRyWgO2fghuIdDBnevSN3sgEJNVQo1gfzlQdHamSkab56jGQNsWr5DBxVQUUveXUtMJ2U-a4ly3a1ufuO09FHWuPM5apwLmspPnz6vxWjqCJgWoE_-gtXlv1hW-LsxyP6nqP0NVCyh_XXZjp86-=w1354-h624-no)

Assume, for `student` collection we have `stdt_id` as the shard key or it could be a compound key. And the `mongos` server, it's a range based system. So based on the `stdt_id` that we send as the shard key, it'll send the request to the right `mongod` instance.

**So, what do we need to really know as a developer?**

 - `insert` must include a shard key, so if it's a multi-parted shard key, we must include the entire shard key
 - we've to understand what the shard key is on collection itself
 - for an `update`, `remove`, `find` - if `mongos` is not given a shard key - then it's going to have to broadcast the request to all the different shards that cover the collection.
 - for an `update` - if we don't specify the entire shard key, we have to make it a multi update so that it knows that it needs to broadcast it

[Photos](https://goo.gl/photos/Zap9QDfK48bqssgd6)
