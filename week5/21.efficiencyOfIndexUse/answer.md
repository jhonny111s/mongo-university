## Question

In general, based on the preceding lecture, what is the primary factor that determines how efficiently an index can be used?

- The number of fileds in a compund index
- Whether we are able to sort using the index
- The selectivity of the index.

## Answer

Selectivity is the primary factor that determines how efficiently an index can be used. Ideally, the index enables us to select only those records required to complete the result set, without the need to scan a substantially larger number of index keys (or documents) in order to complete the query. Selectivity determines how many records any subsequent operations must work with. Fewer records means less execution time.

## Result

 The selectivity of the index.
