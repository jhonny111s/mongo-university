## Challenge

This problem is provided as a supplementary learning opportunity. It is more challenging that the ordinary homework. It is ungraded. We do not ask you submit an answer.

Write an update command that will remove the "tomato.consensus" field for all documents matching the following criteria:

The number of imdb votes is less than 10,000
The year for the movie is between 2010 and 2013 inclusive
The tomato.consensus field is null
How many documents required an update to eliminate a "tomato.consensus" field?

NOTE: There is a dump of the video database included in the handouts for the "Creating Documents" lesson. Use that data set to answer this question.


## Answer

~~~mongo
db.movieDetails.updateMany({ year: {$gte: 2010, $lte: 2013},
                             "imdb.votes": {$lt: 10000},
                             $and: [{"tomato.consensus": {$exists: true} },
                                    {"tomato.consensus": null} ] },
                           { $unset: { "tomato.consensus": "" } });
~~~
In response, you will receive the following:

~~~mongo
{ "acknowledged" : true, "matchedCount" : 13, "modifiedCount" : 13 }
~~~

Using the second approach, you can issue a simpler command, but one that is not precise about what needs to be updated.

~~~mongo
db.movieDetails.updateMany({ year: {$gte: 2010, $lte: 2013},
                             "imdb.votes": {$lt: 10000},
                             "tomato.consensus": null },
                           { $unset: { "tomato.consensus": "" } });
~~~

In response, you will receive the following:

~~~mongo
{ "acknowledged" : true, "matchedCount" : 204, "modifiedCount" : 13 }
~~~

Note that while the query portion of the update matches 204 documents, only 13 documents actually required an update.