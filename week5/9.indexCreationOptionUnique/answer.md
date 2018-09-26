## Question

Please provide the mongo shell command to create a unique index on student_id, class_id, ascending for the collection students.


## Answer

como _id no se puede repetir dos veces este identificador (insertar), esa es la funcincion de unique en los index.

## Result

~~~mongo
db.students.createIndex({'student_id': 1, 'class_id': 1},{'unique': true})
~~~