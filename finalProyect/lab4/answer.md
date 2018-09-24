
## Question

In this lab, you will implement the method in items.js necessary to support the route for adding a review to a single item. This route is implemented in mongomart.js in the function that begins with this line:

~~~javascript
router.post("/item/:itemId/reviews", function(req, res) {
~~~

Note that this route uses a url parameter much like that used in the route for the single item view. However, this route supports POST rather than GET requests. To access the form values passed in the POST request, we use the "body" property of the request object passed to the callback function for this route.

To complete the functionality to support adding reviews, you will need to implement the addReview() method in items.js. The comments in this method describe what you need to do to implement it.

If you have completed this problem successfully, you should be able to add reviews to products. To test your code, experiment with adding reviews to the Leaf Sticker. To add a review, complete the "Add a Review" form on any individual product's page and click "Submit Review". You should see the review appear beneath the "Latest Reviews" heading. When correctly created, reviews will contain the following information: - The reviewer name - The date and time the review was made - The number of stars provided by the reviewer - The reviewer comments

When you are satisfied that your code is working, navigate to the Track Jacket page. Unless you've modified the data in some way you should see reviews from Shannon, Bob, and Jorge only. If you see reviews other than these, please drop the item collection and mongoimport it again, following the instructions in Lab 0.

Add a five-star review with a brief comment. Type any name and review comments you wish, but make sure you select five stars for your review.

After submitting this review, under "Product Description" the Track Jacket page now shows an average of how many stars?

- 1
- 2
- 3
- 4
- 5

## Answer

~~~javascript
this.addReview = function(itemId, comment, name, stars, callback) {
        "use strict";

        /*
         * TODO-lab4
         *
         * LAB #4: Implement addReview().
         *
         * Using the itemId parameter, update the appropriate document in the
         * "item" collection with a new review. Reviews are stored as an
         * array value for the key "reviews". Each review has the fields:
         * "name", "comment", "stars", and "date".
         *
         */

         /*
            db.item.updateOne({"_id": itemId},  {$addToSet: {reviews: reviewDoc}})
         */

        var reviewDoc = {
            name: name,
            comment: comment,
            stars: stars,
            date: Date.now()
        }

        var collection = this.db.collection( 'item' );
        collection.findOneAndUpdate(
            {'_id': itemId},
            {$addToSet: {reviews: reviewDoc}}, function(error, item) {
            assert.equal(error, null);
            callback(item);
        });
    }
~~~

## Result

4



