## Question

As a follow up to the previous question, how many documents in the video.movieDetails collection list both "Comedy" and "Crime" as genres regardless of how many other genres are listed?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.

## Answer

see [array_operations](https://docs.mongodb.com/manual/tutorial/query-arrays/index.html)

~~~mongo
db.movieDetails.find({ "genres": {$all: ["Comedy", "Crime"] } }).count()
~~~

## Result

56




