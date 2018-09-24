
## Question

The cart.js file implements data access for the cart collection. The cart collection contains the shopping carts for users of the MongoMart application.

The mongomart.js application instantiates a cart data access object (DAO) with this call:

~~~javascript
var cart = new CartDAO(db);
~~~

The DAO, cart, is used throughout mongomart.js to implement several of the routes in this application.

In this lab, you will implement the method in cart.js necessary to support the route for viewing a shopping cart. This route is implemented in mongomart.js in the function that begins with this line:

~~~javascript
router.get("/cart", function(req, res) {
~~~

The method you will implement in cart.js is: getCart(). The comments in this method describe what you need to do to implement it. When you are finished, restart mongomart.js application and answer the question below.

Click the "Cart" button in the upper right corner of the MongoMart home page. There are already several items in the user cart. Which of the following values is closest to the total value of items in the cart REPORTED ON THAT PAGE?

- $100
- $200
- $300
- $400
- $500

## Answer

~~~javascript
    this.getCart = function(userId, callback) {
        "use strict";

        /*
        * TODO-lab5
        *
        * LAB #5: Implement the getCart() method.
        *
        * Query the "cart" collection by userId and pass the cart to the
        * callback function.
        *
        */

       var collection = this.db.collection( 'cart' ); 
       collection.findOne({'userId': userId}, function(error, item) {
        assert.equal(error, null);
        callback(item);
    });
    }
~~~

## Result

- $400  (399.97)



