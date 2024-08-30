---
title:  MongoDB Learning Notes and Useful Commands
tags:
  - NoSql Database
  - MongoDB
  - Backend Development
---

MongoDB is one of the typical NoSQL databases. It's a document databased where data is stored in the form of json-type 
document. Understanding MongoDB is crucial for back-end development, particularly for agile development.

<!--more-->

### Useful Commands

#### A. Search Commands

1. start mongosh
2. show databases
3. show collections
3. switch to the database
4. find all datas in the database
5. delete collection
6. insert data
7. get the count of the data
8. find data in page n ( skip((n-1)*pageSize)) (Mongodb can show data by pages)
9. find data by AND conditions
10. find data by OR conditions
11. find the first data
12. find data with age greater than 22
13. find data with age greater than and equals to 22

```zsh
mongosh

show dbs

show collections

use databaseName

db.collectionName.find()

db.collectionName.drop()

db.collectionName.insert({"username": "Tom", "age": 18})

db.collectionName.find().count()

db.collectionName.find().skip((n-1) * pageSize).limit(pageSize)

db.collectionName.find({"username": "Tom", "age": 18})

db.collectionName.find({$or:[{"username":"Tom", "username":Mary}]})

db.collectionName.findOne()

db.collectionName.find({age:{$gt:22}})

db.collectionName.find({age:{$gte:22}})
```


#### B. Update Commands
Notes: don't forget $set when updating data.
1. update name from "Tom" to "Jack"
2. add sex in one specified data(name=Jack, age=18)
3. update multi data at one time
4. increase age by 1

```zsh
db.collectionName.update({"name": "Tom"}, {$set:{"name": "Jack"}})

db.collectionName.update({"name":"Jack", "age": 18}, {$set:{"sex": "male"}})

db.collectionName.update({"age": 18}, {$set:{"sex": "female"}}, {multi:true})

db.collectionName.update({"name": "Tom"}, {inc:{age: 1}}, false, true)
```

#### C. Delete Commands
1. delete one specified data
2. delete multiple data (age > 18)
3. delete just one data which satisfied the condition

```zsh
db.collectionName.remove({"name": "Tom"}})

db.collectionName.remove({"age": {$gt: 18}})

db.collectionName.remove({"age": {$gt: 18}}, {justOne:true})
```

#### D. Advanced MongoDB
Setting an index can make the search speed faster.
1. set an index
2. get the indexes
3. set multiple indexes
4. set unique index (A unique index means that the value cannot be repeated.)
```zsh
db.collectionName.ensureIndex({"username": 1})

db.collectionName.getIndexes()

db.collectionName.dropIndex({"username": 1})

db.collectionName.ensureIndex({"username": 1}, {"age": 1})

db.collectionName.ensureIndex({"age": 1}, {"unique": true})
```

#### E. The relationships of Databases
##### 1. One-to-one
Like National ID to student ID.

##### 2. One-to-many
Like order ID to order items. In one order, there can be many items.


##### 3. Many-to-many
Like products to users. One product can be collected by multiple users. 
One user can collect multiple products. 

In many-to-many situation, we ofter use intermediate table to mark the correspondence.

#### F. Aggregation Pipeline
Aggregation pipeline in MongoDB is used to transfer and group documents.

Usage: Table Association Query and Data Statistics

##### 1. $project
$project is used to edit the structure of the documents. It's useful to rename, add and delete the data.

```zsh
db.collectionName.aggregate([
                    {$project: {trade_no: 1, all_price: 1}}
])
```

##### 2. $match
$match is used to filter the documents.

```zsh
db.collectionName.aggregate([
                    {$project: {trade_no: 1, all_price: 1}},
                    {$match: {"all_price": {$gte: 90}}}
])
```

##### 3. $group
$group is used to filter the documents.

In the following example, data is grouped by order_id and then sum up by the num.
```zsh
db.collectionName.aggregate([
                    {$group: {$_id: "order_id", total: {$sum: "$num"}}},
])
```

##### 4. $sort
$sort the documents in the collection.
{$sort:{"all_price": -1}} 
```zsh
db.collectionName.aggregate([
                    {$project: {trade_no: 1, all_price: 1}},
                    {$match: {"all_price": {$gte: 90}}},
                    {$sort:{"all_price": -1}}
])
```

##### 4. $limit
$limit stands for only returning one data.
Only showing one data.
```zsh
db.collectionName.aggregate([
                    {$project: {trade_no: 1, all_price: 1}},
                    {$match: {"all_price": {$gte: 90}}},
                    {$sort:{"all_price": -1}},
                    {$limit: 1}
])
```

##### 5. $skip
$skip stands for skip data.
Skip one data:
```zsh
db.collectionName.aggregate([
                    {$project: {trade_no: 1, all_price: 1}},
                    {$match: {"all_price": {$gte: 90}}},
                    {$sort:{"all_price": -1}},
                    {$skip: 1}
])
```

##### 6. $lookup
$lookup can connect two tables together.

```zsh
db.collectionName.aggregate([
                    {$lookup:{
                      from:"order_item",
                      localField:"order_id",
                      foreignField: "order_id",
                      as:"items"
                    }},
                    {$project: {trade_no: 1, all_price: 1}},
                    {$match: {"all_price": {$gte: 90}}},
                    {$sort:{"all_price": -1}},
                    {$skip: 1}
])
```

<body data-article-id="post-mongodb-notes">
</body>






