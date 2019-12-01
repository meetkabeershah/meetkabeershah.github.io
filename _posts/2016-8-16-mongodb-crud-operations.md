---
title: CRUD operations in MongoDB
layout: post
---

![CRUD](http://www.codingerik.com/assets/images/crudblog.png)

[courtesy](http://www.codingerik.com/CRUD_Loop_Tutorial-post.html)

In this post, we're going to see a few example of CRUD operation in `MongoDB`

# Restoring using mongorestore
After making sure that `mongod` and `mongo` are running, go to the dump's parent directory in a new terminal. And use the command `mongorestore dump`. Where `dump` is the folder name in which the database dump is present.

![Restoring using mongorestore](https://lh3.googleusercontent.com/GsQPxzd5QaVK3bN6tQaOFAepiQ_BIVmn-CgSuPo5bVH4L3w1Ev5JJUJkO3NaOCqQK7i14uxm5QikvmCbv-6jz5hJJzcFG4-HXZo40-jxAyAPNclNx1m5puEaXUmnLA7Nss5zrP0ovBJL1jiKOBZH0Rof8Kg6yfKzdWBA8I8__kW2eXgLWVnbjqeGlz2N2tH_7Ou9eXYxGNSB4-ZuXot3_rm_GYar-TPwkr05D_0fITy2JgsPQezsTMpMHr7REkxVRK-Il-TRzktppVaS0Pd3eCnyRaK_PF867pCvWI25AkTjS_Y1VUn3BniociBqIqZBsQklP-miKtDlurav6CAh_Fek7b0vQCmfvbDX1MmpV9x00QNUrxfoCdDZ6oVuoH3jRYsVntsxmRfi5zTCqvh9ddUjPjrlBNJ9HyJrRaK5ee8P5tI_xquJODZn4CtLAU6g2oVQ4bxDtfZppzf_pYcmUBWuN1v-jQIn4zdc2xbfhePTqASgDi5NZiF83o8XhwuCjhXEY-aqGastao7ZYC77CNKodQ8knWeR9ApAq9STOQ6Orvsz-IuvCCnlG01-Qz8i2aqCz3Rr4rEX_RFIlfIHd4EmcRfvC98=w648-h443-no)

# Creating Documents

There're two principal commands for creating documents in MongoDB:

- `insertOne()`
- `insertMany()`

There're other ways as well such as `Update` commands. We call these operations, upserts. Upserts occurs when there're no documents that match the **selector** used to identify documents.

Although MongoDB inserts ID by it's own, We can manually insert custom IDs as well by specifying `_id` parameter in the `insert...()` functions.

To insert multiple documents we can use `insertMany()` - which takes an array of documents as parameter. When executed, it returns multiple `id`s for each document in the array. To drop the collection, use `drop()` command. Sometimes, when doing bulk inserts - we may insert duplicate values. Specifically, if we try to insert duplicate `_id`s, we'll get the `duplicate key error`:

<pre><code class="javascript">

db.startup.insertMany(
  [
  {_id:"id1", name:"Uber"},
  {_id:"id2", name:"Airbnb"},
  {_id:"id1", name:"Uber"},
  ]
  );
</code></pre>

![MongoDB duplicate key error](https://lh3.googleusercontent.com/g_f8pkYn3-e01QF8AECbIi-n_x6qB1xhbEx-e5FEZC9KA8f5FI9mx05cGZaNAaDUCdsJ7LHJz9DH-aXpU8iZlFwu154_8FsUe8cpfLTm4yImQJ4MJv8CZyat0GqjCpbN05sZ_UgEv9HqxTTgbNjlFGrPYthKepJwZ0dQrmMNxyAJOwXU_FQd752v9l_f-1-jKzkmrgNwOmYFpkvxq1PKbmo39LJdRxjR2CUsUn0xaIvrX5Ns_dJjKAaiWZN-7Kn73i55eWWt4sZduGdpE4fsUVIUZRZmUp2RpPu6VPZ7nbRG6BVkL6oFvQYuwI0Y4aCbe8AnIlkr3Y8tpN8iSxSLnZIDSoH0KB92ldrIAZjYK2UugB5WlSLiLuJst0tdLCs2FPpbFf4nu1ajDzzpkEKsdOR79lQNRxz-uOAg8lAaXY4EY7QL7VpWNVtKhFFsuCSkcZRKDmwyFwYFVL2RrsKBB6-Jz2lAAfaFFb5tBvHClr-iH91UYoLlNcF138MtaoXanU25K_5SqicvoF7gC5J4TaeaM4Obl95dBFtIVxPdlJOc_sXrPNsCKduhtC7MR3LBj7su0MxKixG850BQApxCjX6Bk_neK8I=w603-h102-no)

MongoDB stops inserting operation, if it encounters an error, to supress that - we can supply `ordered:false` parameter. Ex:

<pre><code class="javascript">

db.startup.insertMany(
[
{_id:"id1", name:"Uber"},
{_id:"id2", name:"Airbnb"},
{_id:"id1", name:"Airbnb"},
],
{ordered: false}
);
</code></pre>

# The _id field

`MongoDB` assigns an `_id` field to each document and assigns primary index on it. There're ways by which we can apply secondary indices as well. By default, `MongoDB` creates values for the `_id` field of type `ObjectID`. This value is defined in `BSON` spec and it's structured this way:

> ObjectID (12 bytes HEX string) = Date (4 bytes, a timestamp value representing number of seconds since the Unix epoch) + MAC address (3 bytes) + PID (2 bytes) + Counter (3 bytes)

# Reading documents

To apply specific value filters, we can pass specific values to the `find()` command. Here is a SQL query:

`SELECT * FROM Table1 WHERE name = 'ABC'`

which is equivalent to the following in `MongoDB` (notice `Collection1` for `Table1`):

`db.Collection1.find({name: 'ABC'})`

We can chain `count()` to get the number of results, `pretty()` to get a readable result. The results can be further narrowed by adding additional parameters:

`db.Collection1.find({name: 'ABC', rollNo: 5})`

It's important to notice that these filters are **AND**ed together, by default. To apply an **OR** filter, we need to use `$or`. These filters will be specified depending upon the structure of the document. Ex: for object attribute `name` for an object `school`, we need to specify filter like `"school.name" = 'AUHS'`

We're using here the **DOT** notation, by trying to access a nested field `name` of a field `school`. Also notice that the filters are **quoted**, without which we'll get syntax errors.

**Equality matches on arrays can be performed:**

- on the entire arrays
- based on any element
- based on a specific element
- more complex matches using operators

In the below query:

`db.Collection1.find({name: ['ABC','XYZ']})`

`MongoDB` is going to identify documents by an exact match to an array of one or more values. Now for these types of queries, the **order** of elements matters, meaning that we will only match documents that have `ABC` **followed** by `XYZ` and those are the **only 2** elements of the array `name`

<pre><code>
{name:["ABC","GHI","XYZ"]},
{name:["DEF","ABC","XYZ"]}
</code></pre>

In the above document, let's say that we need to get all the documnts where `ABC` is the first element. So, we'll use the below filter:

`db.Schools.find({'name.0': 'ABC' })`

# Cursors in MongoDB

`MongoDB` returns results in batches. To see how many objects are left in a batch, we use `objLeftInBatch()` like this:

<pre><code>
var c = db.Schools.find();
var doc = function() {return c.hasNext()? c.next : null;}
c.objLeftInBatch();
</code></pre>

To iterate through this batch we can use `doc()` that we setup in the above code block. More learning on cursors can be found at [https://docs.mongodb.com/](https://docs.mongodb.com/)

# Projection in MongoDB

Projection is a handy way of reducing the size of the data returned for any one query. By default `MongoDB` returns all fields in all documents for queries. To limit the amount of data that `MongoDB` sends to the application, we can include projections in the queries to reduce network overhead and processing requirements by limiting the fields that're returned in results documents. They're provided as second argument to the `find()` command. Now, if we need to limit our documents so that they just contain a title. We can do that using this `db.Schools.find({name:"ABC"},{rollNo:1}).` In the result, `_id` is always returned. To exclude it, use `db.Schools.find({name: "ABC"},{rollNo: 1, _id: 0}).`. So, to exclude any field, use 0 next to the colon in project query.

# Comparison operators in MongoDB

We can use [comparison operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/) as well in our queries. Eg: Use `db.Schools.find({rollNo: {$gt: 10}})` To find all students having roll number beyond than 10. Notice the [`$gt`](https://docs.mongodb.com/manual/reference/operator/query/gt/#op._S_gt) operator. Combine this filter with [$lt](https://docs.mongodb.com/manual/reference/operator/query/lt/#op._S_lt) for getting results beyond roll number 10 and before roll number 50: `db.Schools.find({rollNo: {$gt: 10, $lt: 50}})`.

There're other operators as well: `$gte` (greater than, equal to), `$lte` (less than, equal to), `$ne` (not equal to). One thing to notice about the not equal to (`$ne`) operator is that it not only returns documents having value not equal to specified value but also returns documents not having the attribute itself.  

# Element operators in MongoDB

`MongoDB` because of it's flexible data model supports operators that allow us to detect the presence of or absence of a given field. This flexibility in terms of data models also extends to the data type of a field value. Because it's possible although not usually a good idea, to have the same field in a collection have a different type of value from one document to another. These operators are used for finding the existence of elements (`$exists`) and data type of the field using the `$type` operator.

# Logical operators

Like SQL, there're [logical operators](https://docs.mongodb.com/manual/reference/operator/query-logical/) such as `$and`, `$or`, `$not` and `$nor`. These're the examples:

<pre><code>
db.Schools.find({
  $and: [{ rollNo: { $gt: 10 }}, { rollNo: { $gt: 50 }}]
  })

db.Schools.find({
  $or: [{ rollNo: { $gt: 10 }}, { rollNo: { $gt: 50 }}]
  })
</code></pre>

Now, why there's an `$and` operator [when the filters are by default **AND**ed?](http://stackoverflow.com/q/38960922/2404470) Because, in a `JSON` document, we cannot have duplicate keys. In the above `$and` example, we're **AND**ing `rollNo` twice. Remember that `$and` is used we need to filter data on the same field.

# Regular operators

- The slashes `/` in the below regex code means the start and end of the regular expression.
- The carat `^` means start at the beginning of whatever value we're matching against and match exactly a capital AB.
- The dot `.` is the wild card character.
- The arterisk `*` indicates match any character any number of times
- `\s` means a space character after AB
<pre><code>
db.Schools.find({
{ name: { $regex: /^AB\s.*/ }}
})
</code></pre>

# Array operators

These operators are used to work on arrays. For getting matching values from an array (`$all`), arrays of a particular size (`$size`) and `$elemMatch` - which [requires all criteria be satisfied](http://stackoverflow.com/q/38960922/2404470) within a single element of an array field.  

# Updating documents

`MongoDB` provides 3 ways to update documents.

- `updateOne()` - the first argument is the filter expression, second specifies the values to be updated
- `updateMany()`
- `replaceOne()`

<pre><code>
db.Schools.updateOne({ name: "ABC" }, { $set: { rollNo: 15 } })
</code></pre>

There are a couple of [update operators](https://docs.mongodb.com/manual/reference/operator/update/#id1). In the above query, `$set` operator simply replaces (or adds if not already exists) the value for the field being specified. There are [array update operators](https://docs.mongodb.com/manual/reference/operator/update/#array) as well. To apply updates for each `array` element, use the `$each`. `$position` modifies the $push operator to specify the position in the array to add elements.

Sometimes, we might see elements set to **NULL**. It's better to remove them altogether using `$unset` operator.

<pre><code>
db.Schools.updateMany({ name: null }, { $unset: { name: "" } })
</code></pre>

# Upserts of update command

Upserts are operations for which, if no document is found matching our filter, we insert a new document - hence the term **upsert**.

And here we finish second week [course](https://university.mongodb.com/courses/M101JS/about) notes

[Photos](https://goo.gl/photos/bXNX1CXXhi6qahue9)