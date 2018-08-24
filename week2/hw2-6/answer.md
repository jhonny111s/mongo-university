## Question

Suppose you wish to update the value of the "plot" field for one document in our "movieDetails" collection to correct a typo. Which of the following update operators and modifiers would you need to use to do this?

## Answer

see [update_document](https://docs.mongodb.com/manual/tutorial/update-documents/index.html)

~~~mongo
db.movieDetails.updateOne(
   { _id:  ObjectId("5692a4ca24de1e0ce2dfdbdd") },
   {
     $set: { "plot": "updated pot" }
   }
)
~~~

## Result

~~~mongo
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
~~~




