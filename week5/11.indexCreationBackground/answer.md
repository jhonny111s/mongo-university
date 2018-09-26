## Question

Which things are true about creating an index in the background in MongoDB. Check all that apply.


## Answer

se pueden craer los indices en primer plano (foreground) o en segundo plano ([background](https://docs.mongodb.com/manual/core/index-creation/#index-creation-background)). En foreground (por defecto) es mas rapida la creacion pero se bloquea la lectura/escritura de la base de datos hasta que finalice, mientras que background es mas lento pero no tiene ningun bloqueo.

~~~mongo
db.employees.createIndex({cell:1, {background: true}})
~~~


- A mongod instance can only build one background index at a time per database.
- Although the database server will continue to take requests, a background index creation still blocks the mongo shell that you are using to create the index.
- Creating an index in the background takes longer than creating it in the foreground
- In Mongo 2.2 and above, indexes are created in the background by default.

## Result

- Although the database server will continue to take requests, a background index creation still blocks the mongo shell that you are using to create the index.
- Creating an index in the background takes longer than creating it in the foreground

