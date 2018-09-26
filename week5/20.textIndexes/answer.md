## Question

You create a text index on the "title" field of the movies collection, and then perform the following text search:

~~~mongo
> db.movies.find( { $text : { $search : "Big Lebowski" } } )
~~~

Which of the following documents will be returned, assuming they are in the movies collection? Check all that apply.

- { "title" : "The Big Lebowski" , star: "Jeff Bridges" }
- { "title" : "Big" , star : "Tom Hanks" }
- { "title" : "Big Fish" , star: "Ewan McGregor" }

## Answer

- para poder usar $text debe existir un indice de tipo texto, de lo contrario muestra un error.
- db.movies.createIndex({'title': 'text'})

## Result

- { "title" : "The Big Lebowski" , star: "Jeff Bridges" }
- { "title" : "Big" , star : "Tom Hanks" }
- { "title" : "Big Fish" , star: "Ewan McGregor" }
