## Question

Suppose we have a collection foo that has an index created as follows:

~~~mongo
db.foo.createIndex( { a:1, b:1 } )
~~~

Which of the following inserts are valid to this collection?

## Answer

[multikey indexes](https://docs.mongodb.com/manual/core/index-multikey/index.html)

### example
1. use test
2. db.foo.insert({a:2, b:[1,2]})
3. db.foo.createIndex({a:1, b:1})
4. db.foo.explain().find({a:2, b:[1, 2]})
~~~mongo
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "test.foo",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "$and" : [
                                {
                                        "a" : {
                                                "$eq" : 3
                                        }
                                },
                                {
                                        "b" : {
                                                "$eq" : [
                                                        1,
                                                        2
                                                ]
                                        }
                                }
                        ]
                },
                "winningPlan" : {
                        "stage" : "FETCH",
                        "filter" : {
                                "b" : {
                                        "$eq" : [
                                                1,
                                                2
                                        ]
                                }
                        },
                        "inputStage" : {
                                "stage" : "IXSCAN",
                                "keyPattern" : {
                                        "a" : 1,
                                        "b" : 1
                                },
                                "indexName" : "a_1_b_1",
            ---->               "isMultiKey" : true,
                                "multiKeyPaths" : {
                                        "a" : [ ],
                                        "b" : [
                                                "b"
                                        ]
                                },
                                "isUnique" : false,
                                "isSparse" : false,
                                "isPartial" : false,
                                "indexVersion" : 2,
                                "direction" : "forward",
                                "indexBounds" : {
                                        "a" : [
                                                "[3.0, 3.0]"
                                        ],
                                        "b" : [
                                                "[1.0, 1.0]",
                                                "[[ 1.0, 2.0 ], [ 1.0, 2.0 ]]"
                                        ]
                                }
                        }
                },
                "rejectedPlans" : [ ]
        },
        "serverInfo" : {
                "host" : "DESKTOP-PBLF3G4",
                "port" : 27017,
                "version" : "4.0.1",
                "gitVersion" : "54f1582fc6eb01de4d4c42f26fc133e623f065fb"
        },
        "ok" : 1
}
~~~


- db.foo.insert( { a : [ "apples", "oranges" ], b : "grapes" } )
- db.foo.insert( { a : "grapes", b : "oranges" } )
- db.foo.insert( { a : "grapes", b : [ 8, 9, 10 ] } )
- db.foo.insert( { a : [ 1, 2, 3 ], b : [ 5, 6, 7 ] } )

## Result

debe existir un escalar (valor) y un vector (array), si no hay un array no puede se multikey pero si hay dos array esto no esta permitido

~~~mongo
- db.foo.insert( { a : [ "apples", "oranges" ], b : "grapes" } )
- db.foo.insert( { a : "grapes", b : "oranges" } )
- db.foo.insert( { a : "grapes", b : [ 8, 9, 10 ] } )
~~~