
## Question

Get the MongoMart application up and running. It doesn't do much (yet), but you should be able to run it and experiment with the UI.

1. Download the MongoMart application from the handout.
2. Install the dependencies.
3. Make sure you have a mongod running version 3.2.x of MongoDB.
4. Import the "item" collection: mongoimport --drop -d mongomart -c item data/items.json
5. Import the "cart" collection: mongoimport --drop -d mongomart -c cart data/cart.json
6. Run the application by typing "node mongomart.js" in the mongomart directory.

In your browser, visit http://localhost:3000. If you've set up and launched MongoMart correctly, you should see a page that lists the same product repeated five times. Which of the following products is it?

- Gray Hooded Sweatshirt
- WiredTiger T-shirt 
- MongoDB University Book
- Powered by MongoDB Sticker
- Stress Ball


## Answer

- run "node mongomart.js inside folder


## Result

Gray Hooded Sweatshirt




