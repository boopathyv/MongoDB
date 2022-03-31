show dbs
use sharding
db.createCollection("movies")
db.createCollection("flags")
show collections
db.movies.getShardDistribution()

HASHED SHARDING :
sh.shardCollection("sharding.movies",{"title":"hashed"})

enable sharding in DB :
sh.enableSharding("sharding")

Bulk Insert :
for i in (1..50); do echo -e "use sharding \n db.movies.insertOne({\"title\": \"Spider Man $i\", \"language\": \"English\"})" | mongo mongodb://192.168.1.2:60000; done

Range Sharding :
sh.shardCollection( "sharding.flags", { "_countryId" : 1 }, true)
Insert data
db.flags.insert( { "_countryId" : 1, "countryName" : "hellohh" } )
Split collection
sh.splitAt( "sharding.flags", { _countryId : 10})

multiple field sharding

sh.shardCollection(
  "database.collection",
  { "fieldA" : 1, "fieldB" : 1, "fieldC" : "hashed" }
)