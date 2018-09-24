
## Question

In this lab, you will implement the methods in items.js necessary to support the route for text search or "/search". This route is implemented in mongomart.js in the function that begins with this line:

~~~javascript
router.get("/search", function(req, res) {
~~~

The methods you will implement in items.js are: searchItems(), and getNumSearchItems(). The comments in each of these methods describe in detail what you need to do to implement each method. When you are finished, restart the mongomart.js application and answer the question below.

How many products match the query, "leaf"?
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10


## Answer

~~~javascript
 this.searchItems = function(query, page, itemsPerPage, callback) {
        "use strict";

        /*
         * TODO-lab2A
         *
         * LAB #2A: Implement searchItems()
         *
         * Using the value of the query parameter passed to searchItems(),
         * perform a text search against the "item" collection.
         *
         * Sort the results in ascending order based on the _id field.
         *
         * Select only the items that should be displayed for a particular
         * page. For example, on the first page, only the first itemsPerPage
         * matching the query should be displayed.
         *
         * Use limit() and skip() and the method parameters: page and
         * itemsPerPage to select the appropriate matching products. Pass these
         * items to the callback function.
         *
         * searchItems() depends on a text index. Before implementing
         * this method, create a SINGLE text index on title, slogan, and
         * description. You should simply do this in the mongo shell.
         *
         */

         /*
             db.item.aggregate([ 
                 {$addFields: 
                    {'text': { $concat: ['$title',' - ','$slogan',' - ' ,'$description'] } } }, 
                 {$match: {'text': {$regex: 'leaf', $options: 'i'}}}])
         */

         

        var collection = this.db.collection( 'item' );
        var cursor =  collection.aggregate([
            {'$addFields': { 'text': { '$concat': ['$title',' - ','$slogan',' - ' ,'$description'] } } }, 
            {'$match': {'text': {'$regex': query, '$options': 'i'}}}])
            .skip(page*itemsPerPage).limit(itemsPerPage)
            .sort({_id:1});

        cursor.toArray(function(error, items) {
            assert.equal(error,  null);
            callback(items);
        });
    }
~~~

~~~javascript
    this.getNumSearchItems = function(query, callback) {
        "use strict";

        /*
        * TODO-lab2B
        *
        * LAB #2B: Using the value of the query parameter passed to this
        * method, count the number of items in the "item" collection matching
        * a text search. Pass the count to the callback function.
        *
        * getNumSearchItems() depends on the same text index as searchItems().
        * Before implementing this method, ensure that you've already created
        * a SINGLE text index on title, slogan, and description. You should
        * simply do this in the mongo shell.
        */


       var collection = this.db.collection( 'item' );
       var cursor =  collection.aggregate([
           {'$addFields': { 'text': { '$concat': ['$title',' - ','$slogan',' - ' ,'$description'] } } }, 
           {'$match': {'text': {'$regex': query, '$options': 'i'}}},
           {'$group': {'_id': 'null', 'count': {'$sum': 1} }}])

       cursor.toArray(function(error, items) {
           assert.equal(error,  null);
           callback(items[0].count);
       });
    }
~~~

## Result

7




