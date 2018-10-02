
## Question

Starting with the example we looked at for calculating the total number of relationships individuals have participated in (in the CrunchBase data set):

~~~mongo
db.companies.aggregate( [
    { $match: { "relationships.person": { $ne: null } } },
    { $project: { relationships: 1, _id: 0 } },
    { $unwind: "$relationships" },
    { $group: {
        _id: "$relationships.person",
        count: { $sum: 1 }
    } },
    { $sort: { count: -1 } }
] )
~~~

Write an aggregation query that will determine the number of unique companies with which an individual has been associated. To test that you wrote your aggregation query correctly, from the choices below, select the number of unique companies that Eric Di Benedetto (eric-di-benedetto) has been associated with. I've attached the CrunchBase data set for use in this problem.

Hint: Review the available accumulators before beginning this exercise.

As a check on your work, the number of unique companies for roger-ehrenberg is 16, for josh-stein is 14, and the number for tim-hanlon actually is 28.

- 1
- 3 
- 5
- 10
- 15
- 17
- 20
- 22
- 23


## Answer

- mongoimport --drop -d crunchbase -c companies companies.json
- mongo
- use crunchbase
- show collections

Solucion 1

- busco todas las compañias que no tenga en campo person en null
- solo muestra los campos name y relationship
- crea una nueva salida con cada elemento de relationships
- agrupa por persona y usa un acumulador para agregar las compañias sin repetir.
- solo muestra id y compañia donde compañia es un acumulador que dice el tamaño del array.
- ordena de mayor a menor.

~~~mongo
db.companies.aggregate( [ 
    { $match: { "relationships.person": { $ne: null } } }, 
    { $project: { relationships: 1, _id: 0, name:1 } }, 
    {$unwind: "$relationships"}, 
    {$group: {
        _id: "$relationships.person", 
        companies: {$addToSet: "$name"}
    }}, 
    {$project: {_id: 1, companies: {$size: "$companies"}}}, {$sort: {companies:-1}} ] )
~~~

Solucion 2

~~~mongo
db.companies.aggregate([
    { $project: { relationships: 1, _id: 0, name : 1, permalink: 1 } },
    { $unwind: "$relationships" },
    { $group: {
        _id: { person: "$relationships.person" },
        gross_companies: { $push : "$permalink" },
        unique_companies: { $addToSet : "$permalink" }
    } },
    { $project: {
        _id: 0,
        person: "$_id.person",
        gross_companies: 1,
        unique_companies: 1,
        unique_number_of_companies: { $size: "$unique_companies" },
        gross_number_of_companies: { $size: "$gross_companies" }
    } },
    { $sort: { unique_number_of_companies: -1 } }
])
~~~



## Result

15




