
## Question

The items.js file implements data access for the item collection. The item collection contains the product catalog for the MongoMart application.

The mongomart.js application instantiates an item data access object (DAO) with this call:

~~~javascript
var items = new ItemDAO(db);
~~~

The DAO, items, is used throughout mongomart.js to implement several of the routes in this application.

In this lab, you will implement the methods in items.js necessary to support the root route or "/". This route is implemented in mongomart.js in the function that begins with this line:

~~~javascript
router.get("/", function(req, res) {
~~~

The methods you will implement in items.js are: getCategories(), getItems(), and getNumItems(). The comments in each of these methods describe in detail what you need to do to implement each method. When you believe you are finished, restart the mongomart.js application and evaluate your application to see whether it matches the following description.

If you have completed this lab correctly, the landing page for Mongomart should now show the following five products: Gray Hooded Sweatshirt, Coffee Mug, Stress Ball, Track Jacket, and Women's T-shirt. On the left side of the page you should see nine product categories listed, beginning with "All" and ending with "Umbrellas". At the bottom of the page you should see tabs for pages 1-5 with the statement "23 Products" immediately underneath.

If your application matches the above description, please answer the following question.

Select the "Apparel" category by clicking on it with your mouse. This category contains six products. MongoMart will paginate the products in this category into two pages. Which of the following items is listed on the second page? There should be only one item on this page. Please make sure you are sorting query results as specified in the Lab 1 instructions or you might get the wrong answer.

- Gray Hooded Sweatshirt
- Track Jacket
- Women's T-shirt
- WiredTiger T-shirt
- Green T-shirt
- MongoDB University T-shirt


## Answer

~~~javascript
 this.getCategories = function(callback) {
        "use strict";

        /*
        * TODO-lab1A
        *
        * LAB #1A: Implement the getCategories() method.
        *
        * Write an aggregation query on the "item" collection to return the
        * total number of items in each category. The documents in the array
        * output by your aggregation should contain fields for "_id" and "num".
        *
        * HINT: Test your mongodb query in the shell first before implementing
        * it in JavaScript.
        *
        * In addition to the categories created by your aggregation query,
        * include a document for category "All" in the array of categories
        * passed to the callback. The "All" category should contain the total
        * number of items across all categories as its value for "num". The
        * most efficient way to calculate this value is to iterate through
        * the array of categories produced by your aggregation query, summing
        * counts of items in each category.
        *
        * Ensure categories are organized in alphabetical order before passing
        * to the callback.
        *
        */

        /*
            db.item.aggregate([{$group: {_id: "$category", num: {$sum: 1}}}])
        */


       var collection = this.db.collection( 'item' );
       var cursor = collection.aggregate(
           [ 
               {'$group': {'_id': '$category', 'num': {'$sum': 1}}},
               {'$sort': {'_id': 1}}
           ], { cursor: { batchSize: 1 } }
        );

        cursor.toArray(function(error, categories) {
            assert.equal(error, null);
            var all = {"_id": "All", "num": 0}
            categories.forEach(element => {
               all.num += element.num;
            });
            categories.unshift(all);
            callback(categories);
        });
    }
~~~

~~~javascript
    this.getItems = function(category, page, itemsPerPage, callback) {
        "use strict";

        /*
         * TODO-lab1B
         *
         * LAB #1B: Implement the getItems() method.
         *
         * Create a query on the "item" collection to select only the items
         * that should be displayed for a particular page of a given category.
         * The category is passed as a parameter to getItems().
         *
         * Use sort(), skip(), and limit() and the method parameters: page and
         * itemsPerPage to identify the appropriate products to display on each
         * page. Pass these items to the callback function.
         *
         * Sort items in ascending order based on the _id field. You must use
         * this sort to answer the final project questions correctly.
         *
         * Note: Since "All" is not listed as the category for any items,
         * you will need to query the "item" collection differently for "All"
         * than you do for other categories.
         *
         */

         /*
            db.item.find(query).skip(page).limit(itemsPerPage).sort({_id:1})
         */

        var query = {};
        if (category != 'All') {
         query.category = category
        }
        
        var collection = this.db.collection( 'item' );
        var cursor = collection.find(query)
        .skip(page*itemsPerPage)
        .limit(itemsPerPage)
        .sort({_id:1});

        cursor.toArray(function(error, pageItems) {
            assert.equal(error, null);
            callback(pageItems);
        });
    }
~~~

~~~javascript
    this.getNumItems = function(category, callback) {
        "use strict";

        var numItems = 0;

        /*
         * TODO-lab1C:
         *
         * LAB #1C: Implement the getNumItems method()
         *
         * Write a query that determines the number of items in a category
         * and pass the count to the callback function. The count is used in
         * the mongomart application for pagination. The category is passed
         * as a parameter to this method.
         *
         * See the route handler for the root path (i.e. "/") for an example
         * of a call to the getNumItems() method.
         *
         */

         /* 
            db.item.aggregate([{$match: {'category': 'Stickers'}}, {$group: {_id: '$category', numItems: {$sum: 1}}}])
         */

        var queries = [];
        if (category != 'All') {
            queries = [{'$match': {'category': category}},{'$group': {'_id': '$category', 'numItems': {'$sum': 1}}}];
        }
        else {
            queries = [{'$group': {'_id': 'null', 'numItems': {'$sum': 1}}} ];
        }

        var collection = this.db.collection( 'item' );
        var cursor =  collection.aggregate(queries );

        cursor.toArray(function(error, count) {
            assert.equal(error, null);
            callback(count[0].numItems);
        });
    }
~~~

## Result

Gray Hooded Sweatshirt




