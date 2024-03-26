MongoDB Cheat Checklist
===

[MongoDB](https://www.mongodb.com/developer/products/mongodb/cheat-sheet/#connect-mongodb-shell) This cheat sheet contains some handy tips, commands, and quick references to get you started in no time Connect and CRUD

getting Started
---

### Connect to MongoDB Shell
<!--rehype:wrap-class=col-span-2-->

```bash
mongo # Connect to mongodb://127.0.0.1:27017 by default
mongo --host <host> --port <port> -u <user> -p <pwd> # If prompted, omit the password
mongo "mongodb://192.168.1.1:27017"
#MongoDB Atlas
mongo "mongodb+srv://cluster-name.abcde.mongodb.net/<dbname>" --username <username>
```

### Show database

```mongodb
show dbs
db // print the current database
```

### Switch database

```mongodb
use <database_name>
```

### Show collection

```mongodb
show collections
```

### Run JavaScript file

```mongodb
load("myScript.js")
```

CRUD
---

### Create
<!--rehype:wrap-class=col-span-3-->

```mongodb
db.coll.insertOne({ name: "Max" })
db.coll.insert([{ name: "Max"}, {name: "Alex"}]) // Batch insert
db.coll.insert([{ name: "Max"}, {name: "Alex"}], {ordered: false}) // Unordered batch insert
db.coll.insert({ date: ISODate()})
db.coll.insert({ name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

### Find files

Commands | Description
:-- | ---
`db.docx.findOne()` | Find a random document
`db.docx.find().prettyPrint()` | Find all documents
`db.docx.find({}, {name:true, _id:false})` | Display only the name of the document Docx
`db.docx.find({}, {name:true, _id:false})` | You can find a file by attributes in multiple files

### Find documents using operators
<!--rehype:wrap-class=col-span-2-->

Operator | Description | Commands
:-- | --- | ---
`$gt` | greater than| `db.docx.find({class:{$gt:'T'}`
`$gte` | Greater than or equal to | `db.docx.find({class:{$gt:'T'}`
`$lt` | less than| `db.docx.find({class:{$lt:'T'}`
`$lte` | Less than or equal to | `db.docx.find({class:{$lte:'T'}`
`$exists` | Whether the attribute exists | `db.docx.find({class:{$gt:'T'}`
`$regex` | Regular expression matching | `db.docx.find({name:{$regex:'^USS\\sE'}})`
`$type` | Search by element type | `db.docx.find({name : {$type:4}})`

### Read
<!--rehype:wrap-class=col-span-3-->

```mongodb
db.coll.findOne() // Returns a single document
db.coll.find() // Return a cursor - show 20 results - "it" show more
db.coll.find().pretty()
db.coll.find({name: "Max", age: 32}) // Implicit logical "AND".
db.coll.find({date: ISODate("2020-09-25T13:57:17.180Z")})

// or "queryPlanner" or "allPlansExecution"
db.coll.find({name: "Max", age: 32}).explain("executionStats") 
db.coll.distinct("name")

// counting
db.coll.count({age: 32}) // Estimate based on collection metadata
db.coll.estimatedDocumentCount() // Estimation based on collection metadata
db.coll.countDocuments({age: 32}) // Alias ​​for aggregation pipeline - accurate count

// Comparison comparison
db.coll.find({"year": {$gt: 1970}})
db.coll.find({"year": {$gte: 1970}})
db.coll.find({"year": {$lt: 1970}})
db.coll.find({"year": {$lte: 1970}})
db.coll.find({"year": {$ne: 1970}})
db.coll.find({"year": {$in: [1958, 1959]}})
db.coll.find({"year": {$nin: [1958, 1959]}})


// Logical logic
db.coll.find({name:{$not: {$eq: "Max"}}})
db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
db.coll.find({
  $and: [
    {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
    {$or: [{sale: true}, {price: {$lt: 5 }}]}
  ]
})

// Element element
db.coll.find({name: {$exists: true}})
db.coll.find({"zipCode": {$type: 2 }})
db.coll.find({"zipCode": {$type: "string"}})

// Aggregation Pipeline aggregation pipeline
db.coll.aggregate([
  {$match: {status: "A"}},
  {$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
  {$sort: {total: -1}}
])

// Use the "text" index for text searches
db.coll.find({$text: {$search: "cake"}}, {score: {$meta: "textScore"}})
        .sort({score: {$meta: "textScore"}})

// Regex regular expression
db.coll.find({name: /^Max/}) // Regular expression: starting with the letter "M"
db.coll.find({name: /^Max$/i}) // Regular expressions are not case sensitive

// Array
db.coll.find({tags: {$all: ["Realm", "Charts"]}})
db.coll.find({field: {$size: 2}}) // Cannot index - prefer to store the size of the array and update it
db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})

// Projections predictions
db.coll.find({"x": 1}, {"actors": 1})               // actors + _id
db.coll.find({"x": 1}, {"actors": 1, "_id": 0})     // actors
db.coll.find({"x": 1}, {"actors": 0, "summary": 0}) // Everything except "actors" and "summary"

// Sort, skip, limit
db.coll.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3)

// Read Concern Read Concern
db.coll.find().readConcern("majority")
```

### renew
<!--rehype:wrap-class=col-span-3-->

```mongodb
db.coll.update({"_id": 1}, {"year": 2016}) // Warning! Replace entire document
db.coll.update({"_id": 1}, {$set: {"year": 2016, name: "Max"}})
db.coll.update({"_id": 1}, {$unset: {"year": 1}})
db.coll.update({"_id": 1}, {$rename: {"year": "date"} })
db.coll.update({"_id": 1}, {$inc: {"year": 5}})
db.coll.update({"_id": 1}, {$mul: {price: NumberDecimal("1.25"), qty: 2}})
db.coll.update({"_id": 1}, {$min: {"imdb": 5}})
db.coll.update({"_id": 1}, {$max: {"imdb": 8}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})

// Array
db.coll.update({"_id": 1}, {$push :{"array": 1}})
db.coll.update({"_id": 1}, {$pull :{"array": 1}})
db.coll.update({"_id": 1}, {$addToSet :{"array": 2}})
db.coll.update({"_id": 1}, {$pop: {"array": 1}}) // The last element
db.coll.update({"_id": 1}, {$pop: {"array": -1}}) // first element
db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}})
db.coll.update({}, {$set: {"grades.$[element]": 100}}, {multi: true, arrayFilters: [{"element": {$gte: 100}}]})

// Lots of updates
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

// FindOneAndUpdate Find and update
db.coll.findOneAndUpdate({"name": "Max"}, {$inc: {"points": 5}}, {returnNewDocument: true})

// Upsert update insert
db.coll.update({"_id": 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true})

// Replace alternative
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

// Save save
db.coll.save({"item": "book", "qty": 40})

// Write concern write concern
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

### delete
<!--rehype:wrap-class=col-span-3-->

```mongodb
db.coll.remove({name: "Max"})
db.coll.remove({name: "Max"}, {justOne: true})
db.coll.remove({}) // Warning! Delete all documents but not the collection itself and its index definitions
db.coll.remove({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
db.coll.findOneAndDelete({"name": "Max"})
```

Databases and collections
---

### Drop

```mongodb
// Delete the collection and its index definition
db.coll.drop()    
// Double check that you are *not* on the PROD cluster... :-)
db.dropDatabase() 
```

### Create a collection
<!--rehype:wrap-class=col-span-2 row-span-2-->

```mongodb
// Create a collection using $jsonschema
db.createCollection("contacts", {
   validator: {$jsonSchema: {
      bsonType: "object",
      required: ["phone"],
      properties: {
         phone: {
            bsonType: "string",
            description: "Must be a string and required"
         },
         email: {
            bsonType: "string",
            pattern: "@mongodb\.com$",
            description: "Must be a string and match a regular expression pattern"
         },
         status: {
            enum: [ "Unknown", "Incomplete" ],
            description: "Can only be one of the enumeration values"
         }
      }
   }}
})
```

### Other collection functions

```mongodb
db.coll.stats()
db.coll.storageSize()
db.coll.totalIndexSize()
db.coll.totalSize()
db.coll.validate({full: true})
//The second parameter is used to delete the target collection (if it exists)
db.coll.renameCollection("new_coll", true)
```

index
---

### List index

```mongodb
db.coll.getIndexes()
db.coll.getIndexKeys()
```

### Create index
<!--rehype:wrap-class=col-span-2 row-span-3-->

```mongodb
//Index type
db.coll.createIndex({"name": 1}) // Single field index
db.coll.createIndex({"name": 1, "date": 1}) // Composite index
db.coll.createIndex({foo: "text", bar: "text"}) // Text index
db.coll.createIndex({"$**": "text"}) // Wildcard text index
db.coll.createIndex({"userMetadata.$**": 1}) // Wildcard index
db.coll.createIndex({"loc": "2d"}) // Two-dimensional index
db.coll.createIndex({"loc": "2dsphere"})        // 2dsphere 索引
db.coll.createIndex({"_id": "hashed"}) // Hash index

// Index Options
db.coll.createIndex({"lastModifiedDate": 1}, {expireAfterSeconds: 3600})      // TTL指数
db.coll.createIndex({"name": 1}, {unique: true})
db.coll.createIndex({"name": 1}, {partialFilterExpression: {age: {$gt: 18}}}) // Partial index
// Case-insensitive index with strength 1 or 2
db.coll.createIndex({"name": 1}, {collation: {locale: 'en', strength: 1}})
db.coll.createIndex({"name": 1 }, {sparse: true})
```

### Delete index

```mongodb
db.coll.dropIndex("name_1")
```

### Hide/unhide index

```mongodb
db.coll.hideIndex("name_1")
db.coll.unhideIndex("name_1")
```

Convenient commands
---

###
<!--rehype:wrap-class=col-span-3&style=display:none;&wrap-style=padding-top: 0;-->

```mongodb
use admin
db.createUser({"user": "root", "pwd": passwordPrompt(), "roles": ["root"]})
db.dropUser("root")
db.auth( "user", passwordPrompt() )

use test
db.getSiblingDB("dbname")
db.currentOp()
db.killOp(123) // opid

db.fsyncLock()
db.fsyncUnlock()

db.getCollectionNames()
db.getCollectionInfos()
db.printCollectionStats()
db.stats()

db.getReplicationInfo()
db.printReplicationInfo()
db.isMaster()
db.hostInfo()
db.printShardingStatus()
db.shutdownServer()
db.serverStatus()

db.setSlaveOk()
db.getSlaveOk()

db.getProfilingLevel()
db.getProfilingStatus()
db.setProfilingLevel(1, 200) // 0 == OFF, 1 == ON with slowms, 2 == ON

db.enableFreeMonitoring()
db.disableFreeMonitoring()
db.getFreeMonitoringStatus()

db.createView("viewName", "sourceColl", [{$project:{department: 1}}])
```

Different kinds
---

### Change stream

```mongodb
watchCursor = db.coll.watch([
   {
      $match : {"operationType": "insert" }
   }
])

while (!watchCursor.isExhausted()){
   if (watchCursor.hasNext()){
      print(tojson(watchCursor.next()));
   }
}
```

### Sharded cluster
<!--rehype:wrap-class=col-span-2 row-span-3-->

```mongodb
sh.status()
sh.addShard("rs1/mongodbd1.example.net:27017")
sh.shardCollection("mydb.coll", {zipcode: 1})

sh.moveChunk("mydb.coll", { zipcode: "53187" }, "shard0019")
sh.splitAt("mydb.coll", {x: 70})
sh.splitFind("mydb.coll", {x: 70})
sh.disableAutoSplit()
sh.enableAutoSplit()

sh.startBalancer()
sh.stopBalancer()
sh.disableBalancing("mydb.coll")
sh.enableBalancing("mydb.coll")
sh.getBalancerState()
sh.setBalancerState(true/false)
sh.isBalancerRunning()

sh.addTagRange("mydb.coll", {state: "NY",zip: MinKey}, {state: "NY",zip: MaxKey}, "NY")
sh.removeTagRange("mydb.coll", {state: "NY",zip: MinKey}, {state: "NY",zip: MaxKey}, "NY")
sh.addShardTag("shard0000", "NYC")
sh.removeShardTag("shard0000", "NYC")

sh.addShardToZone("shard0000", "JFK")
sh.removeShardFromZone("shard0000", "NYC")
sh.removeRangeFromZone("mydb.coll", {a: 1, b: 1}, {a: 10, b: 10})
```

### Replica set

```mongodb
rs.status()
rs.initiate({"_id": "replicaTest",
  members: [
    { _id: 0, host: "127.0.0.1:27017" },
    { _id: 1, host: "127.0.0.1:27018" },
    { _id: 2, host: "127.0.0.1:27019",
    arbiterOnly:true }]
})
rs.add("mongodbd1.example.net:27017")
rs.addArb("mongodbd2.example.net:27017")
rs.remove("mongodbd1.example.net:27017")
rs.conf()
rs.isMaster()
rs.printReplicationInfo()
rs.printSlaveReplicationInfo()
rs.reconfig(<valid_conf>)
rs.slaveOk()
rs.stepDown(20, 5)
// (stepDownSecs, secondaryCatchUpPeriodSecs)
```
