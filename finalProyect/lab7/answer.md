
## Challenge

Note: This problem is ungraded. You do not need to submit your solution. This problem is more challenging and requires a little additional learning on your part. Feel free to discuss the problem in the discussion forum, but please don't just give away your solution.

In this lab, you will implement the method in cart.js necessary for updating the quantity of an item in a user's cart. The method you will implement in cart.js is updateQuantity(). This method is called from mongomart.js both when clicking "Add to cart" from the single item view page and when updating the quantity of an item using the quantity selector for an item in the user cart view.

The comments in updateQuantity() describe what you need to do to implement it. When you are finished, restart the mongomart.js application and test that both methods of increasing the quantity for an item in the cart work. Note that you should also be able to remove an item from the cart by setting the quantity to 0.

## Answer

~~~javascript
this.updateQuantity = function(userId, itemId, quantity, callback) {
    "use strict";

    var updateDoc = {};

    if (quantity == 0) {
        updateDoc = { "$pull": { items: { _id: itemId } } };
    } else {
        updateDoc = { "$set": { "items.$.quantity": quantity } };
    }

    this.db.collection("cart").findOneAndUpdate(
        { userId: userId,
          "items._id": itemId },
        updateDoc,
        { returnOriginal: false },
        function(err, result) {
            assert.equal(null, err);
            console.log(result.value);
            callback(result.value);
        });

}
~~~



