No sql databases is a very broad generalizarion term there are dofferent tyoes of databases under it

- NoSql databases usually again this is a generalization but they usually come sharded out of the e box
- This is so because they dont follow transactions and acid properties its because they dont have any strict rules they can be sharded easily

Types of NoSql databases:

1. Document Db
2. KV store

Document db:

1. Supports complex query like aggregations
2. This is most similar to sql in terms of features of aggregations
3. Important: This supports partial updates which means if i have to update a particular field i dont have to download the entire table update and then insert entire table. I can make change the only that field.
4. Most kv doesnt not support partial update
5. Example of documebt db: mongodb and elasticsearch

Kv store:

1. Simple db store that allows key based access
2. Aggregations are not allowed in kv stored
3. Since this is simple these can be easily sharded and partitioned
4. Extremely Simple databases
5. Limited Functionalities(GET,PUT,DEL)

Graph Databases:(Neo4j,Neptune,DGraph)