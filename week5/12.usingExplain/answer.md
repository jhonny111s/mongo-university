## Question

Which of the following are valid ways to find out which indices a particular query uses?


## Answer

el explain se puede usar de dos maneras siempre y cuando devuelva un cursor

~~~mongo
db.foo.find().explain()
db.foo.explain().find()
~~~

- db.example.find( { a : 1, b : 2 } ).explain()
- db.example.remove( { a : 1, b : 2 } ).explain()  (doesn't return a cursor)
- db.example.explain().find( { a : 1, b : 2 } )
- db.example.explain().remove( { a : 1, b : 2 } )
- var exp = db.example.explain(); exp.find( { a : 1, b : 2 } )
- curs = db.example.find( { a : 1, b : 2 } ); curs.explain()

## Result

- db.example.find( { a : 1, b : 2 } ).explain()
- db.example.explain().find( { a : 1, b : 2 } )
- db.example.explain().remove( { a : 1, b : 2 } )
- var exp = db.example.explain(); exp.find( { a : 1, b : 2 } )
- curs = db.example.find( { a : 1, b : 2 } ); curs.explain()

