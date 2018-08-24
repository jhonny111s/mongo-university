## Question

Using the video.movieDetails collection, which of the queries below would produce output documents that resemble the following. Check all that apply.

NOTE: We are not asking you to consider specifically which documents would be output from the queries below, but rather what fields the output documents would contain.

~~~mongo
{ "title" : "P.S. I Love You" }
{ "title" : "Love Actually" }
{ "title" : "Shakespeare in Love" }
~~~

## Answer

~~~mongo
db.collection.find(query, projection)
~~~

projection: Optional. Specifies the fields to return in the documents that match the query filter. To return all fields in the matching documents, omit this parameter.

~~~mongo
db.movieDetails.find({}, {title:1, _id:0})
~~~
~~~mongo
db.movieDetails.find({year:1964}, {title:1, _id:0})
~~~



