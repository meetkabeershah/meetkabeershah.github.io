---
layout: post
title: MongoDB schema design
---

![MongoDB schema design](http://files.pdfsr.com/data/screenshot/MongoDB-Schema-Design-Presentation-Transcript-13756.jpg)

[courtesy](http://pdfsr.com/pdf/mongodb-schema-design)

Notes for 4th week of [`MongoDB` for `node.js` course](https://university.mongodb.com/courses/MongoDB/M101JS/2016_August/)

# Schema Design

There is an ideal way to design databases in relational databases - 3rd normal form. In `MongoDB`, it's important to keep data in way that's conducive to the application using the data. You think about

 - application data patterns
 - what pieces of data are used together
 - what pieces of data are used mostly read-only
 - what pieces of data are written all the time

In contrast, in relational DBMS - the data is organized in such a way that is agnostic to the application.

`MongoDB` supports **rich documents**. We can store an array of items, a value for a certain key can be an entire other document. This is going to allow us to **pre-join/embed data** for fast access. And that's important because **`MongoDB` doesn't support joins directly** inside the kernel. Instead if we need to join, we need to join in the application itself. The reason being *joins are very hard to scale*. This forces us to ***think ahead of time about what data you want to use together with other data***. We might wish to embed the data directly within the document. There're **no constraints**. In case of `MongoDB`, it's as important as we think because of embedding. `MongoDB` considers **atomicity** in a way. Also it **doesn't support transactions**, however **atomic operations** are supported within one document. The data needs to be designed in such a way that it supports atomic operations.

There's **no declared schema** but there's a good chance that an application is going to have a schema. By having a schema, we mean that every single document in a particular collection is probably going to have a pretty similar structure. There might be small changes to that structure depending on the different versions of your application. Even though it's not declared ahead of time, it's important to think about the data structure so that the data schema itself supports all the different features of your application  

# Relational Normalization

Let's look at the below denormalized table for a blog posts project. It's not the 3rd normal form, it's broken. Let's say there are multiple
posts with same author, we may update a few rows and leave others un-updated. Leaving the table data inconsistent.

![denormalized table for a blog posts project](https://lh3.googleusercontent.com/7uhXLc0vHEeIl6guinTbjKfrbn37RlT3Mii6nLdIdAGjR-66TPSDB9EyDkZeca71P7pA_tOphReWJ6xk4Y5vh7zO5eh4K8Twfroyh2N8GizTvbvWLvB_zgdnquVNCKK5vMXPCfigOUS_6MNjEftb8Vl-2Epr4nFOORfi3TlcekzYtPBUdJRHR7Km9MPKCYW8snNQBEvhWmQdJ2jDzUKvKqks38wwGV8tKT8ok6vNX3f9nEmniUOs0fTEcmX5BesT5HH-aufUbUExHOhl2JLqhJvYqIqw2bI6IK1SdhWlwsguJrusjr88ESwR3qVXdSdvTC7nAZrQTohidnlJ79U26c24EhQOpfTjfF1VKQ4jWM7ENAsurGinlQcV1zU2K7X2I0_qQ7oSQZ-O8loyKjzm-0GlfeWNhBnmH3azDKmCWsHsIzga_OCTCk8rGeWjbV-CTbxvnWhkTrqAhd99Y0TIQqMDJjUNPYHkTKBM2aTAq0TD0k9YPOYFheHxDZmmlx49apT2suoSzEQ41r3s9pZAzTsIq9UUwYSK8G7iRtYs4Hvv0rzqlp1TK1VJMQS4SF-8JeKAE8X8aBPlfokq9BjrFaDS8bBEtp81CKnNGFkupYqmM81z=w472-h95-no)

Hence this violates normalization because it violates a common way to describing normalized tables in 3rd normal form, which is that ***every non-key attribute in the table must provide a fact about the key, the whole key and nothing but the key***. And that's of a play on words for what you say in a US courtroom, telling the truth, the whole truth and nothing but the truth. The key in this case, is the `Post Id` and there is a non-key attribute `Author Email` which does not follow that. Because it does, in fact tell something about the author. And so it violates that 3rd normal form.

The above table can be represented in `MongoDB` as:

<pre><code>
{
  id: 'some id',
  title: 'some title',
  body: 'some content here',
  author: {
    name: 'author name',
    email: 'author email id'
  }
}
</code></pre>

# Refresher - what are the goals of normalization?

- **Frees the database from modification anomalies** - For `MongoDB`, it looks like embedding data would mostly cause this. And in fact, we should try to avoid embedding data in documents in `MongoDB` which possibly create these anomalies. Occasionally, we might need to duplicate data in the documents for performance reasons. However that's not the default approach. The default is to avoid it.
- **Should minimize re-design when extending** - `MongoDB` is flexible enough because it allows addition of keys without re-designing all the documents
- **Avoid bias toward any particular access pattern** - this is something, we're not going to worry about when describing schema in `MongoDB`. And one of the ideas behind the `MongoDB` is to tune up your database to the applications that we're trying to write and the problem we're trying to solve.


# Living Without Constraints

One of the great things about relational database is that it is really good at keeping the data consistent within the database. One of the ways it does that is by using foreign keys. A foreign key constraint is that let's say there's a table with some column which will have a foreign key column with values from another table's column. In `MongoDB`, there's no guarantee that foreign keys will be preserved. It's upto the programmer to make sure that the data is consistent in that manner. This maybe possible in future versions of `MongoDB` but today, there's no such option. The alternative for foreign key constraints is **embedding data**.

# Living Without Transactions

Transactions support [ACID](https://en.wikipedia.org/wiki/ACID) properties but although there are no transactions in `MongoDB`, we do have atomic operations. Well, atomic operations means that when you work on a single document that that work will be completed before anyone else sees the document. They'll see all the changes we made or none of them. And using atomic operations, you can often accomplish the same thing we would have accomplished using transactions in a relational database. And the reason is that, in a relational database, we need to make changes across multiple tables. Usually tables that need to be joined and so we want to do that all at once. And to do it, since there are multiple tables, we'll have to begin a transaction and do all those updates and then end the transaction. But with `MongoDB`, we're going to embed the data, since we're going to **pre-join** it in documents and they're these rich documents that have hierarchy. We can often accomplish the same thing. For instance, in the blog example, if we wanted to make sure that we updated a blog post atomically, we can do that because we can update the entire blog post at once. Where as if it were a bunch of relational tables, we'd probably have to open a transaction so that we can update the post collection and comments collection.

So what are our approaches that we can take in `MongoDB` to overcome a lack of transactions?

 - **restructure** - restructure the code, so that we're working within a single document and taking advantage of the atomic operations that we offer within that document. And if we do that, then usually we're all set.
 - **implement in software** - we can implement locking in software, by creating a critical section. We can build a test, test and set using find and modify. We can build semaphores, if needed. And in a way, that is the way the larger world works anyway. If we think about it, if one bank need to transfer money to another bank, they're not living in the same relational system. And they each have their own relational databases often. And they've to be able to coordinate that operation even though we cannot begin transaction and end transaction across those database systems, only within one system within one bank. So there's certainly ways in software to get around the problem.  
 - **tolerate** - the final approach, which often works in modern web apps and other applications that take in a tremendous amount of data is to just tolerate a bit of inconsistency. An example would, if we're talking about a friend feed in Facebook, it doesn't matter if everybody sees your wall update simultaneously. If okey, if one person's a few beats behind for a few seconds and they catch up. It often isn't critical in a lot of system designs that everything be kept perfectly consistent and that everyone have a perfectly consistent and the same view of the database. So we could simply tolerate a little bit of inconsistency that's somewhat temporary.

`Update`, `findAndModify`, `$addToSet` (within an update) & `$push` (within an update) operations operate atomically within a single document.

# One to one relations

1 to 1 relations are relations where each item corresponds to exactly one other item. e.g.:

 - an employee have a resume and vice versa
 - a building have and floor plan and vice versa
 - a patient have a medical history and vice versa

<pre>
<code>
 //employee
 {
 	_id : '25',
  	name: 'john doe',
 	resume: 30
 }

 //resume
 {
 	_id : '30',
  	jobs: [....],
 	education: [...],
  employee: 25
 }
 </code>
 </pre>

We can model the employee-resume relation by having a collection of employees and a collection of resumes and having the employee point to the resume through linking, where we have an `ID` that corresponds to an `ID` in th resume collection. Or if we prefer, we can link in another direction, where we have an employee key inside the resume collection, and it may point to the employee itself. Or if we want, we can embed. So we could take this entire resume document and we could embed it right inside the employee collection or vice versa.

This embedding depends upon how the data is being accessed by the application and how frequently the data is being accessed. We need to consider:

 - frequency of access
 - the size of the items - what is growing all the time and what is not growing. So every time we add something to the document, there is a point beyond which the document need to be moved in the collection. If the document size goes beyond 16[MB](https://en.wikipedia.org/wiki/Megabyte), which is mostly unlikely.
 - atomicity of data  - there're no transactions in `MongoDB`, there're atomic operations on individual documents. So if we knew that we couldn't withstand any inconsistency and that we wanted to be able to update the entire employee plus the resume all the time, we may decide to put them into the same document and embed them one way or the other so that we can update it all at once.

# One to Many Relations

In this relationship, there is many, many entities or many entities that map to the one entity. e.g.:
 - a city have many persons who live in that city. Say [NYC](https://en.wikipedia.org/wiki/New_York_City) have 8 million people.

 Let's assume the below data model:

 <pre>
 <code>
  //city
  {
  _id: 1,
  name: 'NYC',
  area: 30,
  people: [{
      _id: 1,
      name: 'name',
      gender: 'gender'
        .....
    },
    ....
    8 million people data inside this array
    ....
  ]
}
</code>
</pre>

This won't work because that's going to be REALLY HUGE. Let's try to flip the head.

<pre>
<code>
 //people
 {
 _id: 1,
 name: 'John Doe',
 gender: gender,
 city: {
     _id: 1,
     name: 'NYC',
     area: '30'
       .....
   }
}
</code>
</pre>

Now the problem with this design is that if there are obviously multiple people living in NYC, so we've done a lot of duplication for city data.

Probably, the best way to model this data is to use **true linking**.

<pre>
<code>
 //people
 {
 _id: 1,
 name: 'John Doe',
 gender: gender,
 city: 'NYC'
}

//city
{
_id: 'NYC',
...
}
</code>
</pre>

In this case, `people` collection can be linked to the `city` collection. Knowing we don't have foreign key constraints, we've to be consistent about it. So, this is a *one to many* relation. It requires 2 collections. For small one to few (which is also one to many), relations like blog post to comments. Comments can be embedded inside post documents as an array.

So, if it's truly one to many, 2 collections works best with linking. But for one to few, one single collection is generally enough.

# Many to Many Relations

e.g.:

 - books to authors
 - students to teachers

The books to authors is a **few to few** relationship, so we can have either an array of books or authors inside another's document. Same goes for students to teachers. We could also embed at the risk of duplication. However this will required that each student has a teacher in the system before insertion and vice versa. The application logic may always not allow it. In other words, the parent object must exist for the child object to exist.

# Multikeys

Multikey indexes is the feature because of which linking and embedding works so well. Assume that we've 2 schemas for student and teachers.

<pre>
<code>
 //students
 {
 _id: 1,
 name: 'John Doe',
 teachers: [1,7,10,23]
}

//teachers
{
_id: '10',
name:'Tony Stark'
}
</code>
</pre>

Now there are 2 obvious queries.

 - How to find all the teachers a particular student has had? - this can be searched by looking for teachers key in the students collection
 - How to find all the students whom have had a particular teacher? - this is a little difficult query and requires to use `set` operators. And order for that we need to be efficient, we need use **Multikey indexes**.

 To create an index on `teachers` column on `students` collection, use `db.students.ensureIndex({ teachers : 1 })`.

 ![creating indexes in MongoDB](https://lh3.googleusercontent.com/ed4cCRxNgf3FCq2JwHbq-PiHC1vgvvgE3S-rQ3UxA9R0cD3LxHGuI8t_YHk03wWxylFHEhNDjlJ-CfxitfLe35SbxPW9cK84bvTcghlpqf-vWBVC2xAruTx5jOPEesF8gc-9SvTeI8F2ZN-tmOEIuIQmRMrNYONPzkoXjFbs7-wVrMgjT0Jn7PHVyZQKzn9aaFasCcLrZzqHO8AW7qlIhraBZkd9BqbFC4fP6eKzskcbYVNTO4w7oG7CeKLFmc-riIxjZscSRm-_V6P8dZMp8W-l7XfSo_gcaiVyAXnZkAHsws7sd06q1v80IKa5i0lw82c53JoAZzQQKq-T3jxLC9xu1wkVOsprq0qEHODoh_LEc31C7M87lbAvRhkIlSNEjVADfevM8FFwyXlpr11ORFKBJJ4ZHxeMmxLdYgC8AMiegUXxs_LAnweV_A1SHe8N1R9CrC1h-EQXkv7XEFuCAl1Wh69VmxAGA12CbPpunPMiEjhh5vXU_DvCLBHfjvTRLo2aOG7Bdlvs1CAPtAZY5E3zW0nLlP9OHa4xT1TSV9Y6LWC0UMK9QnmOtQ6u0yPrkN1qEuX4i0fm8_VY7n53XFvQ7ZuVJkM4OvXnXdlpJ3gEYlwF=w424-h113-no)

Now to find all the students whom have had a particular teacher? use the query `db.students.find( { 'teachers': {$all: [0,1]}} )`. Now, if we append `.explain()` to the above query - it shows the internal working by showing where the keys were applied etc.

# Benefits of Embedding

The main reason for embedding documents in `MongoDB` is performance. The main performance benefit comes from improved read performance. Now, why do we get read performance. The reason is the nature of the way computer systems are built, which is they often have spinning disks and those spinning disks have a very **high latency**, which means they take a very long time (upto 1ms) to get to the first byte. But, when the first byte is access, each additional byte comes very quickly. So they tend to be pretty **high bandwidth**. So the idea is if we can co-locate the data to be used together in the same document, embed it and then we're going to spin the disk, find the sector where we need this information and then we're gonna start reading it. And we're going to get all the information we need in one go. Also it means if we have 2 pieces of data that would normally be in 2 collections or in several relational database tables. Instead, they're in one document, that we avoid **round trips to the database**.

# Trees

One classic problem from the world of schema design is how do you represent a tree inside the database? Let's look at the example problem for representing the e-commerce categories in a e-commerce site, such as Amazon. Where we have home, outdoors, winter, snow. And the idea is that we've the `products`. Also we've a `category`, where we can lookup **category 7** and see the `categoryName`, some of the properties for the `category`.

<pre>
<code>
 //products
 {
category: 7,
 productName: 'ABC'
}

//category
{
_id: '7',
categoryName:'outdoors',
parent: 6
}
</code>
</pre>

One way to do it is to keep a `parent` id - this might be something we can do in a simple relational database. But this doesn't make it easy to find all the `parent`s to this `category`. We've to iteratively query, find the parent of this and the parent of that until we get all the way to the top.

So an alternative way to do it in `MongoDB` is to be able to list ancestors or children. So, let's think about that and how that would work. So, we could decide to list all the children of this `category`:

<pre>
<code>
//category
{
_id: '7',
categoryName:'outdoors',
children: [3,6,7,9]
}
</code>
</pre>

That's also fairly limiting, if we're looking to be able to look and find the entire sub-tree that is above a certain piece of tree. Instead, what works pretty well and again, enable by the ability to put arrays inside `MongoDB` is to list the ancestors from the top in order.

<pre>
<code>
//category
{
_id: '7',
categoryName:'outdoors',
ancestors: [3,7,5,8,9]
}
</code>
</pre>

Again the ability to structure and express rich data is one of the things that makes `MongoDB` so interesting. This would be very difficult to do in a relational database. Now, in terms of how you represent the data for something like a `product` `category` hierarchy, again it all depends upon the access patterns. It depends on how we believe we're going to need to show the data, access the data for the user. And then based on that, we know how to model it.

# When to Denormalize

One of the reasons for normalization in relational database is to avoid modification anomalies that come with the duplication of data. And when we look at `MongoDB` and how it's structured, allowing these rich documents, it's easy to assume that what we're doing is we're denormalizing the data. And to certain extent, that's true. As long as we don't duplicate data, we don't open ourselves for modification anomalies.

Generally it's good to embed that data in case of **one to one** relationships. In case of **one to many** relationships, embedding can also work well without duplication of data as long as we embed from **many to the one**. Now, if we go from the one to the many, then linking would avoid the duplication of data. Now, if we want to embed something, even if it causes duplication of data for performance reasons to match the access patterns of the applications. That could make sense, especially if the data is rarely changing or being updated. But we can avoid it often enough, even in this relationship, if we go from the **many to one**. In **many to many** relation, which we looked at with `students` and `teachers` and `authors` and `books`, there if you want to avoid the modification anomalies that come with denormalization, all we need to do is link through the arrays of `object ids` in the documents.

![When to Denormalize in MongoDB](https://lh3.googleusercontent.com/7ZmjMz8KulV4BR4hn8A_a2toNpau-CzJmZlpbv8WJ9iSdiwTQLwoJl-VzHQohfJOhYLOZKdwYQX5enzB4D6NyDwHoky95tes8IFlh07ReY_Zi7m8cRdS3AwY-oerBUnu6Nk76yS4QrVW14zLN4FW8jDI9jcizIE9SMw9HmKbtHpVUQ7Jwt8EY1pnOlycrB2Bcx0VmhTKJNawDKf4oFsVDajX0mCVC7DKmIBFWuh2RhKMWmhnf-SEjQt5RAFayO78yW__AZ7IXM7Jv8HA8ENqeDhlaUjr4mXfHq4fn8Z4oUkWPrcskbZihR6dqOjTQl8-Mpcw2afMCqdi06HkaeES8Zvdh6ua6p5lOjzTLq1Nn6Y_Op5k_ENe9sdj_UR-9OnU6ATnpZwRakacZRdlPXbaSLSMUc1doJtG8PSRZSlgf8yUe2UNdKV8xeuTuRBj7gWWeZKzSuN00PQp_Ej6rY9DZbPWlMxhwm2dT1VJDRZkSsmjScGsQdYSNmjGWlnsBUOU4lCEC0GmuDET8YwQPmfRtsc_1IZqdymJUy44q368UTgGWUDEG49532tEnwcv70crSN03dRWoGOdcC7R-lxNR_jNRr1-CPvDzKDIM10mDHGqqwTsW=w629-h270-no)

These are all guidelines. For a real world application, we may need to embed data for performance reasons, to match the data access patterns - - it might be needed to embed the data.

[Photos](https://goo.gl/photos/mTCgFQN8b9s9sNzSA)