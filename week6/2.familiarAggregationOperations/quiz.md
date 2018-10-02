## Quiz

Which of the following are true with respect to constructing aggregation pipelines? Check all that apply.

- You should try to include $match stages as early as possible in your pipeline.
- $sort, $skip, and $limit are always performed in that order regardless of where they appear in an aggregation pipeline.
- $match, $project, $sort, $skip, and $limit stages are not strictly necessary in aggregation pipelines since those same operations are supported in the MongoDB query language.
- To filter documents using a $match stage, we use the same syntax for constructing query documents (filters) as we do for find().

## Answer

check [aggregation pipeline](https://docs.mongodb.com/manual/core/aggregation-pipeline/)

- You should try to include $match stages as early as possible in your pipeline. (se encarga de filtar es igual al find)
- To filter documents using a $match stage, we use the same syntax for constructing query documents (filters) as we do for find().



