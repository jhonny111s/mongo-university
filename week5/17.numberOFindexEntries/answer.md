## Question

Let's say you update a document with a key called tags and that update causes the document to need to get moved on disk. Assume you are using the MMAPv1 storage engine. If the document has 100 tags in it, and if the tags array is indexed with a multikey index, how many index points need to be updated in the index to accommodate the move? Put just the number below.

## Answer

- como el tag es un array, la cantidad de indices serán la longitud del array.

## Result

100

