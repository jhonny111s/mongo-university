## Question

What are the advantages of a sparse index?


## Answer

Se se quiere crear un indice unico con una valor que no siempre se encuentra, mongo no lo va a permitir y va mostrar un error de indice duplicado porque siempre es null.

~~~mongo
db.employees.createIndex({cell:1, {unique:true}})
~~~

Sin embargo se puede crear un indice con estos tipos de valores agregando la llave "sparse"

~~~mongo
db.employees.createIndex({cell:1, {unique:true, sparse: true}})
~~~


- The index will be smaller than it would if it were not sparse.
- You can gain greater flexibility with creating Unique indexes.
- Your indexes can be multikey only if they are sparse. (are multikey if one is scalar and other an vector)
- The index can be used to sort much more quickly in all cases. (spare index omit document in sort )


## Result

- The index will be smaller than it would if it were not sparse.
- You can gain greater flexibility with creating Unique indexes.

