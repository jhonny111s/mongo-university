## Question

Now, using the Mongo shell, perform a *find()* on the collection called *hw1_1* in the database *m101*. There is one document in this collection. Please provide the value corresponding to the "answer" key (without the surrounding quotes) from the document returned.

## Answer

- mongorestore dump
- use m101
- show collections
- db.hw1_1.find()

## Result

~~~mongo
{ "_id" : ObjectId("51e4524ef3651c651a42331c"), "answer" : "Hello from MongoDB!" }
~~~




