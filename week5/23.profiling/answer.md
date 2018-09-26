## Question

Write the query to look in the system profile collection for all queries that took longer than one second, ordered by timestamp descending.

## Answer

- use school
- show collections

## Result

~~~mongo
db.system.profile.find({'millis': {'$gt': 1000}}).sort({'ts':-1})
~~~
