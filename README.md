# a6
Submit source code files (main.c, slist.c, slist.h) to Gradescope.

**ADTs and Deques**

An abstract data type (ADT) is a model of how data can be stored and accessed without specifying a concrete implementation. Examples include stacks, queues, priority queues,dictionaries. The Java Collections Framework and the Standard Template Library in C++ provide support for these ADTs. In the C programming language we need to implement most of these ADTs ourselves. An ADT is usually implemented with basic data structures such as arrays or linked lists. The interface or set of operations that the ADT supports effectively hides the implementation details.
A double-ended queue, or deque, is an abstract data type which stores data as a sequence that can be accessed at both ends. One end is referred to as the 'front' and the other the 'back', but data can be added to or removed from either end. The basic operations supported by a deque are:

  push_back( data )
  
  push_front( data )
  
  data pop_back( )
  
  data pop_front( )
  
Deques are often implemented with a dynamic array or a doubly linked list. Here we will explore the use of a singly linked list to implement a deque.

**Requirements**

A program is needed to experiment with a deque that will be implemented with a singly linked list. The program should read names from a text file and push those names onto the back of a deque. The user should be prompted to enter 'f' to move forward through the names, 'b' to move backwards through the names, or 'q' to quit. When 'f' is pressed the program should display the name that is currently at the front of the queue by popping it off and then pushing it on the back of the queue. That way the next time they press 'f' the program will display the next name at the front of the deque and so on. The 'b' choice is similar but in the other direction (see example below). This allows the user to scroll through the names in either direction.

**Design**

Think about how each of the deque functions can be implemented with a singly linked list function. Draw a deque and try to understand how the program must work and then write some basic pseudocode to represent how you can use the deque operations to achieve the goal.

**Implementation**

The program will be written in C. You can use any code from the course slides. Try to write your program incrementally by first creating the overall structure with empty functions (stubs) and testing often to see that your program is always working as expected.

Organize your code as follows:

**main.c**

 void push_back(Deque* q, char* data)...
 
 void push_front(Deque* q, char* data)...
 
 char* pop_back(Deque* q)...
 
 char* pop_front(Deque* q)...
 
 int main(int argc, char* argv[])...

**slist.c / slist.h**

void insertHead(SList* list, char* data)...

char* removeHead(SList* list)...

void insertTail(SList* list, char* data)...

char* removeTail(SList* list)...

Each deque function in main.c is just a wrapper for one of the functions in slist.c. In main you can declare a deque, which is just a typedef of a singly linked list:

  Deque q = {NULL, NULL};

Then you can read the file and create a buffer for each name with something like:

  Bool done = F;
  while (!done)
  {
      char* name = malloc(MAX_NAME_LEN);
      if (fscanf(fp, "%s", name) == 1)
          push_back(&q, name);
      else
          done = T;
  }
  
**Testing**

When testing, you are checking to see that the program satisfies the requirements. Test to see that you can cycle through all the names from the file in both directions.
Here is an example 'names.txt' file that you should use:

Andrew

Betty

Candace

Dennis

Edward

After reading the file the resulting deque should be:

Andrew    Betty    Candace    Dennis    Edward
(front)                                 (back)

Here is an example run of the program:

To scroll through the names type
f: forwards, b: backwards, q: quit
f
Andrew
f
Betty
f
Candace
f
Dennis
f
Edward
f
Andrew
f
Betty
f
Candace
b
Candace
b
Betty
b
Andrew
b
Edward
b
Dennis
b
Candace
b
Betty
b
Andrew
b
Edward
q
Bye!
