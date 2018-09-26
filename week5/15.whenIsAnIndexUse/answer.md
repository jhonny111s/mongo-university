## Question

Given collection foo with the following index:

~~~mongo
db.foo.createIndex( { a : 1, b : 1, c : 1 } )
~~~

Which of the following queries will use the index?

- db.foo.find( { b : 3, c : 4 } )
- db.foo.find( { a : 3 } )
- db.foo.find( { c : 1 } ).sort( { a : 1, b : 1 } )
- db.foo.find( { c : 1 } ).sort( { a : -1, b : 1 } )

## Answer

>To verify the answer key, and see how each index is used, you can check explain("executionStats").
The overriding principle, though, is that you must use a left-subset (or "prefix") of the index. For sorting, it must either match the index orientation, or match its reverse orientation, which you can get when the btree is walked backwards.

## Result

- db.foo.find( { a : 3 } )
- db.foo.find( { c : 1 } ).sort( { a : 1, b : 1 } )

