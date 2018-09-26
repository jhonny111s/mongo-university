## Question

You would like to perform a covered query on the example collection. You have the following indexes:

~~~mongo
{ name : 1, dob : 1 }
{ _id : 1 }
{ hair : 1, name : 1 }
~~~
Which of the following is likely to be a covered query? Check all that apply.

- db.example.find( { _id : 1117008 }, { _id : 0, name : 1, dob : 1 } )
- db.example.find( { name : { $in : [ "Alfred", "Bruce" ] } }, { name : 1, hair : 1 } )
- db.example.find( { name : { $in : [ "Bart", "Homer" ] } }, {_id : 0, hair : 1, name : 1} )
- db.example.find( { name : { $in : [ "Bart", "Homer" ] } }, {_id : 0, dob : 1, name : 1} )

## Answer

Una consulta es [cubierta](https://docs.mongodb.com/manual/core/query-optimization/#covered-query) por completo cuando cuando el total de documentos examinados es 0. La proyeccion debe contener exactamente el indice al igual que la query. 

- db.example.find( { _id : 1117008 }, { _id : 0, name : 1, dob : 1 } )  (usa _id pero tiene name-bob)
- db.example.find( { name : { $in : [ "Alfred", "Bruce" ] } }, { name : 1, hair : 1 } ) (usa name-bob porque la query es por name, pero tendria _id y hair)
- db.example.find( { name : { $in : [ "Bart", "Homer" ] } }, {_id : 0, hair : 1, name : 1} ) (usa name-bob porque la query empieza con name pero tendria hair)
- db.example.find( { name : { $in : [ "Bart", "Homer" ] } }, {_id : 0, dob : 1, name : 1} ) (usa name-bod y la proyeccion es name-bob)

## Result

- db.example.find( { name : { $in : [ "Bart", "Homer" ] } }, {_id : 0, dob : 1, name : 1} )

