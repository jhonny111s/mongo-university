## Question

Which of the following statements about the MMAPv1 storage engine are true? Check all that apply.

## Answer

- MMAPv1 offers document-level locking (It has collection level locking.)
- MMAPv1 automatically allocates power of two size documents when new documents are inserted. (This is handled by the storage engine)
- MMAPv1 is built on top of the mmap system call that maps files into memory. (This is the basic idea behind why we call it MMAPv1)
- mongodb manges the memory used by each mapped file, deciding wich parts to swap to disk. (The operating system handles this.)


## Result

- MMAPv1 automatically allocates power of two size documents when new documents are inserted.
- MMAPv1 is built on top of the mmap system call that maps files into memory.