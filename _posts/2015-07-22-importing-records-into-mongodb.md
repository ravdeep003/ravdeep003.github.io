---
title: Importing records into MongoDB
layout: single
classes: wide
comments: true
---

In this tutorial, I will demonstrate how we can use `mongoimport` to quickly add records(or documents) into `MongoDB` from JSON or CSV file. We will walk through different structures of file to import documents from.

### JSON

Consider a file `employee.json` which contains the employee's information, each line represents a single document(or record), as shown below:

        { name:"John", city: "New York", state: "NY" }
        { name:"Miller", city: "Dallas", state: "TX" }
        { name:"James", city: "Los Angeles", state: "CA" }

Now to import these records into our local `MongoDB`, just run:

        mongoimport --db <db_name> --collection <collection_name> --file employee.json

Default file type used by `mongoimport` is `JSON`, so we don't need to explicitly specify the `--type` here.


### JSON Array

Let's consider the same data as in above example(employee.json) but in JSONArray format as shown below:

        [
         { name:"John", city: "New York", state: "NY" },
           { name:"Miller", city: "Dallas", state: "TX" },
          { name:"James", city: "Los Angeles", state: "CA" }
         ]

To import these records into our local `MongoDB`, just use `--jsonArray` parameter:

        mongoimport --db <db_name> --collection <collection_name> --file employee.json --jsonArray


### CSV with headerline

Let's consider the same data as above in CSV format(employee.csv):

        "Name", "City", "State"
        "John", "New York", "NY"
        "Miller", "Dallas",  "TX"
        "James", "Los Angeles", "CA"

Use the below command to import these records and specify `--headerline` parameter, so that `mongoimport` determines the fields from the first line:

        mongoimport --db <db_name> --collection <collection_name> --type csv --headerline --file employee.csv


### CSV without headerline

Let's take the same csv file from above example but without the headerline.

        "John", "New York", "NY"
        "Miller", "Dallas",  "TX"
        "James", "Los Angeles", "CA"

To specify the fields use `--fields` or `-f` option followed by comma sperated field names.

        mongoimport --db <db_name> --collection <collection_name> --type csv --file employee.csv --fields name,city,state


or alternatively we can also use `--fieldFile` option, which allows to specify the file which contains fields name.
<BR>
<BR>

### Import JSON to remote Host
In above examples we have considered that `MongoDB` is running locally. If we want to import records into MongoDB instance running on some remote host, we can use the following command:

        mongoimport --host <host_address> --port <port_no> --db <db_name> --collection <coll_name> --file employee.json


There are a lot more options in `mongoimport`, which I have not covered in this blog. Please refer to [mongoimport](http://docs.mongodb.org/manual/reference/program/mongoimport/) documentation for more information.

<BR>
Thank you for reading.


