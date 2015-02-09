#Abstract data types in C

##What's an abstract data type? 
A modification to a program commonly requires a change in one or more of its data structures. For instance, a new field might be added to a personnel record to keep track of more information about each individual; an array might be replaced by a linked structure to improve the program's efficiency; or a bit field might be changed in the process of moving the program to another computer. You don't want such a change to require rewriting every procedure that uses the changed structure. Thus, it is useful to separate the use of a data structure from the details of its implementation. This is the principle underlying the use of abstract data types.

Here are some examples.

  +  stack: operations are "push an item onto the stack", "pop an item from the stack", "ask if the stack is empty"; implementation may be as array or linked list or whatever.
  +  queue: operations are "add to the end of the queue", "delete from the beginning of the queue", "ask if the queue is empty"; implementation may be as array or linked list or heap.
  +  search structure: operations are "insert an item", "ask if an item is in the structure", and "delete an item"; implementation may be as array, linked list, tree, hash table, ... 

There are two views of an abstract data type in a procedural language like C. 
  +  One is the view that the rest of the program needs to see: the names of the routines for operations on the data structure, and of the instances of that data type. 
  +  The other is the view of how the data type and its operations are implemented. C makes it relatively simple to hide the implementation view from the rest of the program. 

##Implementation of abstract data types in C 

In C, a complex data type is typically represented by a pointer to the information stored in the data type. A C function can pass the pointer to other functions without knowing the details of what the pointer points to. One may also use parts of a program that have been separately compiled. All that a part of a program need know about functions it calls is their names and the types they return.

Thus, the convention in C is to prepare two files to implement an abstract data type. One (whose name ends in ".c") provides the implementation view; it contains the complete declaration for the data type, along with the code that implements its associated operations. The other (whose name ends in ".h") provides the abstract view; it contains short declarations for functions, pointer types, and globally accessible data. 

The abstract data type "stack" might then be represented as follows:

**_stack.h_**
```c
	typedef struct StackStructType *StackType;
	
	/* Return a pointer to an empty stack. */
	extern StackType InitStack ( );
	/* Push value onto the stack, returning success flag. */
	extern boolean Push (int k);
	/* Pop value from the stack, returning success flag. */
	extern boolean Pop ( );
	/* Print the elements of the stack. */
	extern PrintStack (StackType stack);
```

**_stack.c_**
```c
	#include "stack.h"
	#define STACKSIZE 5
	struct StackStructType {		/* stack is implemented as */
		int stackItems [STACKSIZE];	/*  an array of items */
		int nItems;	/*  plus how many there are */
	};
	typedef struct StackStructType *StackType;
	
	/*
	**	Return a pointer to an empty stack.
	*/
	StackType InitStack ( ) {
		char *calloc( );
		StackType stack;
		stack = (StackType) calloc (1, sizeof (struct StackStructType));
		stack->nItems = 0;
		return (stack);
	}
	```

Parts of the program that need to use stacks would then contain a line
```c
	#include "stack.h"
```
