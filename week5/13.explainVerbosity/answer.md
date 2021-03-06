## Question

Given the following output from explain, what is the best description of what happened during the query?

~~~mongo
> exp = db.example.explain("executionStats")
Explainable(test.example)
> exp.find( { a : 7 } )
{
    "queryPlanner" : {
        "plannerVersion" : 1,
        "namespace" : "test.example",
        "indexFilterSet" : false,
        "parsedQuery" : {
            "a" : {
                "$eq" : 7
            }
        },
        "winningPlan" : {
            "stage" : "COLLSCAN",
            "filter" : {
                "a" : {
                    "$eq" : 7
                }
            },
            "direction" : "forward"
        },
        "rejectedPlans" : [ ]
    },
    "executionStats" : {
        "executionSuccess" : true,
        "nReturned" : 10000,
        "executionTimeMillis" : 619,
        "totalKeysExamined" : 0,
        "totalDocsExamined" : 999999,
        "executionStages" : {
            "stage" : "COLLSCAN",
            "filter" : {
                "a" : {
                    "$eq" : 7
                }
            },
            "nReturned" : 10000,
            "executionTimeMillisEstimate" : 520,
            "works" : 1000001,
            "advanced" : 10000,
            "needTime" : 990000,
            "needFetch" : 0,
            "saveState" : 7812,
            "restoreState" : 7812,
            "isEOF" : 1,
            "invalidates" : 0,
            "direction" : "forward",
            "docsExamined" : 999999
        }
    },
    "serverInfo" : {
        "host" : "cross-mb-air.local",
        "port" : 27017,
        "version" : "3.0.1",
        "gitVersion" : "534b5a3f9d10f00cd27737fbcd951032248b5952"
    },
    "ok" : 1
}
~~~

- The query used an index called BasicCursor and returned its results in 619 milliseconds
- The query scanned 999,999 documents, returning 10,000 in 619 milliseconds.
- The query scanned 10,000 documents and return in 520 milliseconds. (escaneo 999999 en 619 milisegundos)
- The query's explain plan is performed on a cursor.

## Answer

db.example.explain("executionStats") muestra mas informacion que nos puede ser de utilidad.

- The query used an index called BasicCursor and returned its results in 619 milliseconds. (no hay un winning plan o un IXSCAN donde podriamos ver los indice que se usaron)
- The query scanned 999,999 documents, returning 10,000 in 619 milliseconds.
- The query scanned 10,000 documents and return in 520 milliseconds.
- The query's explain plan is performed on a cursor. (en el parametro del explain debio usar "allPlansExecution" y no fue asi)

## Result

- The query scanned 999,999 documents, returning 10,000 in 619 milliseconds.

