# Stack and Queue
stack is a data structure consists of Nodes , each Node stores a value and a reference to the next node , but does not reference to its previous.

comon terminology in stack :
1. Push: to add a Node to the stack
2. Pop: to remove a node from the stack
3. Top:to refer to the top of stack
4. Peek: to refer to the value of the top Node
5. IsEmpty: it returns True if the stack is empty 

### Stack follow these concepts:
#### FILO: first in last out

this means the first item to enter the stack should be the last item to be popped out of the stack>

#### LIFO: last in first out
this means that the last item added to the stack should be the first item to be popped out of the stack


## Stack Visualization 
the following imag is a representation of a stack , its shows the top , and every node has the refernece to the next node and the value . 
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/stack1.PNG)

### Push O(1):
pushing a Node will always be an O(1), because adding a node will take the same amount of time regardless of the number of nodeds (n) in the stack.

when pushing a new node , we add it to the top of the stack, this means we need to assign it as a top and its (next) should point to the original top
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/pushStack2.PNG)
### Pop O(1):
popping a node off a stack means removing the top Node, to do that you need to assign reassign the top to the current top next Node , and the pop should return the value of the deleted Node

to perform a pop, you need to assign the currrent top Node to a temp node, then you need to change the top to the current top next value , then you should change the next of the temp node to none , and return the temp value.
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/popStack3.PNG)

### Peek O(1):
this method is to check the top node of the stack and returns its value

### IsEmpty O(1):

this method is to check if the stack is empty , we do this by checking if the top node exist , ie not None, the we return False if there is a top Node , and True if there is no top Node.


-----
# Queue
 
 1. Enqueue - Nodes or items that are added to the queue.
 2. Dequeue - Nodes or items that are removed from the queue. If called when the queue is empty an exception will be raised.
 3. Front - This is the front/first Node of the queue.
 4. Rear - This is the rear/last Node of the queue.
 5. Peek - When you peek you will view the value of the front Node in the queue. If called when the queue is empty an exception will be raised.
 6. IsEmpty - returns true when queue is empty otherwise returns false.

### Queues follow these concepts:
#### FIFO: First In First Out

This means that the first item in the queue will be the first item out of the queue.

#### LILO: Last In Last Out
This means that the last item in the queue will be the last item out of the queue. 
## Queue Visualization :
queue is a data structure that has a Rear and Front Nodes , the following image is a visual representation of a Queue
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Queue.PNG)

### Enqueue O(1):
it is used to add a Node to the Rear of the Queue, this is done by adding the new Node as the Next of the Rear Node . and assign the new Node as the Rear.
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Enqueue3.PNG)

### Dequeue O(1):
to remove a node from the Front of the Queue and returns its value, this is done by assigning the the front to a temp value. and then change the front to the next of the original Front, then set the next of the temp node to None and return its value
![](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Dequeue3.PNG)

### Peek O(1):
this method is to check the Front node of the Queue and returns its value


### IsEmpty O(1):

this method is to check if the Queue is empty , we do this by checking if the Front node exist , ie not None, the we return False if there is a Front Node , and True if there is no top Node.




