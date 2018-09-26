## Question

Which of the following is a valid way to discover indexes for a collection in mongoDB?

## Answer

- show indexes
- [db.collection.getIndexes()](https://docs.mongodb.com/manual/reference/method/db.collection.getIndexes/index.html)
- db.collection.findIndexes()
- db.collection.find("indexes")
- db.getIndexes()

## Result

~~~mongo
db.collection.getIndexes()
~~~