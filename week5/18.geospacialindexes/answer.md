## Question

Suppose you have a 2D geospatial index defined on the key location in the collection places. Write a query that will find the closest three places (the closest three documents) to the location 74, 140.

## Answer

los indices geoespaciales estan basadas en coordenadas cartesianas (x, y) 

- use test
- db.places.insert({name: 'casa2', location: [1,1]})
- db.places.createIndex({location: '2d'})
- db.places.explain().find({'location': {'$near': [0,1], $maxDistance: 1}}).limit(3)

## Result

~~~mongo
db.places.find({'location': {'$near': [74,140]}}).limit(3)
~~~