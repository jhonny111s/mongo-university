## Question

Please provide the mongo shell command to add an index to a collection named students, having the index key be class, student_name.

Neither will go in the "-1" direction..

## Answer

- Run mongo
- copy create_scores2 content (is slow)
- use school
- db.students.explain().find({student_id:5})

>The explain() method returns a document with the query plan and, optionally, the execution statistics.

~~~mongo
// without indexes
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "school.students",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "student_id" : {
                                "$eq" : 5
                        }
                },
                "winningPlan" : {
                        "stage" : "COLLSCAN",
                        "filter" : {
                                "student_id" : {
                                        "$eq" : 5
                                }
                        },
                        "direction" : "forward"
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

- db.students.createIndex({student_id: 1})
- db.students.explain().find({student_id:5})

~~~mongo
{
        "queryPlanner" : {
                "plannerVersion" : 1,
                "namespace" : "school.students",
                "indexFilterSet" : false,
                "parsedQuery" : {
                        "student_id" : {
                                "$eq" : 5
                        }
                },
                "winningPlan" : {
                        "stage" : "FETCH",
         ---->          "inputStage" : {
                                "stage" : "IXSCAN",
                                "keyPattern" : {
                                        "student_id" : 1
                                },
                                "indexName" : "student_id_1",
                                "isMultiKey" : false,
                                "multiKeyPaths" : {
                                        "student_id" : [ ]
                                },
                                "isUnique" : false,
                                "isSparse" : false,
                                "isPartial" : false,
                                "indexVersion" : 2,
                                "direction" : "forward",
                                "indexBounds" : {
                                        "student_id" : [
                                                "[5.0, 5.0]"
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

## Result

~~~mongo
db.students.createIndex({class: 1, student_name: 1});
~~~