---
layout: post
title: Working with the examples for Node.js driver
---

The `node.js` driver is a package for interacting with `MongoDB`.

# Importing a JSON

The command `mongoimport` allows us to import human readable `JSON` in a specific database & a collection.
To import a `JSON` data in a specific database & a collection, type `mongoimport -d databaseName -c collectionName jsonFileName.json`

# find() and Cursors in the Node.js Driver

<pre>
<code>
var MongoClient = require('mongodb').MongoClient,
assert = require('assert');

MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

assert.equal(err, null);
console.log("Successfully connected to MongoDB.");

var query = {
"category_code": "biotech"
};

db.collection('companies').find(query).toArray(function(err, docs) {

assert.equal(err, null);
assert.notEqual(docs.length, 0);

docs.forEach(function(doc) {
console.log(doc.name + " is a " + doc.category_code + " company.");
});

db.close();

});

});
</code>
</pre>

Notice that the call `.toArray` is making the application to fetch the entire dataset.

<pre>
<code>
var MongoClient = require('mongodb').MongoClient,
assert = require('assert');

MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

assert.equal(err, null);
console.log("Successfully connected to MongoDB.");

var query = {"category_code": "biotech"};

var cursor = db.collection('companies').find(query);

function(doc) {
cursor.forEach(
console.log( doc.name + " is a " + doc.category_code + " company." );
},
function(err) {
assert.equal(err, null);
return db.close();
}
);
});
</code>
</pre>

Notice that the **cursor** returned by the `find()` is assigned to `var cursor`. With this approach, instead of fetching all data in memort and consuming data at once, we're streaming the data to our application. `find()` can create a cursor immediately because it doesn't actually make a request to the database until we try to use some of the documents it will provide. The point of `cursor` is to describe our query. The 2nd parameter to `cursor.forEach` shows what to do when the driver gets exhausted or an error occurs.

In the initial version of the above code, it was `toArray()` which forced the database call. It meant we needed **ALL** the documents and wanted them to be in an `array`.  

Also, `MongoDB` returns data in batch format. The image below shows, requests from cursors (from application) to `MongoDB`   

![MongoDB cursor requests](https://lh3.googleusercontent.com/_utjj5lUN8AMPPf9JCUf3NwP6SoK14g9IrDiglPhNOyLYQq81PaoibVcsDGLxtN1GgBOrUk-_xiobeUcKSUP90crPC7JiflvblQhgRX-d_8noqoBXkQxhDGLRJs8O2LvcdwA4_hoGJSVmFgDUZUkRI-TYG2PKaQMKE171ufX3QFHkKE-jO1gZC06mHAxRLhuDkzip1IFR-Slo-Y6i4hO_bnNGSIMLflu40KZ-waxx0El1D0rNu3JfWFvMkta48SB2a9SGmSZnOD-Vl8A_8B9i7xk4oCaY4TZLq5PKOcgL8z_pCSY2sTqkYACHfl_Itd54Od38fpPAIBu7TWKKAm8hAJfU6QAfuAOiT1khMmzOqvO6zRmEAVlrXybWV26WDtvBumcfmnaZIBUUNUC7MeKP0nim32axhwJQxa_hEs7kmNHjrOzp2k4URp_mFl-XIBNfCGPkjafJkgnw2Tfz4qI8E5p1L29hlgjAmJyZWKvA8Ny5olYK7fe_N_1Sj9mc0hm3vnMnuKaA61pReh8Q2OSLqwJxyYRXhocFaNC6HXiBaqH9s4_VahUeO_xHvdgZWL1u9SGPYiNK2vVSexagjYVKJXnJ3RfJ1g=w668-h230-no)

`forEach` is better than `toArray` because we can process documents **as they come in** until we reach the end. Contrast it with `toArray` - where we wait for **ALL** the documents to be retrieved and the **entire** array is built. This means we're not getting any advantage from the fact that the driver and the database system are working together to batch results to your application. Batching is meant to provide efficiency in terms of memory overhead and the execution time. *Take advantage of it, if you can in your application*.

# Projection in the Node.js Driver

Remember that projections allows us to explicitly include or exclude fields in a `MongoDB` query. We use **`1`** to indicate that we want to include a field and **`0`** to indicate that we wish to exclude the field. Remember that `_id` field is special -

 - `_id` field gets included by default, unless we explicitly exclude it
 - All other fields are excluded, until we explicitly include them

Also, since we're working in `javascript`, we can construct our project documents and documents to be inserted into our collections in a way that is very similar to the way we do this in the `mongo` shell. What's different is the driver provides one set of classes and methods we use to interact with `MongoDB` and the `mongo` shell provides it's own API.

W. r. t. `CRUD` as of `MongoDB 3.2` the driver and the `mongo` shell adhere to the same spec. How you access these methods and how they're implemented varies of course, from the `mongo` shell.

<pre>
<code>

var MongoClient = require('mongodb').MongoClient,
    assert = require('assert');


MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

    assert.equal(err, null);
    console.log("Successfully connected to MongoDB.");

    var query = {"category_code": "biotech"};
    var projection = {"name": 1, "category_code": 1, "_id": 0};

    var cursor = db.collection('companies').find(query);
    cursor.project(projection);

    cursor.forEach(
        function(doc) {
            console.log(doc.name + " is a " + doc.category_code + " company.");
            console.log(doc);
        },
        function(err) {
            assert.equal(err, null);
            return db.close();
        }
    );

});

</code>
</pre>

The current best practice in the `node.js` driver, is to chain a call to `project` onto our `cursor` i.e. `cursor.project`. This call to project sets a field projection for the query. This call does not force a request to retrieve documents from the database, as does the `foreach` method. Rather it adds some additional details to the query representation maintained by our `cursor`. There're a number of cursor methods, we can chain together to fully express the operation we wish to execute against our `MongoDB` database. The call to `db.collection` is synchronous. We're going to modify that `cursor` with a field `projection` here using the `project` method on the cursor.

# Query Operators in the Node.js Driver

<pre>
<code>
var MongoClient = require('mongodb').MongoClient,
    commandLineArgs = require('command-line-args'),
    assert = require('assert');


var options = commandLineOptions();

MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

    assert.equal(err, null);
    console.log("Successfully connected to MongoDB.");

    var query = queryDocument(options);
    var projection = {"_id": 1, "name": 1, "founded_year": 1,
                      "number_of_employees": 1, "crunchbase_url": 1};

    var cursor = db.collection('companies').find(query, projection);
    var numMatches = 0;

    cursor.forEach(
        function(doc) {
            numMatches = numMatches + 1;
            console.log( doc );
        },
        function(err) {
            assert.equal(err, null);
            console.log("Our query was:" + JSON.stringify(query));
            console.log("Matching documents: " + numMatches);
            return db.close();
        }
    );

});


function queryDocument(options) {

    console.log(options);

    var query = {
        "founded_year": {
            "$gte": options.firstYear,
            "$lte": options.lastYear
        }
    };

    if ("employees" in options) {
        query.number_of_employees = { "$gte": options.employees };
    }

    return query;

}


function commandLineOptions() {

    var cli = commandLineArgs([
        { name: "firstYear", alias: "f", type: Number },
        { name: "lastYear", alias: "l", type: Number },
        { name: "employees", alias: "e", type: Number }
    ]);

    var options = cli.parse()
    if ( !(("firstYear" in options) && ("lastYear" in options))) {
        console.log(cli.getUsage({
            title: "Usage",
            description: "The first two options below are required. The rest are optional."
        }));
        process.exit();
    }

    return options;

}
</code>
</pre>

To call it use `node app.js -f 2004 -l 2008 -e 100`. Notice that `commandLineArgs` is getting `parse`d. Also, you might see the difference between the `_id` field representation by `mongo` shell and `node.js` driver:

 - `_id : ObjectId("507f1f77bcf86cd799439011")` on `mongo` shell
 - `_id : 507f1f77bcf86cd799439011` on `node.js` driver

This happens because of the difference in the way `node.js` driver and the `mongo` shell chooses to stringify the `_id` field.

# $regex in the Node.js Driver

<pre>
<code>
var MongoClient = require('mongodb').MongoClient,
    commandLineArgs = require('command-line-args'),
    assert = require('assert');

var options = commandLineOptions();

MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

    assert.equal(err, null);
    console.log("Successfully connected to MongoDB.");

    var query = queryDocument(options);
    var projection = projectionDocument(options);

    var cursor = db.collection('companies').find(query);
    cursor.project(projection);

    var numMatches = 0;

    cursor.forEach(
        function(doc) {
            numMatches = numMatches + 1;
            console.log( doc );
        },
        function(err) {
            assert.equal(err, null);
            console.log("Our query was:" + JSON.stringify(query));
            console.log("Matching documents: " + numMatches);
            return db.close();
        }
    );

});

function queryDocument(options) {

    console.log(options);

    var query = {};

    if ("overview" in options) {
        query.overview = {"$regex": options.overview, "$options": "i"};
    }

    if ("milestones" in options) {
        query["milestones.source_description"] =
            {"$regex": options.milestones, "$options": "i"};
    }

    return query;
}

function projectionDocument(options) {

    var projection = {
        "_id": 0,
        "name": 1,
        "founded_year": 1
    };

    if ("overview" in options) {
        projection.overview = 1;
    }

    if ("milestones" in options) {
        projection["milestones.source_description"] = 1;
    }

    return projection;
}

function commandLineOptions() {

    var cli = commandLineArgs([
        { name: "overview", alias: "o", type: String },
        { name: "milestones", alias: "m", type: String }
    ]);

    var options = cli.parse()
    if (Object.keys(options).length < 1) {
        console.log(cli.getUsage({
            title: "Usage",
            description: "You must supply at least one option. See below."
        }));
        process.exit();
    }

    return options;
}
</code>
</pre>

The `$options` set to `i` indicates that the `regex` search needs to be case-insensitive. `MongoDB` supports `perl` like regular expressions. There're a couple of ways in which we can set the values for the query documents:

 - Using curly braces `{ "_id": 0, "name": 1, "founded_year": 1 }`

 - Using dots `projection.overview = 1;`

 - Using array indexing `projection["milestones.source_description"] = 1;`

# Sort, Skip, and Limit in the Node.js Driver

To sort documents, we can apply `sort` on a `cursor` object. To enforce order of sort, instead of passing an object, we need to pass an array to the `sort` method.

<pre>
<code>
var MongoClient = require('mongodb').MongoClient,
  commandLineArgs = require('command-line-args'),
  assert = require('assert');


var options = commandLineOptions();


MongoClient.connect('mongodb://localhost:27017/crunchbase', function(err, db) {

  assert.equal(err, null);
  console.log("Successfully connected to MongoDB.");

  var query = queryDocument(options);
  var projection = {
    "_id": 0,
    "name": 1,
    "founded_year": 1,
    "number_of_employees": 1
  };

  var cursor = db.collection('companies').find(query);
  cursor.project(projection);
  cursor.limit(options.limit);
  cursor.skip(options.skip);
  cursor.sort([
    ["founded_year", 1],
    ["number_of_employees", -1]
  ]);

  var numMatches = 0;

  cursor.forEach(
    function(doc) {
      numMatches = numMatches + 1;
      console.log(doc.name + "\n\tfounded " + doc.founded_year +
        "\n\t" + doc.number_of_employees + " employees");
    },
    function(err) {
      assert.equal(err, null);
      console.log("Our query was:" + JSON.stringify(query));
      console.log("Documents displayed: " + numMatches);
      return db.close();
    }
  );

});

function queryDocument(options) {

  console.log(options);

  var query = {
    "founded_year": {
      "$gte": options.firstYear,
      "$lte": options.lastYear
    }
  };

  if ("employees" in options) {
    query.number_of_employees = {
      "$gte": options.employees
    };
  }

  return query;

}


function commandLineOptions() {

  var cli = commandLineArgs([{
    name: "firstYear",
    alias: "f",
    type: Number
  }, {
    name: "lastYear",
    alias: "l",
    type: Number
  }, {
    name: "employees",
    alias: "e",
    type: Number
  }, {
    name: "skip",
    type: Number,
    defaultValue: 0
  }, {
    name: "limit",
    type: Number,
    defaultValue: 20000
  }]);

  var options = cli.parse()
  if (!(("firstYear" in options) && ("lastYear" in options))) {
    console.log(cli.getUsage({
      title: "Usage",
      description: "The first two options below are required. The rest are optional."
    }));
    process.exit();
  }

  return options;

}

</code>
</pre>

One thing to notice is the order in which `MongoDB` applies `skip`, `limit` and `sort`

 - `sort`
 - `skip`
 - `limit`

![MongoDB skip, limit and sort order](https://lh3.googleusercontent.com/6mhk_4rQhKp8sF03brXg-OAbsKEJtxHLFp4MtPA_eom3Dabo1ptkY5Nz7UUZ8W-q_JfGiiVVt9AGGIwJns2KoVYKk18Z5VVP6PWaC7zktndNIXzFp3U-IadJSt-KzIxL2hP4wA3vguJqZB7GP9JBOUtJWgYmgX1gEMmIXQRW2z6DKMB_J0YUcZ9pF0a_woe0Weg76MADCcxwXgeb5qRbkXKjxhsqlwgo00qYZBdhlWAExclJ0uDv0awFKQrkbGDuv6ztk1S4huyaSKpeFQq-QOof0oq0YsjRUy_npf-C36_BSV2ACOQvXihdjyVNbj8Ie31y3uNK3musJ035P-L-OAhOqFWc92UZTVVc1JXQQrHO8vTnJyLNc0mmgEfnou9iK2CiPAu4mka0lxjJamuTpnFSCk8u_oDT_mnschCPOVsQv_28YwduIXtQSDsinrw_Kgt1CYMHF3nr1yGH03-YDsZ_tMopADig7LMzaFNBNP3FZZMZyuGYJJrfmX7somz2eLBdJHg5oWX9O7mQIK2trAM4kknc1_2FqzJTDPCOYmarmo8rXP4j_bHB6no-f_FJYDdJ7_Crrnn7jXiaosLYpxMbwkoZbb0=w629-h201-no)

There's also a possibility that we can sort data on the `MongoDB` side as well, provided that we've setup the indexing.

Notice that `MongoDB` driver will send a query when we call a cursor method passing a callback function to process query results.

[Photos](https://goo.gl/photos/rV5pRUS2f8PZJiKF7)
