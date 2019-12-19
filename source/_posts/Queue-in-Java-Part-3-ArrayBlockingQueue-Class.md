---
title: Queue in Java | Part 3 - ArrayBlockingQueue Class
date: 2019-12-19 22:44:02
tags:
    - [Data Structure]
    - [Queue]
categories:
    - [Data Structure]
    - [Queue]
---

### Introduction - ArrayBlockingQueue
*ArrayBlockingQueue* class is a bounded blocking queue backed by an array. By bounded it means that the size of the Queue is fixed. Once created, the capacity cannot be changed. Attempts to put an element into a full queue will result in the operation blocking. Similarly attempts to take an element from an empty queue will also be blocked. Boundness of the *ArrayBlockingQueue* can be achieved initially by passing capacity as the parameter in the constructor of *ArrayBlockingQueue*.<!-- more --> This queue orders elements **FIFO(first-in-first-out)**. It means that the head of this queue is the oldest element of the elements present in this queue. The tail of this queue is the newest element of the elements of this queue. The newly inserted elements are always inserted at the tail of the queue, and the queue retrieval operations obtain elements at the head of the queue. 

This class and its iterator implement all of the optional methods of the Collection and Iterator interfaces. This class is a member of the Java Collections Framework. 

#### Class Heirarchy
```java
java.lang.Object 
    ↳ java.util.AbstractCollection 
        ↳ java.util.AbstractQueue 
            ↳ java.util.concurrent.ArrayBlockingQueue
```

> **Type Parameters**: The type parameter of ArrayBlockingQueue E is the type of elements held in this collection

##### Implemented Interfaces
Following are the interfaces implemented by the ArrayBlockingQueue Class
	
- Serializable
- Iterable
- Collection
- BlockingQueue
- Queue

#### Syntax
```java
public class ArrayBlockingQueue
    extends AbstractQueue
        implements BlockingQueue, Serializable
```

#### Constructor Summary
-  ArrayBlockingQueue(int capacity)
    - Creates an ArrayBlockingQueue with the given(fixed) capacity and default access policy
- ArrayBlockingQueue(int capacity, boolean fair)
    - Creates an ArrayBlockingQueue with ths given(fixed) capacity and the specified access policy. If the fair value is true then queue accesses for threads blocked on insertion or removal, are processed in FIFO order; if false the access order in unspecified. 
- ArrayBlockingQueue(int capacity, boolean fair, Collection c)
	- Creates an ArrayBlockingQueue with the given(fixed) capacity, the specified access policy and initially containing the elements of the given collection, added in traversal order of the collection's iterator. If the fair value is true then queue accesses for threads blocked on insertion or removal, are processed in FIFO order; if false the access order is unspecified. 

---

### Method Summary
- **boolean add(E e)**
	- Inserts the specified element at the tail of this queue if it is possible to do so immediately without exceeding the queue's capacity, returning true upon success and thrwoing an IllegalStateException if this queue is full.
- **void clear()**
	- Atomically removes all of the elements from this queue.
- **boolean contains(Object o)**
	- Returns true if this queue contains the specified element.
- **int drainTo(Collection c)**
	- Removes all available elements from this queue and adds them to the given collection
- **int drainTo(Collection c, int maxElements)**
	- Removes at most the given number of available elements from this queue and adds them to the given collection.
- **Iterator iterator()**
	- Returns an iterator over the elements in this queue in proper sequence.
- **boolean offer(E e)**
	- Inserts the specified element at the tail of this queue if it is possible to do so immediately without exceeding the queue's capacity, returning true upon success and false if this queue is full.
- **Boolean offer(E e, long timeout, TimeUnit unit)**
	- Inserts the specified element at the tail of this queue, waiting up to the specified wait time for space to become available if the queue is full. 
- **E peek()**
	- Retrieves, but does not remove, the head of this queue, or returns null if this queue is empty.
- **E poll()**
    - Retrieves and removes the head of this queue, or returns null if this queue is empty.
- **E poll(long timeout, TimeUnit unit)**
	- Retrieves and removes the head of this queue, waiting up to the specified wait time if necessary for an element to become available.
- **void put(E e)**
	- Inserts the specified element at the tail of this queue, waiting for space to become available if the queue is full
- **int remainingCapacity()**
	- Returns the number of additional elements that this queue can ideally (in the absence of memory or resource constraints) accept without blocking
- **boolean remove(Object o)**
	- Removes a single instance of the specified element from this queue, if it is present.
- **int size()**
	- Returns the number of elements in this queue
- **Spliterator spliterator()**
	- Returns a Spliterator over the elements in this queue
- **E take()**
	- Retrieves and removes the head of this queue, waiting if necessary until an element becomes available.
- **Object[] toArray()**
	- Returns an array containing all of the elements in this queue, in proper sequence; the runtime type of the returned array is that of the specified array.
- **T[] toArray(T[] a)**
	- Returns an array containing all of the elements in this queue, in 0proper sequence; the runtime type of the returned array is that of the specified array.
- **String toString()**
	- Returns a string representation of this collection.



















