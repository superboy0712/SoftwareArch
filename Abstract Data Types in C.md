#Abstract data types in C

##What's an abstract data type? 
A modification to a program commonly requires a change in one or more of its data structures. For instance, a new field might be added to a personnel record to keep track of more information about each individual; an array might be replaced by a linked structure to improve the program's efficiency; or a bit field might be changed in the process of moving the program to another computer. You don't want such a change to require rewriting every procedure that uses the changed structure. Thus, it is useful to separate the use of a data structure from the details of its implementation. This is the principle underlying the use of abstract data types.

Here are some examples.

  +  stack: operations are "push an item onto the stack", "pop an item from the stack", "ask if the stack is empty"; implementation may be as array or linked list or whatever.
  +  queue: operations are "add to the end of the queue", "delete from the beginning of the queue", "ask if the queue is empty"; implementation may be as array or linked list or heap.
  +  search structure: operations are "insert an item", "ask if an item is in the structure", and "delete an item"; implementation may be as array, linked list, tree, hash table, ... 
