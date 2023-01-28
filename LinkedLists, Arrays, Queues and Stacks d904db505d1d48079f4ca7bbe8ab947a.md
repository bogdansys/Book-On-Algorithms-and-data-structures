# LinkedLists, Arrays, Queues and Stacks

## Array definition:

- all elements are the same type
- fixed length
- elements are accessed by index

## Operations:

- **Inserting:** inserting at a certain index is done by shifting all subsequent elements forward (updating the references) and then filling the 'empty' slot
- **Removing:** removing at a certain index is done by shifting all subsequent elements backwards (updating the references)
- **Insertion sort:**
- Start at index 1
- Scan array from left to right, one element at a time. Place that element in a temporary variable.
- Compare with previous elements (from the back to the front) and check where the element should be placed
- **Expanding capacity:** make a deep copy into a larger array, an expansion with at most﻿ *n* additional positions take up O(n) time and O(n) space
- **Clone** makes a shallow copy, it makes an object but it reference the original.
- **Deep copy**: makes identical copies of what is inside the original array (is recursive)

For an array with **n** elements, the following operations have the time complexity:

- insert at end O(n)
- insert at end O(1)
- access O(1)
- remove O(n)
- clone O(n)

## (Dis)advantages:

- *Advantages:* it keeps elements in a specific order and they are efficiently accessible by index
- *Disadvantages:* it has a predetermined fixed size which is costly to expand, insert or delete

# **Linked Lists**

# Disclaimer

All the methods marked with ****** are methods which could be used internally, but aren't part of the spec, meaning, you can't use those methods!

# Singly Linked List (SLL)

*This is about chapter 3.2, 3.5.2 and 3.6.2 in the textbook*

## SLL definition:

- A list is a sequence of nodes starting from a **head** pointer.
- Each node will **reference** to an element and another node.
- Last node is the **tail** of a node, its next reference is null.
- The way we move through the list we call **traversal**, we jump from node to node.

## Operations:

- **Insert at the head:** To insert we create a new node with as reference null, then we insert this new node to the list by referencing it to the head. We only need to update our head pointer to the new first node in the list. The new node was a local variable, which will be cleaned up by garbage collection (in Java).
- **Insert at the tail:** The only way to find the tail is by traversing the list (this is highly inefficient). We fix this by “cheating” by creating a new reference directly to the tail. Than we update the old tail to the new tail (which is the element we inserted).
- **Remove the head:** We update the head pointer to the new head and the garbage collection will clean the previous head
- ***Remove the tail:** Traverse the list to find the node before the tail, then set the 'next' reference of that node to **null.** The previous tail node will be cleaned by garbage collection.

For a list with **n** elements, the following operations have the time complexity:

- *****Access element by index *O*(*n*)
- *****Search element  *O*(*n*)
    
    -Insert element
    
    **at the head** *O*(1)
    
    **at the tail** *O*(1)
    

      -Removing element

     **at the head** *O*(1)

******at the tail *O*(*n*)

- *****Clone/copy array *O*(*n*)

## (Dis)advantages:

- *Advantages:* it grows efficiently as needed
- *Disadvantages:* accessing elements requires traversal, can't easily remove tail or in the middle

# Circularly Linked List (CLL)

*This is about chapter 3.3 in the textbook*

## CLL definition:

- It is a **SLL** but the **tail**'s **next** points to **head**, instead of **null** (so there's no explicit head)

## Operations:

- **Rotate:** sets the tail to the next element
- **Insert at the head:** We need to create a new node, set the **next** reference to the **“tail.next”** reference. Then we need to update the **tail.next** reference so it points to the new node. Again new node is a local variable in the method, so it will not exist after performing the operation.
- **Insert at the tail:** Insert the first node at the **head**, then you need to update the **tail** reference to the new node.
- **Remove the head:** Get an explicit pointer to the head, if identical to tail (length == 1), set **tail** to **null**. Otherwise, set **tail**'s **next** to **head**'s **next**.

For a list with **n** elements, the following operations have the time complexity:

- *****Access element by index *O*(*n*)
- *****Search element *O*(*n*)

Insert element

**at the head** *O*(1)

**at the tail** *O*(1)

Removing element

**at the head** *O*(1)

******at the tail *O*(*n*)

- *****Clone/copy array *O*(*n*)

## (Dis)advantages:

- *Advantages:* it grows efficiently as needed, natural representation of cyclic data
- *Disadvantages:* accessing elements requires traversal, can't easily remove tail or in the middle

# Doubly Linked List (DLL)

*This is about chapter 3.4 in the textbook*

## DLL definition:

- Each node contains a element, next reference and prev reference.
- There are two dummy nodes (**header** and **trailer**), which only include references. They avoid the need voor special cases. You don’t need them, it is handy to do so (seems like it is really important)
- Creation of DLL:
- **Create header**: element, prev and next all have values **null**
- **Create trailer:** element and next have values **null** and prev has value **header**
- Point **header**'s **next** to **trailer**

## Operations:

- ***Insert at element:** Create a new node, set the **prev** pointer to the predecessor and the **next** to the successor node. Then update the references on the predecessor and successor nodes to point to the newly created node
- ***Remove at element:** If you want to remove node (**node**), ****get predecessor (**pred**) and successor (**succ**) nodes, set **pred.next = node.next** and **succ.prev = node.prev**
- **Insert** **at the head:** Insert node between **header** and **header.next**
- **Insert at the tail**: Insert node between **trailer** and **trailer.prev**
- **Remove the head:** Point the **header.next** to **header.next.next**
- **Remove the tail:** Point the **trailer.prev** to **trailer.prev.prev**

For a list with **n** elements, the following operations have the time complexity:

- *****Access element by index *O*(*n*)
- *****Search element *O*(*n*)

Insert element

**at the head** *O*(1)

**at the tail** *O*(1)

Removing element

**at the head** *O*(1)

**at the tail** *O*(1)

- *****Clone/copy array *O*(*n*)

## (Dis)advantages:

- *Advantages:* it grows efficiently as needed, efficient insertion/deletion at head and tail
- *Disadvantages:* accessing elements requires traversal, added space for **prev** references

# **Stacks**

## Stack definition:

- Stack (pile) of elements
- We can only access/modify the top of the stack
- Using the **last-in**, **first-out** principle (**LIFO**):
- Elements can be inserted at any time
- Only the last inserted element (top of stack) can be accessed or deleted
- A stack is an **Abstract Data Type (ADT),** it is an abstraction of a data structure, it cannot be instantiated. It contains:
- Signatures of operations on the data structure
- Perhaps constants, default or static methods

## Operations:

- **Push:** insert element onto the stack
- **Pop:** remove element from the top of the stack
- **Top/peek:** access top element without removing it
- **Size:** get the size of the stack
- **isEmpty:** returns whether the stack is empty

## Implementations:

There are a few types of implementations of stacks:

- **Array-based:**
- Stores elements in an array of **fixed** capacity*C*
- **Top** element: index*t*﻿, at the end of the array, proving efficient insertion/deletion
- Stack size: ﻿**t+1*t*+1**﻿ (as it's zero-indexed)
- **List-based:**
- **Top** is the **head** of the list, for efficient insertion/deletion
- It reuses **SLL** methods (**adapter** design pattern)

## Complexity

**Space**

Array: fixed capacity so wastes space if overdimensioned and costs time if underdimensioned

List: grows efficiently but uses more space per element than the array

Time O(1) all operations

# **Queues**

## Queue definition:

- Collection of objects
- Using the **first-in**, **first-out** principle (**FIFO**):
- Elements can be inserted at any time
- Only the element that has been the longest in the queue can be accessed or deleted

## Operations:

- **Enqueue:** adds element to the tail of the queue
- **Dequeue:** removes & returns the head element
- **First:** access top element without removing it
- **Size:** get the size of the queue
- **isEmpty:** returns whether the queue is empty

## Circular queue:

Used to add the front element to the end. Almost the same as a queue, but now with an extra **rotate** operation to do so efficiently (comparable to **CLL**). So this has a tail and an implicit head, which it shifted on each **rotate** operation.

# Double-ended queue (deque)

## Deque definition:

- Almost the same as a queue, but then people are removable from the front and the tail

## Implementations:

- **Array-based**
    - Just like in the queue, we should use a circular array
    - Now, when we insert from the front, we should decrement﻿ in a circular fashion and make sure it doesn't become negative
- **List-based (DLL);**
    - It already is a deque