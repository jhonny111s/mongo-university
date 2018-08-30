## Question

This application depends on the companies.json dataset distributed as a handout with the findAndCursorsInNodeJSDriver lesson. You must first import that collection. Please ensure you are working with an unmodified version of the collection before beginning this exercise.

To import a fresh version of the companies.json data, please type the following:

~~~mongo
mongoimport --drop -d crunchbase -c companies companies.json
~~~
If you have already mongoimported this data you will first need to drop the crunchbase database in the Mongo shell. Do that by typing the following two commands, one at a time, in the Mongo shell:

~~~mongo
use crunchbase
db.dropDatabase()
~~~

The code in the attached handout is complete with the exception of the queryDocument() function. As in the lessons, the queryDocument() function builds an object that will be passed to find() to match a set of documents from the crunchbase.companies collection.

For this assignment, please complete the queryDocument() function as described in the TODO comments you will find in that function.

Once complete, run this application by typing:

~~~node
node buildingQueryDocuments.js
~~~

When you are convinced you have completed the application correctly, please enter the average number of employees per company reported in the output. Enter only the number reported. It should be three numeric digits.

As a check that you have completed the exercise correctly, the total number of unique companies reported by the application should equal 42.

## Answer

- Complete this statement to match the regular expression "social-networking"
~~~mongo
 "tag_list": {"$regex":  "social-networking","$options": "i"}
~~~

- Write one line of code to ensure that if both firstYear and lastYear appear in the options object, we will match documents that have a value for the "founded_year" field of companies documents in the correct range. 
~~~mongo
query.founded_year = { "$gte": options.firstYear, "$lte": options.lastYear };
~~~
   
- Write one line of code to ensure that we do an equality match on the "offices.city" field. The "offices" field stores an array in which each element  is a nested document containing fields that describe a corporate office. Each office document contains a "city" field. A company may have multiple corporate offices. 

~~~mongo
query["offices.city"] = options.city;
~~~

## Result

169




