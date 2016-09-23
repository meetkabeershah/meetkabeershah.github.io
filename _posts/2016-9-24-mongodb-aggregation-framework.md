---
layout: post
title: The Aggregation framework
---

![The Aggregation framework](https://lh3.googleusercontent.com/KCXoOKQIIxCJYAjPPjaIyBzm5aC6PbDpMqV6--qJZ4pLLDx7EHrnjnN5ZamCPxSSIVrPqKTf9bdafFC3KGmDAXetPn7JEwzpwf8XWDFabgUGYfY63_ZqAmfUDX1e00c5RjZoA-OJRgBzVKTXnkkHutAqrWFCk5gKvCiaV7tv3nDOipIpIYbFZNldXeO7V_VjdRGEmr7sgHqaa9HxgBq1X8vZC-ApX1Fa55GOpRl2UzKgMR9WHZcs4bx4Z4MAfyZK3p3YnZ2G-KW30i-nuP7HB-GavXTpDzVM_irJiQn_ZNEQanL9ZLHtoMbCeDc1ofC-miN1vKF6QsvDXLgGBCQ6Z9Fw8n1xc9f9hWbRClHIr3xu2UAz0ASmiRGupb29LBJ0T9_ZE92JiNA9ofiKbuaLaNaoy3ueVaTg90yBwQP3CePNGeXosP35jw-21IYq4Uc6MpK0kHC7zCys4vlVEKDnrRFabIvjdRtShs3Vl1Tcq4_P0EHVCSBTxkx17l4yGZpvB3OgOjNpefX_unfdL9FzyieSHUcmSKjAenOEE2xTUvzl6RAagvZIEwLGzqtz1gdUaqKak2GSH0ixp97fomhsuXxvt1FCFx4_1SDOEJqFr1_8ITo3=w665-h310-no)

And here is the Week 6's [course](https://university.mongodb.com/courses/MongoDB/M101JS/2016_August/syllabus) notes:

The aggregation framework is a set of analytics tools within `MongoDB` that allows us to run various types of reports or analysis on documents in one or more collections. Based on the idea of a pipeline. We take input from a `MongoDB` collection and pass the documents from that collection through one or more stages, each of which performs a different operation on it's inputs. Each stage takes as input whatever the stage before it produced as output. And the inputs and outputs for all stages are a stream of documents. Each stage has a specific job that it does. It's expecting a specific form of document and produces a specific output, which is itself a stream of documents. At the end of the pipeline, we get access to the output.

![aggregation framework stage](https://lh3.googleusercontent.com/94DZVWvokpQxASevDZqq1L9tVauVMg20OGfn6zCn3V_PmA7ArWpEbqqnKURY15v3fdKcZQ323ojvKXJ0kPsWPZsLkPElFLW7pRr8suMuHqBOe4lMj1fAJvz0JiZ-qmSS6l51scltQwUEZ3algd_u-MR7Jbd5l9hcTXgQx59ryFjxf1dThIjY85am9BBvyh9baQ4fGCZ_w1QyvlwBrHHIrUFJfuMkFXzxbcva7gYAM5EBAEmmSZkCbBG5oMebhf4z0lWvC1lvWZZ0NOun7onFc-GkmLkZx1JIsh1lRnxTfNTAHSCuG2j3G4Yw3waZGhq7EvNEVRxgQIelEV9kbmBWgsj1Lp809BRzjae-Aqml_uNe-m-S1Y8r2KNRT5K5mAMJLHEKBMRIoTmPUrQsHqGHLAAB14tyeD44n4SnarML44W3u947ugYje1u-XWbfgteLJTreMS0JS09eRx5tCxbyev0RXhwBPVbmnwqZuImFRb1Xseivh3rnGz9qGfJj6wK-JC0Ez54sQp9mYAW4F7BhT8cHEU_zd1naOwMgEIEaeyrfKL0QnPU7hskAEuHwMJ4dnb9STT1gTQ8gIHJ8QjVISWR299erQ0wOFEieXvq_ffB-dxob=w656-h292-no)

An individual stage is a data processing unit. Each stage takes as input a stream of documents one at a time, processes each document one at a time and produces the output stream of documents. Again, one at a time. Each stage provide a set of knobs or tunables that we can control to parameterize the stage to perform whatever task we're interested in doing. So a stage performs a generic task - a general purpose task of some kind and parameterize the stage for the particular set of documents that we're working with. And exactly what we would like that stage to do with those documents. These tunables typically take the form of operators that we can supply that will modify fields, perform arithmetic operations, reshape documents or do some sort of accumulation task as well as a veriety of other things. Often times, it the case that we'll want to include the same type of stage multiple times within a single pipeline.

![same type of stage multiple times within a single pipeline](https://lh3.googleusercontent.com/mWNoePqRo5B6KHaTT_8A9oGoGdTTS-uWCYGJtWtV1e_kRREELGt7LYAI31BKR7isICF4peK1z7CG21QKGh7XJZlnfB55f48SjanovPRTihvSN7FZYqV3rz4Vprpb7t2nyLQcLaHUbSiKKK3SXlZbIkattNe_ISn94u9j2bOcYsXqVHQNPKYuWZ2ndECd-x8d1OMIS5q77q2w7Jo46A4D1JKuFFLf0KncTjb18kif2VUPX67Iq6nlAKGXl2_WEOxGlF4THp6qWbt-o7MKN8caiexQ5TE7SyD5YQE3vZgLyil_bwj801UBp3dltkpZMb5Iy_Hiq4sHCwd9wLC-_rxEMLu1N7Mi02qCkPbxwO2p085UF5zRqwv4rvdN4SHay_8XGOZEVoa9pC0RG3FXri3oNr5mMv6N15CezjpxwG-uM4bTL4W7lx5dr2ecUWiPDLG0_hK3KA03SiNuQpCDIV39_lY55aaXOrTnZO-97hBJNcKgJJgqDGJ7er9PHzofNgej3O38NDvT4Bm0aYBCl0Fa4fWGB9Qq3pD_aHtX09Kkylem8HESLS_zSg1mzWSYfVMr-95sb1zEceFJqCr4cVMod3VkShYDpemVxVN8N4RsdkwguDTX=w1359-h541-no)

e.g. We may wish to perform an initial filter so that we don't have to pass the entire collection into our pipeline. But, then later on, following some additional processing, want to filter once again using a different set of criteria. So, to recap, pipeline works with a `MongoDB` collection. They're composed of stages, each of which does a different data processing task on it's input and produces documents as output to be passed to the next stage. And finally at the end of the pipeline output is produced that we can then do something within our application. In many cases, it's necessary to include the same type of stage, multiple times within an individual pipeline.

# Familiar Aggregation Operations

As our first step in developing aggregation pipelines, what we'd like to do is take a look at building some pipelines that involve operations that are already familiar to us. So, we're going to look at the following stages:

 - `match` - this is filtering stage, similar to `find`.
 - `project`
 - `sort`
 - `skip`
 - `limit`

We might ask ourself why these stages are necessary, given that this functionality is already provided in the `MongoDB` query language, and the reason is because we need these stages to support the more complex analytics-oriented functionality that's included with the aggregation framework. The below query is simply equal to a `find`:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, ])
</code>
</pre>

Let's introduce a project stage in this aggregation pipeline:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded_year: 1
  }
}])
</code>
</pre>

We use `aggregate` method for implementing aggregation framework. The aggregation pipelines are merely an array of documents. Each of the document should stipulate a particular stage operator. So, in the above case we've an aggregation pipeline with **two** stages. The `$match` stage is passing the documents one at a time to `$project` stage.

<pre>
<code>
db.companies.aggregate([{
  $match: {
    "funding_rounds.investments.financial_org.permalink": "greylock"
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    ipo: "$ipo.pub_year",
    valuation: "$ipo.valuation_amount",
    funders: "$funding_rounds.investments.financial_org.permalink"
  }
}, ])
</code>
</pre>

In the above example, we're promoting deeply nested fields to upper level in the output we'll produce from this aggregation pipeline. If we specify `$1` in the quotes, `MongoDB` interprets it as give me the value identified by this key. We cannot change the `datatype` for a value from the project stage.

<pre>
<code>
db.companies.aggregate([{
  $match: {
    "funding_rounds.investments.financial_org.permalink": "greylock"
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded: {
      year: "$founded_year",
      month: "$founded_month",
      day: "$founded_day"
    }
  }
}, ])
</code>
</pre>

In this case, we're taking the top level `founded_year`, `founded_month` & `founded_day` documents and showing them as part of the nested document `founded`. Now, let's extend to `limit` stage:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $limit: 5
}, {
  $project: {
    _id: 0,
    name: 1
  }
}])
</code>
</pre>

This gets the **matching** documents and limits to **five** before projecting out the fields. So, projection is working only on **5** documents. Assume, if we were to do something like this:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $project: {
    _id: 0,
    name: 1
  }
}, {
  $limit: 5
}])
</code>
</pre>

This gets the **matching** documents and projects those large number of documents and finally limits to **five**. So, projection is working on large number of documents and finally limiting to **5**. This gives us a lesson that we should **limit the documents to those which are absolutely necessary** to be passed to the next stage. Now, let's look at `sort` stage:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $sort: {
    name: 1
  }
}, {
  $limit: 5
}, {
  $project: {
    _id: 0,
    name: 1
  }
}])
</code>
</pre>

This will sort all documents by name and give only **5** out of them. Assume, if we were to do something like this:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $limit: 5
}, {
  $sort: {
    name: 1
  }
}, {
  $project: {
    _id: 0,
    name: 1
  }
}])
</code>
</pre>

This will take first **5** documents and sort them.

Let's add the `skip` stage:

<pre>
<code>
db.companies.aggregate([{
  $match: {
    founded_year: 2004
  }
}, {
  $sort: {
    name: 1
  }
}, {
  $skip: 10
}, {
  $limit: 5
}, {
  $project: {
    _id: 0,
    name: 1
  }
}, ])
</code>
</pre>

This will sort **all** the documents and skip the initial **10** documents and return to us. We should try to include `$match` stages as early as possible in the pipeline. To filter documents using a `$match` stage, we use the same syntax for constructing query documents (filters) as we do for `find()`.

# The $unwind stage

![The $unwind stage](https://lh3.googleusercontent.com/JQSpp4ukNmQnAcbRCGF-PfzQtcLuCrXSPiI1ZtOBz6GLHmBhU85WgUf0ksM_CtNcyxMlHDXYfC6fIXSr6KR6zfIr6mhQG6e_aHIHaBZhBXC0mnKU7QJbn67OVfVzkHuQEcZvegnifGCzf9_DnBKYeNUbJWPr2rLNaxXfhIhHFb0_O_waybvY6o4jiQlYUpEFnNVv5t-97VngtsBwHL1XP5sKmhUuSXUbIJIxQKNysX32QWgH4T82R2p538N1rMIpMoBJi_JuGGT09gFX6YOsLG6I2qjLlMMdtzBnB64lpC8_GkIiFshvQ_6Fo0_G-pbGpZKP-G_mqeYpiqF0jCV23ld1vPZP_K2VQoM_hHON80mKBPmSq4-8-ZuJePm7cB_AcE_AFP7HimrC9KZ_WOvyyuNquDnfjgCyNKXAJqpyxgQkycqZKUl3NiEl-6QNMKTuz3nwr3obtkHYb10yWlvijbrSejmZ0Hdb4i_OQX0VC3MkY24081WgGP-DnIYC0CAIWc4OMdqSopEN1Czxa_YK9B1tGSai63y2MpF7H-b8VYb8lrpeCZkXpKPuazkPHmoLzXZOO691ADRq3M1SY1hoGoE13dkf4AUySkXWqprWr4c9k3L1=w1316-h677-no)

The `$unwind` allows us to take documents as input that have an array valued field and produces output documents, such that there's one output document for each element in the array. [source](https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/#examples)

So let's go back to our companies examples, and take a look at the use of unwind stages. This query:

<pre>
<code>
db.companies.aggregate([
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $project: {
        _id: 0,
        name: 1,
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } }
])
</code>
</pre>

produces documents that have arrays for both amount and year.

![project output](https://lh3.googleusercontent.com/IIQAkdNosQFdyCWm4QRSwFcX45-5Eo3mC48rIKKtZsOStC7VllsxXMqrOX9yOH3BE4FGIrOJyxWoBCzEcA15_Yl-FXiBn_rWgvGehqIfceqIWyh3-FRsMviGbtpDOaSkzqBkf9SAdOQVamwAvJS_ssuAETcWETiVpCYSvVt2SQ6geaV_UwPy5LIVB2WtTriJFxL4KYagPyEkOCllkCnQvHDbIPYKqesHUCTl31uuOlpQL8rPZUh2s4uv7FLgkbYHkQD9EiXEL2ExIPDPLFjQ3aNmnzVO7h8a5WY4pOsSVPldZZg3MNPYLysLLbhLWgF1O-qx_bBtP66vgq2YdLnq9l_fhgl6yqY0-71kLVnKA1ZSCCgSc6WUOKouA7wI0H9-771lq41SLFqQuuPlFS_g5RDM1YVUBVTtJgnUMp-M3cNIw-kZz4tF2mZGuUWSF6yZjxjJeGfy-ZlQFzwsmOLqENCmaWXeq05J693xyV3nnrHEuopg350evUllzhNiiloMYNws4K52NPOPOnufwf9onFxa13wYHNRYEnFftcJ4ELPDJ7PFzGDFb9FGFSwvtI7BnIJdelCzb0XT-L39X7gDDyRiv1w3EESRF12EcUOoeUwp-B7V=w217-h185-no)

 Because we're accessing the raised amount and the funded year for every element within the funding rounds array. To fix this, we can include an unwind stage before our project stage in this aggregation pipeline, and parameterize this by saying that we want to `unwind` the funding rounds array:

<pre>
<code>
db.companies.aggregate([
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $unwind: "$funding_rounds" },
    { $project: {
        _id: 0,
        name: 1,
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } }
])
</code>
</pre>

![unwind has the effect of outputting to the next stage more documents than it receives as input](https://lh3.googleusercontent.com/Cmoobrm_U8Pj8Bq6pu3luA9kc8-EDumWXTT1K5UymkHXGXhkZjhjed3ZOZYeMuQB0Q66EjOcspiRaOeaKtcSWoUx1b_-LR-6FI1QfMT6_tA1mEFxk04LIUr8veYCPMGj4W9AwIztSE4fNYFvfzl433E2-A22rP86TwNnvqnxiPy9Cze4GQKQGKG45wulQVuaq9xG0_eEV4QWkoSqRmGYT45ZTC6AtJAVWr8tuYh524a0D1BfengaTOeXewSQesI9S8lWDtaerN1ViyjwzK9AWnMx2U7_ftZC4QbXpLytuRl9uOLUzxQtr0mThiF65YzjFi831oXG6L3710JbMCO0srMjQdL1NHMMOcczXSnKbKoei5OJciAVb5xS35RpfiIy0dt4GBy3u_P4ZYjGx9QA8O9aZJCWn-ZFTnylQ3EvwCdMNZEljzXt-VFd3yarikgzFK4lfQaHhX00AYl5-qD4xGDFnkemq2DZb0eO51RwTSZjIhgit4VAvTU3IdcyFqDe_EHKiX9jt4AuVDOMOvQylO9BStwQmlAflaneCA4iQJiQb2sg8ejzvW1iF2CSXkj8LG7UTzBrF8IGh78KYgX7exI58NtGtsnCVj5uPt9Ve9ohlowz=w503-h256-no)

This is how the document looks like:

![original document](https://lh3.googleusercontent.com/ahadVLSLDSIfwdcYIu0o-MdwGGsf27JpNERF4RJE-naDeD0O7aqlVkWi4kj1mDHjsqRTTCG_bO4192koLbrBt4a-4o75IiTHsGfF6kXnq2iXfC88dXPf0lVW3bqdphCd7F8_3gXKxh3qoIG3O1fsbn284lXhAghSXeC6QMfsDCAVOl9FZWSoNkTt4fxhy2QuwsJ08FtXUMs2zciyBUbqyj62_vUlJHyfhA_ZlgPONXH2s3N1Wvm7TVb92cBUKfruSq29Ih1wnGVXYSQvEvqYaDr28dv6AVZ7R-RJL9lXyEG2XCykipf6LsuoubQrYAEiDmGqkn2WOWPCi0_f_o6cbLp7zZeLzD8nrIfkMf1jgpfDOQsyObksd_me1QVdEpPgZampvI-h4ksSFs0lK0KfLEOJvCAN8NZ42Iz877qs95lor-NNc5RO1kmB0IszI7c1T2mDBM4vjb8zUZMa7qdk0HepKvzxUi9xYlbO_o6PcOeegCK-RKgs5hWlYeB_CJqqf1RB09O_tNWyC9AJsVCdKSpEYGUJFqJ5Y2D6OJRXJ_mM9GZh8EuSI9ra4Rr5y6Jg-RscMefKVh-e2O7NwT61mq4EmTJOV59Oob_c3uo3iVS0Pv-W=w831-h511-no)

If we look at the `funding_rounds` array, we know that for each `funding_rounds`, there is a `raised_amount` and a `funded_year` field. So, `unwind` will for each one of the documents that are elements of the `funding_rounds` array produce an output document. Now, in this example, our values are `string`s. But, regardless of the type of value for the elements in an array, `unwind` will produce an output document for each one of these values, such that the field in question will have just that element. In the case of `funding_rounds`, that element will be one of these documents as the value for `funding_rounds` for every document that gets passed on to our `project` stage. The result, then of having run this, is that now we get an `amount` and a `year`. One for **each funding round for every company** in our collection. What this means is that our match produced many company documents and each one of those company documents results in many documents. One for each funding round within every company document. `unwind` performs this operation using the documents handed to it from the `match` stage. And all of these documents for every company are then passed to the `project` stage.

![unwind output](https://lh3.googleusercontent.com/QEaWqaVrBK_E32vf1f7livxwP0vCmWmubTDMb2Om-Nj-8G9zD0zB-VUfocK0mGw-oVd_Y5PiVqzHBM85CFstH8LBCj5KxfhSE7oOy21pQqB9i3Cb1ZJXSIxrR09K8yisWUTElyDn6v0ylo4GYer-BulP9jQSSLbRc3bHl6zlDGPN2x3hupVVeWLx9ElNeAxSMzdf5xrpaRITIYteJI37Cd_7MnSzLb60titRFd3JJHk31w6fHUTr5RSx1i25i00xHUaLDh0pMDtyVA-Vi8y-vsOIkAC3WSpm1ky0kZWTfGBbc-_C18ZaI3DGo63NjRpfHglYZ5gQ75f07-s3tjsdRCDTBE6GjTolNdthOQJVs8-TR8mPfToENxrRhX0QeXzIgzuObIqfJRlkQoMn0qg74x658k4nbkxsphDQY64EziDCEFOBO5YU5rrhlgDZpNM1OeMeeP2wDv7k3_dBsyTXcr3zjcUQ_XVfloiKeEnlx8i1bsSzfkJd2VduApu-n8u8ZGYqgzuhGqBfVVbQ_OMw1rQVYmezuQ5iGejws6nLVjS7Y-WMIa5rXmokJU65pSpoMLolSKLKd2egy416bIpVKb_Co-z7828PkNh1O20EthPq0bKn=w1324-h576-no)

So, all documents where the funder was **Greylock** (as in the query example) will be split into a number of documents, equal to the number of funding rounds for every company that matches the filter `$match: {"funding_rounds.investments.financial_org.permalink": "greylock" }`. And each one those resulting documents will then be passed along to our `project`. Now, `unwind` produces an exact copy for every one of the documents that it receives as input. All fields have the same key and value, with one exception, and that is that the `funding_rounds` field rather than being an array of `funding_rounds` documents, instead has a value that is a single document, which is an individual funding round. So, a company that has **4** funding rounds will result in `unwind` creating **4** documents. Where every field is an exact copy, except for the `funding_rounds` field, which will instead of being an array for each of those copies will instead be an individual element from the `funding_rounds` array from the company document that `unwind` is currently processing. So, `unwind` has the effect of outputting to the next stage more documents than it receives as input. What that means is that our `project` stage now gets a `funding_rounds` field that again, is not an array, but is instead a nested document that has a `raised_amount` and a `funded_year` field. So, `project` will receive multiple documents for each company `match`ing the filter and can therefore process each of the documents individually and identify an **individual amount and year for each funding round for each company**.

We'll add an additional field for understanding this and in doing so, we'll identify a little bit of a problem with this aggregation query as currently written. So, what I'm going to do is a `funder` field and this will access the `investments` field of the `funding_rounds` embedded document, that it gets from unwind and for the `financial_org` gets the `permalink` (refer to the `$match` filter in the below snippet).

<pre>
<code>
// Add funder to output documents.
db.companies.aggregate([
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $unwind: "$funding_rounds" },
    { $project: {
        _id: 0,
        name: 1,
        funder: "$funding_rounds.investments.financial_org.permalink",
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } }
])
</code>
</pre>

Notice, that `funder` and `$match` are very similar. We need to be sure that the funder is what we have stipulated. In general, when building aggregation pipelines - it's a good idea to put in checks as we're constructing them to **make sure they're doing what we think they're doing**. The output looks like this:

![full output with funder details](https://lh3.googleusercontent.com/2psAv6IgTI_UgQQnxyRfDBEFmk1iQ9OYuAuljJV3RnA5_M_R3BJnTyi-xt1CeLTmn4ShCPhY_2XMwb06mKsNyroyaJeddpIsowrE9vJSkZoqZmRqxm1FG2eD5ICDIEaZ2Dvw1CdsGIYM2vJQhFy9VcdpKotCrYcemm--Zv-drkI1I3UhpaM4pvKlH_6PuHU8dQjXgt8VHLXmt_Q7elbUMcMdhJGjAQ820Y_dOPXElzmnL7kjoavHyBFS0q1I2AiHogKkwcoNTTaqppxjmu_IIy999nWDT4F5mnCMBPs4SuU-PP2Avu42ictBX7b5KNC2fsalTlIydKv0g1M2lH2_zCgtGXBxqBeO0LgWiotj0T-vm_1206zCfIshioPMo6DXu68FvshVAdUiMTUSuO1NBn_yiToGL_cYYHATBqfdG7xtVdqUEzrvYmQNCcjXt5RgVio2M7-RKau9x3mBguS2Lpqlevj-WojZku0VW7r63F0bngTHoIVnpUnsxa1yoXzqIg0XPZxxmFKtx9s0N2Ae5lJ3p6Rd394vrOiSLAgWHep77Gs8G_OLvR8EXmtedwZhpkgcJbgoLEHFbP07IVTVzZ2IbPvlM4VZgWVUUCzOsF5DOQyU=w283-h245-no)

If, we look at the document and look at the `investments` field. We find that it's an array:

![investments array](https://lh3.googleusercontent.com/I8_YY5_Q_UTNQK7iBUkfYCMnLZ0fQrIW4A_EFVels2Cvb3k0rYG7iOy1a6pvsqr8Qe4hzQonGjg_nu-V_ZGVzRDktnOkUJTrg5PTJz3XksEhRN0TE0pv2auYq1naIYb5wSqbyFMAOKGi9zmbcwLT_328_QPDqIyuEz4yyfMuQ0FaSExSNonSP3ooPo1Lsie-SypiLPZsxlvBX_lYplFF9GjLsTHuUdHQUeMW6yKuLyvj_aEQ12eN5UJgrIPTpN_xFTWwwUG25_8Ryy2ZlU-r9mKqnD550jUQx-2n1EYKUVQknMOhEFuzX736ojmpVfRQQ2R7jimAYTfY37G6QhRc5kLXNGNWwDV6Z4TM7OUiBF25ZztPNe4nHQsPE715OD77Gvv_Wq0VEsUsR52rnhmC75w7c4STurmmgOMo8ClSZJVt8FZpsjEGIdsd5h6PvlNcTJ9c1rZHPjDcWFDviclrU9TkSFQZMXNV85UtmgiFIx4CUNXe2pi2XUniZu4FvEkNNCtEUvwg0ORB1FSesbi3nE1aIq1oR4P6xPDTErviRKez1KMz9MIUy3wc3rWIgpJWQZr49ZlzyMdFtOW67VUhlSssOcnrz5ITtgR-0yCuZpjkil-R=w308-h163-no)

Multiple funders can participate in a single funding round.

![multiple funders](https://lh3.googleusercontent.com/yyJWT0lN-_OecyYxitRAatHTv2TZZIS91GgYKSumrs0p3ySLmk44d0p6ZM0CUUUzKuvXtNXF-PC5WctxVb-52PQFgk6GqifOp2HdIBmwzhUJlzLqRXA_zt-fP3ujalNaC3uLcFmI-jKzpcjpgs1UbQ29EMTyqtv7wa6N-tvZCpiCqmNuxjY8cGpEMwzEpTylIq1udDv8nhX3PkvT9MaFRoRgkoaidXLgHFkzrPxh6xX18mxGoPM1ebvUx-Q6OJ6LLCKcyssm5ArBN8M6ZeK6AIFJuFcLzjApo2MDpu_FnlFc0EizSMBJXmzhcYZ92AHckT_nj5INCYNIyUGFCA7uBonjrUz1anaEmCUPQmX9_4W9viNDym_ZCnxRiOcxecnhz5SjLQqtxE9g01FoWsyP6gBIHEJfB_LXOKOxdjksgrCfr45yrS_2mc1-U-8sPeFioCjFpi9DjYWj8fGmJxKgYEnytbz1YY5iRRfG_CYSgalEsE5KpBknRsQw4fH3BSbNBF3-xRJIv65NcZPc_LbfCVvRi0LabV2kPIPSHzzAZJ-O9UTZCaBDjw6AqlG_fz5ClVmgju1-iRtQ-G75pGA0Pjrj4Ia0eq1rWEc-c8aLhE2yQGf4=w380-h305-no)

So, `investments` will list every one of those funders. The output, as we originally saw with the `raised_amount` and `funded_year` - we're now seeing an array for `funder`. Because, `investments` is an array valued field and as we know, the semantics for a project, on an array valued field is to produce all of the values for whatever field we've stipulated.

**The above query returns companies for which at least in one of the funding rounds, Greylock participated in**, what we'd like to do is **constrain our results so that we only see results that Greylock participated in**. Not, all the companies for which Greylock participated in at least one. So, in order to do that, what we're going to have to do is figure out a way to filter this further. One possibility is to **reverse the order** in which we're doing our `$unwind` and `$match`:

<pre>
<code>
// Add second unwind stage.
db.companies.aggregate([
    { $unwind: "$funding_rounds" },
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $project: {
        _id: 0,
        name: 1,
        funder: "$funding_rounds.investments.financial_org.permalink",
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } },
])
</code>
</pre>

This will guarantee that we'll only match documents coming out of `$unwind` that represent funding rounds that Greylock actually participated in. If we run this, we see a **slight delay** - but then we see that Greylock is one of the funders. To make it more clear, we can include a second `$unwind`:

<pre>
<code>
// Add second unwind stage.
db.companies.aggregate([
    { $unwind: "$funding_rounds" },
    { $unwind: "$funding_rounds.investments" },
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $project: {
        _id: 0,
        name: 1,
        funder: "$funding_rounds.investments.financial_org.permalink",
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } },
])
</code>
</pre>

Which outputs this:

![double unwind output](https://lh3.googleusercontent.com/76FS_Pi3aVLXHA_uNgGeSKCB5ajb5xGmX9oSeaa4kg1be89iLn_m132jiR229YRdpC7WfLrBKtqRa2N57lUTH2xmsqLu4z9Gydwrzmudr0oQGc6BDicOgtdXlPKR3xfoOOjAodcKE4ocOZ4epX81moowkp-C_nMr6jMO--0iTSaGeNdwHXNp68LFuzGd_gKtB7Ky1_T60g633QBI-RJCFR-o3DXWcbm7V_tyfduNDIoCOEXX4NDopnmwaTu4sqXP3HHH9MfdaPo5yjjs66A9CaYv_DXHhmnKQIWzlixr_pcpwAGvq4d6zOWipePqbh3rmb7kx0Jd8AvjEwQOJZBRRn0TInaKczLNjsIFX_UoNLhqhF2P5cdKBY88r7tiCDjs1OuQnc-64ZPgmDKXy_nWV8SCv6jqlhdbe_TwsmayiaOQwl3NbY2TOD0c8bDTHvpmlc-vRg3qt5AUY6cmsyfXkxSpc_ksR0uegq0MwGN7PtoJ01Tj6fXtnvAX0MqtpwT5LjHOxgYp43yCc1lpdC8u1wKNRRlWW2JyMjJbC8YHnd6Sx0HkR0yfR2l35BwBnjeTJL8NPxbCXVcuP0R9E2H2yq4CB-h7RF2FrokFP4skkz3KAkc6=w254-h218-no)

So, what are these two `$unwind` stages doing? Both of these are running through the entire collection. However, the `$match` operation should occur as early as possible. So, that for each stage we have least number of documents to work with.

So, what we can do is - leave the `$match` filter as a first stage in our pipeline and simply include a second match:

<pre>
<code>
// Instead, use a second match stage.
db.companies.aggregate([
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $unwind: "$funding_rounds" },
    { $unwind: "$funding_rounds.investments" },
    { $match: {"funding_rounds.investments.financial_org.permalink": "greylock" } },
    { $project: {
        _id: 0,
        name: 1,
        individualFunder: "$funding_rounds.investments.person.permalink",
        fundingOrganization: "$funding_rounds.investments.financial_org.permalink",
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
    } },
])
</code>
</pre>

The first `$match` will return company documents for which Greylock participated in at least one of the funding rounds. We'll then unwind the `funding_rounds` and the `investments` nested array. And then finally filter again - so that any funding rounds, any documents that represent funding rounds, that Greylock did not participated in will be removed from what's passed on to project. **Sometimes, we need to include multiple stages of the same type**. This **query is a bit faster** because of less documents.

# Array Expressions

These expressions are used to work with arrays and can be used with project stages. There are a couple of different array expressions such as:

 - [`$filter`](https://docs.mongodb.com/manual/reference/operator/aggregation/filter/) for selecting a subset of elements in the array based on a certain set of filter criteria that should be passed, in the documents, passed to the next stage in the aggregation pipeline:

 <pre>
 <code>
 db.companies.aggregate([{
   $match: {
     "funding_rounds.investments.financial_org.permalink": "greylock"
   }
 }, {
   $project: {
     _id: 0,
     name: 1,
     founded_year: 1,
     rounds: {
       $filter: {
         input: "$funding_rounds",
         as: "round",
         cond: {
           $gte: ["$$round.raised_amount", 100000000]
         }
       }
     }
   }
 }, {
   $match: {
     "rounds.investments.financial_org.permalink": "greylock"
   }
 }, ]).pretty()
 </code>
 </pre>

Here is where things gets interesting. We're using a `$filter` expression - it is designed to work with array fields and has **3** fields we must supply as part of it's parameters, or this document that we set as the value for our `$filter` operator. The first is `input` which is an array, `as` specifies the alias we need to use for the `input` array throughout the rest of the filter expression. And the `cond` parameter will provide the condition used to filter whatever array we've provided as input selecting a subset. In the above case, we're selecting elements where `raised_amount` is greater than or equal to 100 million. There's `$$round` - where `$` refers to a variable named `round`. `$$` says that we want to **dereference a variable specified in this expression**. This is to disambiguate the reference to a variable from a reference to, say, fields in the input document. Returns an array with only those elements that match the condition. The returned elements are in the original order.

Let's look at [`$arrayElemAt`](https://docs.mongodb.com/manual/reference/operator/aggregation/arrayElemAt/) for returning the element at the specified array index. Let's pull out the first round and the last round (maybe for comparison).

<pre><code>
db.companies.aggregate([{
  $match: {
    "founded_year": 2010
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    first_round: {
      $arrayElemAt: ["$funding_rounds", 0]
    },
    last_round: {
      $arrayElemAt: ["$funding_rounds", -1]
    }
  }
}]).pretty()
</code></pre>

This requires the array name and the index of the element which needs to be returned. 0 means the first one and -1 refers to last one. -2 would give the second to last or penultimate element in the array. The output will look likes this:

![arrayElemAt output MongoDB](https://lh3.googleusercontent.com/jbmORWw7GdoYCVwpjK8xMSlI3ZrwxdendKuhNTg-t25RnY98xAeDeBLkOispOhYyrGJRzSLBOz2ml2JiYKNFD5sw151gAcSHojE_cJFjf3b5OnM4v6J-PGegrdQRmd9_7Zv0-JMrTcpirTkW9gqWGQqKtA15A1ayNLAm3C-sM1fvDWErvD4A_9dRRm-D84_-BxJ2syv6BQKqfb7rfJ5ANjAFvWfaZz_onKoJmS7WszDw1ccjFIVSeK3lKoAwiFMTAlpsn1IuJkYTei6c87HiW0F2m7TaaHa4_49yvlek-ElshOGtD9Rxc4v7eJhsyJ5_6pMqyrMIUlB1rU-fEdlLYJJJDcdfOyKDRXQ3ahbdPjPrm3keiX1mxXcd5jrD9qGcCXvH8e8MVGBXkAahvRF9woXhsHSmrcPWyP5Sw5XwMpC8ghCKFZTiKvQEaaGPldm0Nbjgxl5U4pUVjNCvx8ZL18VVfZOVKtVywqoEJbJu4nrf5YZbyCcAV3BjAZQ-ylxmmxK0biKblZ9gpOwej5zGFrMbr5Me_OPsKr4M3Ljbqtpf2XfxHlktE1MxqeXgoshxrAqlX39DlfgXH-wZBLjIPnOgthObM4vyilFelNPV5rJyuh7h=w387-h344-no)

This can also be done by `$slice`:

<pre><code>
db.companies.aggregate([{
  $match: {
    "founded_year": 2010
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    first_round: {
      $slice: ["$funding_rounds", 1]
    },
    last_round: {
      $slice: ["$funding_rounds", -1]
    }
  }
}]).pretty()
</code></pre>

Now, related to `$arrayElemAt` is the `$slice` expression which allows us to return multiple items from an array in sequence beginning with a particular index.

<pre><code>
db.companies.aggregate([{
  $match: {
    "founded_year": 2010
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    early_rounds: {
      $slice: ["$funding_rounds", 1, 3]
    }
  }
}]).pretty()
</code></pre>

Notice that the index is 1, **skipping the first** (which is 0) funding round.

![slice output in MongoDB](https://lh3.googleusercontent.com/9pR9sntbgYGEn55vmdQxZclfgrluLL-HJZN-db1h5IUvkioZh4iacHDOos01l8opC46mnhs-u2Lx-IbhRblSl7dkaazxD8t25YuQ3xPHFzVXjK9AlVoU8dp1PavCGNjqM9cQ1F4zXHIapkvmhRqlhB6OfSZ8YZ0ELqETQB0mxcs-QlgAJJZcD2c6Vr1iTcfn7MtXV-r7dF4Vofk5VnK0v6F33lhECRYKcj7Z1j6nICfw98bE0OA58UrSnM_xdbdlLdXqeutuQkn0aVXIHGMFrwIE4920VosjQX8k5k9F12oWD1aBI8EYCHMmwKc1MJqrAYHwMVHF_TNkCzamLeZ-C-2mPKzQMikJhkfbj4y1rZy8mm8oyziK0VWSkThVN8GdUajFWcuX1Z4uqC3D8Yaenq0aBjdRiFVZN5jxEkJkkBuAI_UQYin452KKmjuwdJR4dn7jRkCvBG-NgCeAwJUteUfhygbhVhsJk2DWhcsTEf_XAjA-LDbNNsiY8xJ-i3JuWTQaKI5vyjc1tIwRtlvSi6ctmjbPP5_OyjQk18ePEC-4AGW6T0229_B0w906xPK1vzjoVa4prXaQ2_RwzdX6H0PxmgSnTZlMIQCwOhDzjmBBAGGz=w451-h363-no)

The last one we need to see is $size - which simply returns the size of the array:

<pre><code>
db.companies.aggregate([{
  $match: {
    "founded_year": 2004
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    founded_year: 1,
    total_rounds: {
      $size: "$funding_rounds"
    }
  }
}]).pretty()
</code></pre>

![$size output MongoDB](https://lh3.googleusercontent.com/BN7z1zh7kg2HmGtqidwYad_KGYtrbERVXexoVbkHackZMWe2_mhD4OgYx83hkXDuwyVS-WYF4ptPsiVCKNlqDH_CWHSYygIDKAb7WQthnb4tx0v4e_aXwFG_qb2iJqDyphw8kjwpZTAfz5V0dPhcWS7_fRMDMhhdcYM_lsYGJIS4_tkqkx75sRlQV9U4VS_h62msxE3cwAqghxoGO3Q7aHbBkI3JqYEw1V6cBOveaAlxUIxm1aRT57Q_z4OxG0I2GXSNmBn4IqtM1hu-mm3wlILzd_PKxxqSclJSMakB7ET1W2HKZGoGpPxiidES0ii2__DMaHCqQoj6TYzzGCWdRv6Rn3RMaVJPHhxKJHXMzLY6qM6uMZ_KAb0DwmWnwMBWHze2YUQkWk88k8xJrPVYb64P-DOhLsEOgoxALVyPINicIN3_QUrdLtOPO8b_MinfoRXUG-sVH0sOERtDlZyANJuoJTE2WJEbtPTmQM7d2b-by2NkIPlz1DR5kTH83F9GKf0zFRhuUf2VoLXWS-XF5IJ49VbE_7QT7MkVQ-BLDtzA9IcCa_ub_XiIBF8buC5M6jTzFtrJCzgxMfYZLmd5EA0VKiBcbj206D347LZNPOVLyHgT=w580-h90-no)

# Accumulators

[Accumulators](https://docs.mongodb.com/manual/reference/operator/aggregation-group/) are another type of expressions. They involve calculating values from fields in multiple documents. Prior to `MongoDB` 3.2 accumulators were available only in the `group` stage. We've ability to access a subset of accumulators within the `project` stage. The primary difference between the accumulators in the `group` stage and the `project` stage is that in the project stage accumulators, such as `$sum` and `$avg` must operate on arrays within a single document. Whereas accumulators in the `group` stage provide us the ability to perform calculations on values across multiple documents.

# Using Accumulators in $project Stages
There're multiple accumulators. The `$max` accumulator gives the largest value from the passed in array.

<pre><code>
db.companies.aggregate([{
  $match: {
    "funding_rounds": {
      $exists: true,
      $ne: []
    }
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    largest_round: {
      $max: "$funding_rounds.raised_amount"
    }
  }
}]).pretty()
</code></pre>

![$max operator in MongoDB](https://lh3.googleusercontent.com/Xzc8vJ4nLjlkIg_kNudODemBhi8LWJiT59F6b6KlooRsHiByKghGdE1wdTWZ2P07XRZS9hG3YuWWKphINh0PExnNRlzFeeeQF699EF4QUwWnNEE-sP2h5LuFbKggmVj6uRQ3AUQLrMVKFqpOPVsMxEsEB8ja7zguagxq9vBKyMA-zYnd131E1TLCONU2pmkZHmQw7uegmUI8TnJxj6pn5vtuu6x6L0hdZah0fBaaUeFL6-31-hDV47D9HTkORcjd4YBlTKmvLmvXq0Ehx3xweoNhoQuUKvQ39GN1GPiAQgmbc_zkxmjV923cEeGZVIwWKiaSXUy73q96o0DY3v9pf_CFBmc51kItw1f4vP8bn78ilCk_kMVbBdAjiaNyfyhNagHf0kDM4e3jnE4dvYVHbNgqOIDA1eU7iI1F4kxZ6xuYBdSREhxhuR0o_uH-iTtetO2g7M1DEua-Lb3L6oJ4xZxxA5-AUcHiVjF09pA_4Gm6hoDKwlPSChnENhD8h9FMQ3H9eyUpfQTvg7vw-GfyPwMrayLavpsn1HnrVJMat7_CSjaTY2Dd5uSYJsdOjJFRdW9VSAynHImsLXMT4zfFGRjx0ftr8UdgXIKUmBUGuw2DWufp=w465-h114-no)

The below examples shows the uses of `sum` & `avg`:

<pre><code>
db.companies.aggregate([{
  $match: {
    "funding_rounds": {
      $exists: true,
      $ne: []
    }
  }
}, {
  $project: {
    _id: 0,
    name: 1,
    total_funding: {
      $sum: "$funding_rounds.raised_amount"
    }
  }
}])

db.companies.aggregate([{
    $group: {
      _id: {
        founded_year: "$founded_year"
      },
      average_number_of_employees: {
        $avg: "$number_of_employees"
      }
    }
  }, {
    $sort: {
      average_number_of_employees: -1
    }
  }
])
</code></pre>

# Introduction to $group

`$group` is similar to SQL Group by command. In the below example, we're going to aggregate companies on the basis of the year in which they were founded. And calculate the average number of employees for each company.

<pre><code>
db.companies.aggregate([{
    $group: {
      _id: {
        founded_year: "$founded_year"
      },
      average_number_of_employees: {
        $avg: "$number_of_employees"
      }
    }
  }, {
    $sort: {
      average_number_of_employees: -1
    }
  }
])</code></pre>

![$avg operator MongoDB](https://lh3.googleusercontent.com/uQ1ZUarX8PJ9XytFlKr4gOjnGVuoWpFrLw42WiOj1FGADly5h9Hu_Yal3iiRdTpsTmdh4CR7OCB-nCBae5iNoxHhdIdJvLw5tEc-ovF_ZxxjrF0TFRb92rEHeS3eH981Fg9FybqCsyElwJEzlSRf2fENCOLM86TDaNdNSdYDzbps2arTDO_av_sOO6mR8iBgDQHHhSjBVVs6csLOHuD--AHoBrAr9pX0uSvCbBaSEVi--XUpmfZClz4cI7sFZunkv-ndzwVqcKbPH5Nl5lEp4NPnXDVVf5WS3wMaBgpelpPhchX3OI8laH9_2bW1JOOXxVF4G0GiiHD2pYjiyGQvUEiWwOn1AWhVlUjcQolNoTruHPXoykTYf6i3M00ihpM-fW2MYi28ZKbWM4PynZ956vPcd8Ah3gjBkOBWlyw_08p_FfeXAhbekw9TV9gFWkcCxsNWTDwS2XOvDb9nhxVPEYWsiLWm1NvgJDprdA3MYVxvc1J1o3fjkSEldpRrTGpQVu4RJu7KGm7Zj-fCVky1_6G77TP2a6U6hh5A-NxtZhd9MCLwCvjzvF3T_BsqXfUBLO2KcdpKZZ7B3HmdsrZ1SHIdlejtcVBrfSWb3BbHqurlw99c=w626-h102-no)

This aggregation pipeline has 2 stages

 1. `$group`
 2. `$sort`

Now, fundamental to the `$group` stage is the `_id` field that we specify as the part of the document. That is the value of the `$group` operator itself using a very strict interpretation of the arrogation framework syntax. `_id` is how we define, how we control, how we tune what the group stage uses to organize the documents that it sees.

The below query find the relationships of the people with companies using `$sum` operator:

<pre><code>
db.companies.aggregate([{
  $match: {
    "relationships.person": {
      $ne: null
    }
  }
}, {
  $project: {
    relationships: 1,
    _id: 0
  }
}, {
  $unwind: "$relationships"
}, {
  $group: {
    _id: "$relationships.person",
    count: {
      $sum: 1
    }
  }
}, {
  $sort: {
    count: -1
  }
}])</code></pre>

![$sum in MongoDB](https://lh3.googleusercontent.com/VxlQ5BLNDRxYL9sBNHCFzY7GMhcS4B48_8K27wsBRPcgUJ9SBERPZgHjVuXVL7_G0NWKZfv6Yp_LH14IG_KqC7qmIRJNEgfCDgAM9CkanRQxQ-3Gddth-p_o3mmn7AkecMtpUPPEKcr5ZaQ3-HBBDTsiY4ojiHIZERscBGT4MTP3hfYQraG5Og5p_VZKW1j0NmLlv-Y2cXeo_Xo2uMi5S39j827C-SQo1avlUL240qA_mc3orjeTipeYJvIOAexiZKItWcPTn5_iz6-7YHQaQ8ojKp562tzbP50NDmdHDvByRMzLm5X41kWQWPOVzv4vwidAv8LkWaE8eonyd1a9d1MOUUZlu11GLwuADesqZ93Sn7rAkUgN6Qu4uB8pan9CLfOozgufmxJ7EVVqxaQAacqBP1BIX7JaFY7ku_nwID-xk25klYSoCfiANLTmhCZewVs63Gso52canottIwRUN384-DVeKZ91RaOeN_pzgnxZ-2jotOvlYl7TwRLmkvZHwOybGyMXMaZxPWlUHUuk3fyIr37STLV5R-X6lm58ATpBeL_QYWbq52bMYMfcGQD68nby0L5EPIDEYvMPwr_dJZiKMskVfeiBphUginEPfTGsfp2U=w359-h194-no)

# _id in $group Stages

We're going to understand the `_id` field within the `$group` stage & look at some best practices for constructing `_id`s in group aggregation stages. Let's look at this query:

<pre><code>
db.companies.aggregate([{
  $match: {
    founded_year: {
      $gte: 2010
    }
  }
}, {
  $group: {
    _id: {
      founded_year: "$founded_year"
    },
    companies: {
      $push: "$name"
    }
  }
}, {
  $sort: {
    "_id.founded_year": 1
  }
}]).pretty()
</code></pre>

![MongoDB $group with document approach](https://lh3.googleusercontent.com/cZdysCDFCMxAH0aA5UaCSKgsa23oINU-cC81I72xoB-dJaTYoCAC_Z29Jbf4DYgCPPnadfThclubc4d6bYGEGKI40-mp-Nqh5NSKezeS1W6HHzy7HCVi-BYLWNf2Qzo_lGtvDEjdS1bijrMao9pimLRSophJHrIeF0yq4DcutY6CG9l1DUarH4Chz1jjzcozOkgsU44W0AoAVX413CzX-Bm4hwR-z_XCNXDMAAuJOJUgm5tSGAyvanCbegqFc5MIH3bcwY21-BYlr2PZbX8wp9veq2h6l9Igiu1Ghw73WxMwzEKy7Q1smjigWNJUAwNJArJxdahO-WeWLDtNC0rQltt0Q5-eeKtei0I1Vr117qCyerREiUunDyZt7cOK9rDI0BqoFGQKaAuST5XK95BrUOj-S7PP-YcpsxiQmWQZgOilr3x-muwxy48MxM-qhvEkFYIWbDjS_H5RzRY17jJkFgPStt8WkbcNT6FwOlNLWhW3pXm0tbcvP37jOzZy_IZvatZEcYpCSuiYrEMvqdDB4tmV6kRcIxbaZ3wlZL-zGWopfo98HyLQqziwowKhr1v3Fp1ueY_m9mSOG3vH2dnj_wM384TaB5IB3Pxwjm4lTHSbkscK=w323-h246-no)

One thing which might not be clear to us is why the `_id` field is constructed this "document" way?  We could have done it this way as well:

<pre><code>
db.companies.aggregate([{
  $match: {
    founded_year: {
      $gte: 2010
    }
  }
}, {
  $group: {
    _id: "$founded_year",
    companies: {
      $push: "$name"
    }
  }
}, {
  $sort: {
    "_id": 1
  }
}]).pretty()</code></pre>

![MongoDB $group without document approach](https://lh3.googleusercontent.com/wt6rd44VLJdMXAM0_bafbHEEAH9r5DZvE-Jurpe3FM64nWQtk4XFTInfjYcc93c2n3Ms-r9hykOLXqcGCkhk7cQ0jyFgfBw3XZSVaOhZ94DxsYlMGXE-kXjhLu-rtcNDzqZ8_9K9GHGexwH2I9dX3jalSPIcoprKv6Noqo6whMZRAsmNZt93gimVP6q5kYFbly0LTWYBnh4c3qnZE0q1OounH6pP_KmI0k04WMuvRUvr7adIrXpslRIW-Aq6QrpV3HVhp398cQtW4mT45qqru2ZiTHaPVJCJ2sV0fqboJbKYweG8LcTlraBaNLj0vfMG-SGElc6PG6WhU5C7-i1ZMMqu60l9FlPCyKG3AJacqhAeiCefTC3vbB9uZ027IS0mWhSuwhRrMmy-hsjlBBLplGJ3Ry88fSwroNqlYxOFSlalmse--PP91BXCTW_DH_Kt19Iw2tRr89EyRQ2aurqZkP0pPsdLJppbS7HegGTmBhaAEu28ooFDAXT9mUZrIXBL6ObwtktVpLAsrRlg8o9P9iIwTDIiHebewSUG57VoC3BsEZE4pSOhK5lyLBdaYGvnc7LiwzHQS8l9yCSpmnInaSQ9LB6zgAfM0Skr-ig7B29y1qZd=w322-h220-no)

We don't do it this way, because in these output documents - it's not explicit what exactly this number means. So, we actually don't know. And in some cases, that means there maybe confusion in interpreting these documents. So, another case maybe to group an `_id` document with multiple fields:

<pre><code>
db.companies.aggregate([{
  $match: {
    founded_year: {
      $gte: 2010
    }
  }
}, {
  $group: {
    _id: {
      founded_year: "$founded_year",
      category_code: "$category_code"
    },
    companies: {
      $push: "$name"
    }
  }
}, {
  $sort: {
    "_id.founded_year": 1
  }
}]).pretty()
</code></pre>

![group an _id document with multiple fields in MongoDB](https://lh3.googleusercontent.com/Dp75pUue_R3I8DI18FVuErEUeBNBomiGTQcVO45FoBeHgu9H_MAfGSpgmxOyVQddvuNTnv_oDMIoQWMsrQKmETdDLjBk8Yj6vh8cLmxrpbZd6u2g2qBJWkgBNvQRKVIpflDo9-7-tdOhneJ6QC_DqC4Nhb68Yac42rlzNeHjlrz8lKYLZFJMQ79m3dodgI6bI9JGHHKPfdHE7X_ypVxbARpqvYO8J6lh4Rtg6VshULFnskCQHBQYsCXfs3RtSaNi3t-D5dGSbf7RUuoTFaXxWGco6lBiALZze8Dfnen2wPHhTVDzqzDthR1o7NwB_VviKSMtFHZsb8B9lxzRy8X3DxCx297p8qG1R6xHKbw5lG5rawpIs-HCBkreXavm3MDwhrLbAnZuimFLTzVqxYBeICKSX1uCnzRKNKZkUAdhSDm4tof4nAJkkkP5RcOU7r7dNGLUMiK9bdHqqZVoTLopwRY8dcSW7OfPky3kyk5LKlGAG2jUJBaDY95WojrnSkZ2e8f7m6oocAaXPevZ0oqpg_Tp4jAoftsUoqcr3az3_3vL1JPweM3eNnyQQWIQUrvsOOIEGO3DWYTDE12zEy0ZBeoVNWVgNKINz0DA-aADQNVVL0aP=w354-h219-no)

`$push` simply pushes the elements to generating arrays. Often, it might be required to group on promoted fields to upper level:

<pre><code>
db.companies.aggregate([{
  $group: {
    _id: {
      ipo_year: "$ipo.pub_year"
    },
    companies: {
      $push: "$name"
    }
  }
}, {
  $sort: {
    "_id.ipo_year": 1
  }
}]).pretty()</code></pre>

![group on promoted fields to upper level in MongoDB](https://lh3.googleusercontent.com/XqzUb0ni8-HrWSEsiUydzqXjJX0snqmU5NaHaZzKoubs3iy8Zp20F18g-fKt3cSiJucKtAkc72L2I7LI0BWrWmCL29ZmOZueKt3HCcONkTVnwRWPXkHWmotQ8-8ebeN2rKIYP0J6GWbfSQkjVq4vTgnoqnSIZv0CSRhSbh3NhjYv8xLxSf_bYvP6QNGUndBbJPwlE5wmCCpmiuNhVRgTz3XNkdYFsjbzzFUSrarnNtls9k9WnLMRlyx8_VWP-7iwWoQHY2WlLdff7VNAUF6IC4ih0mA8wV6GxyX5l_Bw9AqRj8rCgeDhGCpNzteUg0WTfxae0xyVqe73GjaA-o6j9mx-qch1RC1gf1xWXUEhdcxz2hBlJS6JjXPW95o43wNr-YJm-TAyp8Y38aLe7vgw75fO6Jl5mq3AGnoBrBFqceK6luEhe76QupAPQalWabE7JDAp4dEZ3ruvX7998vHR1afrShPG1DyP8DN267ef7UookJNbpq1scFqbX5DxNQZqCYZ89re5uW3dKiDq-Hqnx-h9a5oCLJ03HNapyg9i3T3e96hsPDAiIWahlQ0b_33jzZhiT1premDidg3pLIr_DHniV0YVSiK0Sffm7hN4MUpVlOBf=w280-h123-no)

It's also perfect to have an expression that resolves to a document as a `_id` key.

<pre><code>db.companies.aggregate([{
  $match: {
    "relationships.person": {
      $ne: null
    }
  }
}, {
  $project: {
    relationships: 1,
    _id: 0
  }
}, {
  $unwind: "$relationships"
}, {
  $group: {
    _id: "$relationships.person",
    count: {
      $sum: 1
    }
  }
}, {
  $sort: {
    count: -1
  }
}])</code></pre>

![It's also perfect to have an expression that resolves to a document as a _id key in MongoDB](https://lh3.googleusercontent.com/GrLY0VWm7RExvL4So548j-OPoeBlcB4t8YlsPNfWuvM1zLHEwf2XaJly-Cg-wqu8_avEz3qYiYvY2quN3q4eVnok9DhAwAF8E-MPw3q1orDOipb-9mXnLzZPdNgIyAlVPBo3oQuPChXa1flWvNNz9xLD1QHQN_H4UiEo4SB2FONhMZ5QlebWfSSPiJlpE4LJupomYINf1kiFx-mD2p_Hfol7HB2VZEUxT4kgOlHo02hvXWh0k-CHr7sloJXnuEWM_cKIajOGyZLVbfsgEtf-2lMLJMQOIqcPP6fJ54sWjsVr2dMD6b7QtBUOgaR0E_-z_8Zik9wkHA3d6ShpUuPUaFpbHPre8UwVCRVOBcTuryn8JoRTHrVso4HshELeNp4XZTnz1oFDVKdFSOJ3eawiO3_0SWaNr6KJltgxAOAODX80nYp8r7rawWtMiCSX_GgmV7UELNKHemACsoykNpmTjqc5eWBx0B_HuhJmxN9sZY2Y0pDmaQdOwzKPMTTBFZyrwyLEAegARNM3DcEi1suRWnJWJZBhcpArVNggHpstSMK9BbM-fdvUcR6pGdtXE3a4_S6A28zDf68OqELWuFzNe5WMW1scoyAkg4svzvHJQZ_aCCdx=w346-h101-no)

# $group vs. $project

Not all accumulators are available in `$project` stage. We need to consider what we can do in project with respect to accumulators and what we can do in group. Let's take a look at this:

<pre><code>
db.companies.aggregate([{
  $match: {
    funding_rounds: {
      $ne: []
    }
  }
}, {
  $unwind: "$funding_rounds"
}, {
  $sort: {
    "funding_rounds.funded_year": 1,
    "funding_rounds.funded_month": 1,
    "funding_rounds.funded_day": 1
  }
}, {
  $group: {
    _id: {
      company: "$name"
    },
    funding: {
      $push: {
        amount: "$funding_rounds.raised_amount",
        year: "$funding_rounds.funded_year"
      }
    }
  }
}, ]).pretty()
</code></pre>

![$group in MongoDB](https://lh3.googleusercontent.com/iP9Z2s3BhkLDDkkNwvOG8PhmdkUn4vfCDjxflG41nvKIiwiUsJj4tlojJS256qmu3OD_5jL7nJdXj3HPyB6s7wYdqjTt9sAKwtjW-cxSW2pkUU_uE4CKSryguEq_T8KxmV7chfDxTB06TqVrHrZhj7HNne0xdbt3ybgdnMurQvBTCEMiV01_qCaXT9-NjBhQLCahcFqlfpM17Jk65I1VOqPZGUOdtInqKHCZ8ikAoZmyYP6wMThL6CjHHaf5rzjFrP1RQs8wVwN7xJ8J95EYSOIGbOXuFLwnxvU8HgOLF-QAE_YyII3aRwws-sdAD1F8QP5mZMBJKk8pdbcwtBCJRKkC98Uw77vCUOpfkQI9t-50Agv-0mxZkfb8VCh-Kk2z8YU64Czp6UwftiEVdH9qIHbtGhz42ZPvCKNTHOlkxfZDBKty_PguxuqwSBT1tdzUkE22GTF06WvmJEJBZRnBZnaqyILaN3EpZKZk1BS67bBlH-1bfCQA1I4YQnfgg4zpaLyvjaElZEPo-Pg259hFnwMN_avT9PYNwQl3a4k8aqhQlQtRS3QRzBjK4tuoAFDpHus-rlBqzjv5Top3y-y65TKSlGp16U3MkuWE0pzD53aJfuoN=w366-h134-no)

Where we're checking if any of the `funding_rounds` is not empty. Then it's `unwind`-ed to `$sort` and to later stages. We'll see one document for each element of the `funding_rounds` array for every company. So, the first thing we're going to do here is to `$sort` based on:

 1. `funding_rounds.funded_year`
 2. `funding_rounds.funded_month`
 3. `funding_rounds.funded_day`

In the group stage by company name, the array is getting built using `$push`. `$push` is supposed to be part of a document specified as the value for a field we name in a group stage. We can push on any valid expression. In this case, we're pushing on documents to this array and for every document that we push it's being added to the end of the array that we're accumulating. In this case, we're pushing on documents that are built from the `raised_amount` and `funded_year`. So, the `$group` stage is a stream of documents that have an `_id` where we're specifying the company name.

Notice that `$push` is available in `$group` stages but not in `$project` stage. This is because `$group` stages are designed to take a sequence of documents and accumulate values based on that stream of documents.

`$project` on the other hand, works with one document at a time. So, we can calculate an average on an array within an individual document inside a project stage. But doing something like this where one at a time, we're seeing documents and for every document, it passes through the group stage pushing on a new value, well that's something that the `$project` stage is just not designed to do. For that type of operation we want to use `$group`.

Let's take a look at another example:

<pre><code>
db.companies.aggregate([{
  $match: {
    funding_rounds: {
      $exists: true,
      $ne: []
    }
  }
}, {
  $unwind: "$funding_rounds"
}, {
  $sort: {
    "funding_rounds.funded_year": 1,
    "funding_rounds.funded_month": 1,
    "funding_rounds.funded_day": 1
  }
}, {
  $group: {
    _id: {
      company: "$name"
    },
    first_round: {
      $first: "$funding_rounds"
    },
    last_round: {
      $last: "$funding_rounds"
    },
    num_rounds: {
      $sum: 1
    },
    total_raised: {
      $sum: "$funding_rounds.raised_amount"
    }
  }
}, {
  $project: {
    _id: 0,
    company: "$_id.company",
    first_round: {
      amount: "$first_round.raised_amount",
      article: "$first_round.source_url",
      year: "$first_round.funded_year"
    },
    last_round: {
      amount: "$last_round.raised_amount",
      article: "$last_round.source_url",
      year: "$last_round.funded_year"
    },
    num_rounds: 1,
    total_raised: 1,
  }
}, {
  $sort: {
    total_raised: -1
  }
}]).pretty()
</code></pre>

![group vs project in MongoDB](https://lh3.googleusercontent.com/mRiC7j6YFAk080yqyikHn0jyUO80jb9JT6dOgD5v6Gt6VRvbnVN4mr5YJs4t80zVhflyJMtiQJe-edk7RJcR378OkToVa1Wh5mMSZUTHp_9s-uGHf851eVOByztPWZZ8Xhpcl2r3-MsK45rY5yg2SI5h6nVhCpyvfHl1o55sgkKc-9p_1MsMIZlcYZG9J-eSSxCrQP0rl4LaAdxWZ72fZ5w7FstYRYPrUh1cG9OTZPncmoFTA2mN4IfRW201QBK2Xt4AvhKRBbwXyPc4QfWPvTU8j25BImEKyWbtKynluMMhRmLl8dUuZYAXznNZFegQ2yIwV3PZZLIYfg0JFrec6_gGvqZbdSpNzbyLzmOj6MqJJJyBS4r9Z_7NnUH1_gw6oTwu1z6dJVpvaF6wB5wuC9tsxiV5hxXfI2q7mPMwVcq6rECoRH-IMyOgK9gyI34HUirWEaZoV4cdYmrOCh8DhWuYt6ggGrejTqEOfbTyORyMQVDfoxytqrElabsN_ZRHUqurPpcu48h1gKTyv8SwKK4sgPKbtw6fxZOs2A0_NEKsxGNfSbrGWHQCuswTOPLoWS9t5X3lwO92UxBzBr74G9NkLJpEQO1nzOn4B4omClDeLO1P=w642-h207-no)

In the `$group` stage, we're using `$first` and `$last` accumulators. Right, again we can see that as with `$push` - we can't use `$first` and `$last` in project stages. Because again, project stages are not designed to accumulate values based on multiple documents. Rather they're designed to reshape documents one at a time. Total number of rounds is calculated using the `$sum` operator. The value **1** simply counts the number of documents passed through that group together with each document that matches or is grouped under a given `_id` value. The project may seem complex, but it's just making the output pretty. It's just that it's including `num_rounds` and `total_raised` from the previous document.

[Photos](https://goo.gl/photos/VdyC1uyf62GcsJKx7)
