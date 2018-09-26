## Question

Suppose you have a collection called people in the database earth with documents of the following form:

~~~mongo
{
    "_id" : ObjectId("551458821b87e1799edbebc4"),
    "name" : "Eliot Horowitz",
    "work_history" : [
        {
            "company" : "DoubleClick",
            "position" : "Software Engineer"
        },
        {
            "company" : "ShopWiki",
            "position" : "Founder & CTO"
        },
        {
            "company" : "MongoDB",
            "position" : "Founder & CTO"
        }
    ]
}
~~~
Type the command that you would issue in the Mongo shell to create an index on company, descending.

## Answer

1. use earth
2. db.people.createIndex({'work_history.company':1})
3. db.people.find({'work_history.company': 'shopWiki'})


## Result

~~~mongo
db.people.createIndex({'work_history.company': -1});
~~~