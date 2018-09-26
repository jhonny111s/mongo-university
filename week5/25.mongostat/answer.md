## Question

Which of the following statements about mongostat output are true? Check all that apply.

- the mmap column field appears for all storage engines.
- The getmore column concerns the number of requests per time interval to get additional data from a cursor
- only the wiredTiger storage engine reports the resident memory size of the database.
- the faults column appears only in the mmapv1 output
- by default, mongostat provides information in 100ms increments.

## Answer

- mongostat es un comando que muestra algunos valores utiles de las instancias que corren de mongo.
- en una pestaña aparte correr "mongostat".

## Result

- The getmore column concerns the number of requests per time interval to get additional data from a cursor.
- the faults column appears only in the mmapv1 output
