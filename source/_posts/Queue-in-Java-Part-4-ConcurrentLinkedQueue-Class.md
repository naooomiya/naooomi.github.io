---
title: Queue in Java | Part 4 ConcurrentLinkedQueue Class
date: 2019-12-21 22:00:38
tags:
    - [Data Structure]
    - [Queue]
categories:
    - [Data Structure]
    - [Queue]
---

### Intriduction - ConcurrentLinkedQueue
The *ConcurrentLinkedQueue* class in Java is part of the Java Collection Framework and implements the Collection Interface and the AbstractCollection class. It is used to implement Queue with the help of LinkedList concurrently. 

<!-- more -->

#### Class Hierarchy
```java
java.lang.Object
  ↳ java.util.AbstractCollection<E>
     ↳ java.util.AbstractQueue<E>
        ↳ Class ConcurrentLinkedQueue<E>
```

#### Syntax
```java
public abstract class ConcurrentLinkedQueue<E>
    extends AbstractCollection<E>
        implements Queue<E>, Serializable
```
where E is the type of elements maintained 
by this collection

#### Constructors in Java ConcurrentLinkedQueue
- **ConcurrentLinkedQueue()**: This constructor is used to construct an empty queue.
- **ConcurrentLinkedQueue(Collection<E> c)**: This constructor is used to construct a queue with the elements of the Collection passed as the parameter.

---

### Methods in Java ConcurrentLinkedQueue
- **add(E e)**
	- This method inserts the specified element at the tail of this queue.
- **addAll(Collection c)**
	- This method appends all the elements in the specified collection to the end of this queue, in the order that they are returned by the specified collections's iterator.
- **contains(Object o)**
	- This method returns true if this queue contains the specified element.
- **isEmpty()**
	- This method returns true if this queue contains no elements
- **iterator()**
	- This method returns an iterator over the elements in this queue in proper sequence.
- **offer(E e)**
	- This method inserts the specified element at the tail of this queue.
- **peek()**
	- This method retrieves, but does not remove, the head of this queue, or returns null if this queue is empty.
- **poll()**
	- This method retrieves and removes the head of this queue, or returns null if this queue is empty.
- **remove(Object o)**
	- This method removes a single instance of the specified element from this queue, if it is present.
- **size()**
	- This method returns the number of elements in this queue
- **spliterator?()**
	- This method returns an array containing all of the elements in this queue, in proper sequence.
- **toArray()**
	- This method returns an array containing all of the elements in this queue, in proper sequence.
- **toArray(T[] a)**
	- This method returns an array containing all of the elements in this queue, in proper sequence; the runtimet type of the returned array is that of the specified array.

#### Examples
```java
import java.util.concurrent.ConcurrentLinkedQueue;
// Small Java Program to demonstrate ConcurrentLinkedQueue
public class ConcurrentLinkedQueueDemo {
    public static void main (String[] args)
    {
        // Create a ConcurrentLinkedQueue
        // Using ConcurrentLinkedQueue() constructor
        ConcurrentLinkedQueue<Integer> clq1 = new ConcurrentLinkedQueue<Integer>();
        
        clq1.add(11);
        clq1.add(22);
        clq1.add(33);
        clq1.add(44);
        
        // Displaying the existing LinkedQueue
        System.out.println("ConcurrentLinkedQueue : " + clq1);
        
        // Create a ConcurrentLinkedQueue
        // Using ConcurrentLinkedQueue(Collection c) constructor
        ConcurrentLinkedQueue<Integer> clq2 = new ConcurrentLinkedQueue<Integer>(clq1);
        
        // Displaying the existing LinkedQueue
        System.out.println("ConcurrentLinkedQueue : " + clq2);
                
        // Displaying the first element
        // using peek() method
        System.out.println("First element is : " + clq2.peek());
        
        // Remove and display the first element
        // using poll() method
        System.out.println("Head element is : " + clq2.poll());
        
        // Displaying the existing LinkedQueue
        System.out.println("ConcurrentLinkedQueue : " + clq2);
        
        // Get the size using size() method
        System.out.println("Size : " + clq2.size());
    }
}
```

#### Example output
```java
ConcurrentLinkedQueue : [11, 22, 33, 44]
ConcurrentLinkedQueue : [11, 22, 33, 44]
First element is : 11
Head element is : 11
ConcurrentLinkedQueue : [22, 33, 44]
Size : 3
```


















