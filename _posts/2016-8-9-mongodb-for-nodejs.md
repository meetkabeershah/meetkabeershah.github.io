---
layout: post
title: MongoDB for node.js developers jumpstart
---

![MongoDB for node.js developers jumpstart](http://coenraets.org/blog/wp-content/uploads/2012/10/nodemango1.jpg)

[courtesy](http://coenraets.org/blog/2012/10/creating-a-rest-api-using-node-js-express-and-mongodb/)

These're my notes for the [MongoDB for node.js course](https://university.mongodb.com/courses/M101JS/about)

# What is MongoDB?

MongoDB is a document database holding data in JSON format. Since it's not based on joining, it's easy to distribute data across servers by it's sharding feature. 

Developers can develop application which can be agnostic about deployments. MongoDB supports scaling out as opposed to RDBMS which supports scaling up. Mongo shell is written using C++ V8 for administering the MongoDB.

# What is node.js

> `node.js` is basically a `C++` program that you control using `V8 javascript`. So any applications you write using `node.js` will be written in `javascript` and it will control this `C++` application (`node.js`) and you'll be able to say something like they made request for this resource and your application actually in `javascript` will say: okey, they made a request for this resource, I don't have to respond to that. Now respond accordingly.

`Node.js` connects to `MongoDB` using drivers. Installing `32` bit release shall be avoided because it limits the addressable size of data using the default storage engine.


# What is JSON?

To a layman, [`JSON`](http://json.org/) is merely a string, anyways. `JSON` objects are composed of *key-value* pairs. Keys must be strings, Keys and values must be separated by semi-colons. Fields within a `JSON` object are separated by commas as delimiters. `JSON` objects are opened and closed using curly braces:

<pre>
<code>
{
  "string" : "sting value goes here",
  "date" : "2015-10-27T22:35:21.908Z",
  "number" : 123,
  "object" : {
    "key1" : "value1",
    "key2" : "value2"
  },
  "boolean" : true,
  "array" : [ 
    "test", 
    { "key1" : "a", "key2" : "b" },
    [ "abc", "xyz" ]
  ]
}
</code>
</pre>

The above example shows that `JSON` supports a number of data-types. The `object` field shows an example of nested values. As we can see `object` and `array` - `MongoDB` data models commonly make use of nesting and even what we might call **deep nesting**. The flexibility `JSON` provides makes it simple to implement different data access patterns by creating objects that contain all the data required to render a webpage full of content or say to provide another type of data view for users with very few requests.

# What is BSON?
`MongoDB` stores data as [`BSON`](http://bsonspec.org/) (binary `JSON`). Here is the comparison:

<pre>
<code>
// JSON
{
	"hello": "world"
}

// BSON
"\x16\x00\x00\x00\x02hello\x00 \
x06\ x00\ x00\ x00world\ x00\ x00 "
</code>
</pre>

`MongoDB` drivers send and recieve data in `BSON` format and when the data is written to `MongoDB`, it's stored in `BSON`.

On the application side, the drivers map `BSON` to most appropriate native data types. It's

 - lightweight
 - traversable, to support a variety of operations necessary for writing, reading and indexing `MongoDB` documents
 - efficient, meaning encoding/decoding data to/from BSON as the drivers need to do can be performed very quickly.

`JSON` doesn't distinguishes between `integer`s and `float`s. Doesn't supports `date`s. `BSON` extends the JSON value types to include `integer`s, `double`s, `date`s and binary data to support images and a number of other types of data.

# Installation for Windows

To access the `mongo` and `mongod` directly from shell, Change the path for MongoDB:

 - Go to `System Properties`
 - Go to `Advanced settings`
 - Click `Environment variables`
 - Go to `System variables`
 - Go to `Path` (this is where Windows looks for executables)
 - Add the `MongoDB`'s startup location (eg: `C:\Program Files\MongoDB\Server\3.2\bin`)

Sometimes, you [might need to refresh the system to see these shortcuts working](http://superuser.com/q/1111180/249540)

However before using `mongodb` from terminal, create the `C:\data\db` directory for `MongoDB` to **store** data by following the below commands:

`md \data\db`

Notice, the `\` before `data\db` - this makes sure that the directory is created in root directory (in this case `C:\`) only.

Now, if you type `mongod` and hit <kbd>Enter</kbd>, it starts running. If you read the log printed on the terminal, it says that `MongoDB` is listening on `port=27017` and that `dbpath=C:\data\db` i.e. the default path - which we created lately.

Now, once `mongod` is running, we can start `mongo` which makes a connection to port `27017`.

# Doing some CRUD

For the sake of testing this installation, we'll do a simple document `insert` using:

`db.names.insert({name:'testing'})` and `find` (or `select` in relational terms) using the below command:

`db.names.find()`

![testing MongoDB installation](https://lh3.googleusercontent.com/kry_91WuTGqKobZt4ma96UEYocDv8YPufHa4YA1JQdo4Or9JQZPR6hBaQbEZ3r_829TIWIPAkCPPgnC4t1g-UxkNxxc_cTULnZ6B2CLwxz94SxTC1DRS6BGuFrWUk19WLOp1Km-_FsjZKK6TUQlPurTtk7iqKaGUlXogg05Dgl4Cj4swVbi3HhuY0-7oEjXuVi52FpNZtwpG4RujgvtUQ4kZb9kC66iP328As9XpnZAiBqtmImc1vzllMIut5Zxg4TYZUlnO3DB4zYIq1_cynCmoy_kVn4u8tJ-Wtp4RFY9sOmlXMPlAT1t49H1H0OpMHjAtelVxs_BJU0TMbaphDyQ28xeepwNiSPa4IE_nxiMFGJySs6s5RN_d0mQR_kjKD3rW0uaAt5vozAQAcscrt6qzYkQxHPg8n7kBAvOCDupumKmnpbbyPzoCQpCQjvOoRojxwoemeldPNrJ1mCkYCBJjuZoCa3CIvFm2b7U0sRy3Hp7pFAgU-TVvxFA6L5hphNx-KQ0uMWaM_iAKi3isMNzneTRmtSLSLuHKfC-jWPw3AgZsi8qjX6YTx31q3VMbW21DeUvBUV-bcj-vKc_a674rt621BHc=w643-h158-no)

Where `{name:'testing'}` is an example of document. Also, to make the result of `.find()` much readable, we can chain `.pretty()` command.

We can run `MongoDB` as a [service](http://stackoverflow.com/a/2438758/2404470) as well.

In `MongoDB`, documents are stored in colletions which are organized into databases. To see databases present in `MongoDB` run `show dbs`

To insert a document into a collection, we first need to know how to specify that collection in the command. A collection and database that contains it form a **namespace**. When doing `CRUD` operations, we reference the global variable `db`. This variable holds the reference to the database we're currently using. To switch to a database names **test** type [MySQL like command](http://stackoverflow.com/a/5287027) `use test`.

The insert operation returns a document as well, where `acknowledged` set to true indicates that the record (or better say, document) was inserted successfully. All documents must have an **underscore** _id field. Each document in a collection must have a unique document id. At the heart of the query language for `MongoDB` is a query by example strategy. We can pass a blank object `{}`, key value pair `{name: "Uber"}`. The result of `find()` command is not a mere array of documents, it's instead a `cursor object`. We can see this:

<pre><code>
var c = db.names.find();
c.hasNext() //returns true, meaning there is a document yet to be visited by this cursor 
c.next() //grabs that document
</code></pre>

# Building using node

To build applications using [node.js](https://nodejs.org/en/), we first need to [install it](http://xameeramir.github.io/install-node/).

Let's create a simple `http` server:

<pre><code>
// Source: howtonode.org/hello-node

// Load the http module to create an http server.
var http = require('http');

// Configure our HTTP server to respond with Hello World to all requests.
var server = http.createServer(function (request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello World\n");
});

// Listen on port 8000, IP defaults to 127.0.0.1
server.listen(8000);

// Put a friendly message on the terminal
console.log("Server running at http://127.0.0.1:8000/");
</code></pre>

Store the above code in a `.js` file, let's say `app.js`

> And how do we start it?

In the terminal, go to the location of the file and type `node app.js`. To verify, if it's running or not, go to [http://localhost:8000](http://localhost:8000). Notice port `8000`, which **we**'ve pecified in the above code.

# What is NPM

<pre><code>
    var express = require('express'),
    cons = require('consolidate'),
    mongodb = require('mongodb');
</code></pre>

`require()` is how we add an external library in a `node.js` application. If we run this code through `node` terminal, we'll get the below error:

![could not find module express](https://lh3.googleusercontent.com/heymDr6IIbrxBAL1ZtKpC7pZBQ9uZ3jb2IGIJ9H7sceVBVg_zIx8J4hY48Ez2Vff4JMz2arwZN-Q6TAakoT_Zz1OR5cxkOtnT5qzhP9Rw_Jnc3_kS97U2H_UHOn4dFZ4-f5umRvGA-UX0z7QvsNdUinYtxdJ1eFWbyoooSzPTwd2CRsesjNth1K9s-OqaucfLSqzEzCkTAvQksHnBNyQs-q0H4gYSN80E-LJj2FApyuS514y8423lfpyWXO6JLXU3qlmCnU3E5jcPajmQVUyEREJHTVwNBxxVBtZgDpMpJ-9ME4xkZCOqA4POINzSKaGf76JCsEsq2ZN--690d_pESogGYV_hps4i15KVDfw25UqW5k5MTQC3QwjOB_ynDOhrI3GrOx-WXePjgRNQwaMH24Noga6DXbtTsCfTxAT1ICKZqWDKyicj_PWMwwDrPpc2BaFfBXJNbvfGrp5uqMpnGg3al1agYZNSj-pD-aJ7ov76oVL-FiMKo3MR3dt6U9kPXK4u0-s3ZUAwVcvxem8q0P4OE9OAHtxvXLQEgiCJbVR1-AjftZuzJNjfjDBSQfVKy20FDh560_QzQAK7oXOJgD0tpX8tK0=w643-h171-no)

To get this missing `express` thing as a `node` package, we can use `node` command line `npm install express`.
In real projects, there will be a bunch of package dependencies. Installing them all one-by-one will be a big pain. To resolve this comes `package.json` file. This file contains meta data about the dependencies:

<pre><code>
{
  "name": "project name goes here",
  "version": "0.1.2",
  "description": "npm introduction",
  "main": "app.js",
  "dependencies": {
        "consolidate": "~0.13.1",
        "express": "~4.13.3",
        "mongodb": "~2.1.3"
  },
  "author": "ABC",
  "license": "MIT"
}
</code></pre>

With this file in **place**, simply running `npm install` will get all the packages for us inside **project's local** `node_modules` directory. There's also a way to install packages globally.

# What is Node.js Driver

The driver communicates with the `MongoDB` server using it's wire protocol. It handles things like opening sockets, detecting errors and managing connections to replica sets. To include the driver in an application, use code `var mongodb = require('mongodb');` and install using `npm install mongodb`. As we can see, it's **just** a node package. Try to connect to `MongoDB` using this package:

<pre><code>
var MongoClient = require('mongodb').MongoClient,
    assert = require('assert');

var url = 'mongodb://localhost:27017/startup';

MongoClient.connect(url, function(err, db) {

    assert.equal(null, err);
    console.log("Successfully connected to server");

    // Find some documents in our collection
    db.collection('startup').find({}).toArray(function(err, docs) {

        // Print the documents returned
        docs.forEach(function(doc) {
            console.log(doc.name);
        });

        // Close the DB
        db.close();
    });

    // Declare success
    console.log("Last call");
});
</code></pre>

In order to use the `MongoDB Node.js driver`, it's important to have a solid understanding of the **asynchronous** nature of `IO` in `javascript`, including database requests.

> The `mongo` shell is synchronous meaning that when you issue a find command, it blocks waiting for command to return before continuing. This is not the case with `Node.js` driver. Whether you're doing a query, as we are here in the call defined or just setting up a connection to the database. As is common in `Javascript` applications, the `Node.js` driver we're going to use is designed so that it's methods function asynchronously. What this means is that instead of waiting on a return value from any methods we call, we instead pass in a callback function.

The second parameter in the above `MongoClient.connect` call is a callback function. And is going to handle the result of this connection operation. Because of **anysnchronous** nature of `node.js`, the following message gets printed before any database values:

>`Last call`

# What is Express

`Express` is a `node.js` module that handles routing, request parameters and other details of `HTTP` requests.

Here is a basic example of setting up a basic `Express` server:

<pre><code>
var express = require('express'),
    app = express();

app.get('/', function(req, res){
    res.send('Hello World');
});

app.use(function(req, res){
    res.sendStatus(404); 
});

var server = app.listen(3000, function() {
    var port = server.address().port;
    console.log('Express server listening on port %s', port);
});
</code></pre>

# Implementing HTML Templates

The following example shows how to **implement** a `HTML` template:

<pre><code>
//file: app.js
var express = require('express'), //set up the Express server
    app = express(), //use it to create an Express app
    engines = require('consolidate'); //use the wrapper library

app.engine('html', engines.nunjucks); //register nunjucks template engine

app.set('view engine', 'html'); //as being associated with the html extension, set the view engine app setting

app.set('views', __dirname + '/views'); //specify template location

app.get('/', function(req, res) {
    res.render('hello', { name : 'Templates' });
});

app.use(function(req, res){
    res.sendStatus(404); 
});

var server = app.listen(3000, function() {
    var port = server.address().port;
    console.log('Express server listening on port %s', port);
});
</code></pre>

<pre><code>

//file: views/hello.html

&lt;h1&gt;Hello, &#123;&#123;name&#125;&#125;!&lt;/h1&gt;

</code></pre>

In the above code, `consolidate` is basically a set of wrappers for a number of template engines for `Express`. `Express` requires certain libraries to have a certain interface and `consolidate` handles that for us. `__dirname` is a `node.js` variable which allows us to access to the directory in which the application file (in our case, `app.js`) resides. Since, we've passed `name : 'Templates'` - we'll see the below output:

![Hello Templates](https://lh3.googleusercontent.com/G2kdPbPZRByvK44lLOPvSLCYd7l-NOpK9MayaxFBJeme9UjdUNxvLJex0qtUHhYPi-TM-apU0SMT0ZnjtnwkmNCLxw4JkLNFHapWujKjlSbVCfDSux_J-daorCYLATI6YuedbLFhsXySXqFg5Iv4xJ-p578uxuo0C-_DYc8J4QYCo_6ppJHFH3EHATavtPwzeGdLPmspF_Px97A9WANzbtRAirmE0GjQYVptcb13AXl9bm5aJ2gFGJJLjQw18ddl7gH7E-wuOtwEy3S5fi9oirjzn5wUqvyU2UhTywMLKzPB4BMom_LW0k7-hVQp_JBsDjoZeXKuSCkL4dYk9iYKjESSPq3A693RLP83vYJq1qhK0cloVMraAeIWBfDdLWaJG3WJGxzc5GitE4LQR2PeDQDoqLylMymGoXoNuj4gEsi2UAXlO01ncifSaU7lGiIucX8hcgWZ6dCFbMgbjxlNoFqlIm3bN_G5we6o25ZAvVoabBt6csO7YS5szhFtVSLA56J2rZaFFH2-2ODqNF8_Z4hg7mKcFWRJOIqT1QC8P4NpqyE9pkMQHzfA6GwRvfBBMBVHehwHsR341FOYcdM3JNZ20RUCtF4=w276-h98-no)

Here's a more advanced version which connects to the database as well:

<pre><code>
//file: app.js

var express = require('express'),
    app = express(),
    engines = require('consolidate'),
    MongoClient = require('mongodb').MongoClient,
    assert = require('assert');

app.engine('html', engines.nunjucks);
app.set('view engine', 'html');
app.set('views', __dirname + '/views');

MongoClient.connect('mongodb://localhost:27017/startup', function(err, db) {

    assert.equal(null, err);
    console.log("Successfully connected to MongoDB.");

    app.get('/', function(req, res){

        db.collection('startup').find({}).toArray(function(err, docs) {
            res.render('startup', { 'name': docs } );
        });

    });

    app.use(function(req, res){
        res.sendStatus(404);
    });
    
    var server = app.listen(3000, function() {
        var port = server.address().port;
        console.log('Express server listening on port %s.', port);
    });

});
</code></pre>

<pre><code>

//file: views/startup.html

&lt;h1&gt;Hello, &#123;&#123;name&#125;&#125;!&lt;/h1&gt;

</code></pre>

# Handling GET requests using Express

<pre><code>
var express = require('express'),
    app = express(),
    engines = require('consolidate');

app.engine('html', engines.nunjucks);
app.set('view engine', 'html');
app.set('views', __dirname + '/views');

// Handler for internal server errors
function errorHandler(err, req, res, next) {
    console.error(err.message);
    console.error(err.stack);
    res.status(500).render('error_template', { error: err });
}

app.get('/:name', function(req, res, next) {
    var name = req.params.name;
    var getvar1 = req.query.getvar1;
    var getvar2 = req.query.getvar2;
    res.render('hello', { name : name, getvar1 : getvar1, getvar2 : getvar2 });
});

app.use(errorHandler);

var server = app.listen(3000, function() {
    var port = server.address().port;
    console.log('Express server listening on port %s.', port);
});
</code></pre>

The `hello` template is:

<pre><code>
&lt;h1&gt;Hello, &#123;&#123;name&#125;&#125;, here are your GET variables:&lt;/h1&gt;
&lt;ul>
    &lt;li&gt;&#123;&#123;getvar1&#125;&#125;&lt;/li&gt;
    &lt;li&gt;&#123;&#123;getvar2&#125;&#125;&lt;/li&gt;
</ul>
</code></pre>

and the `error` template goes here:

<pre><code>
&lt;h1&gt;Error: &#123;&#123;error&#125;&#125;&lt;/h1&gt;
</code></pre>

In the above app, we're just registering only one route i.e. `/:name`. The colon says to take this part of the URL and store in a variable called `name`.

Will share further notes next week.

[Photos](https://goo.gl/photos/Yuigw4S9mLXDpSZN6)
