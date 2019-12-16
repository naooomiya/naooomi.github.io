---
title: Queue in Java | Part 2 AbstractQueue
date: 2019-12-16 22:34:04
tags:
    - [Data Structure]
    - [Queue]
categories:
    - [Data Structure]
    - [Queue]
---

### Introduction
The **AbstractQueue** class in Java is a part of the Java Collection Framework and implements the Collection Interface and the AbstractCollection class. It provides skeletal implementations of some **Queue** operations. The implementations in this class are appropriate when the base implementation does not allow null elements.

<!-- more -->

##### All implemented Interfaces:
*Iterable<E>, Collection<E>, Queue<E>*

##### Direct Known Subclasses:
*ArrayBlockingQueue, ConcurrentLinkedQueue, DelayQueue, LinkedBlockingDeque, LinkedTransferQueue, PriorityBlockingQueue, PriorityQueue, SynchronousQueue*

#### Class Hierarchy:
```java
java.lang.Object
 ↳ java.util.AbstractCollection<E>
    ↳ Class AbstractQueue<E>
```
#### Syntax:
```java
public abstract class AbstractQueue<E>
  extends AbstractCollection<E>
     implements Queue<E>
```
Where E is the type of element maintained by this collection class.

#### Constructors in Java AbstractQueue:
- **protected AbstractQueue()**: The default constructor, but being protected, it doesn't allow to create an AbstractQueue object.

#### Methods in Java AbstractQueue:
1. **add(E e)** : Inserts the specified element into this queue if it is possible to do so immediately without voilating capacity restrictions, returning true upon success and throwing an IllegalStateException if no space is currently available. 
2. **addAll(Collection c)** : Adds all of the elements in the specified collection to this queue.
3. **clear()** : Removes all of the elements from this queue.
4. **element()** : Retrives, but does not remove, the head of this queue. 
5. **remove()** : Retrieves and removes the head of this queue. 

#### Methods inherited from different class
| java.util.AbstractCollection | Java.lang.Object | interface java.util.Queue | interface java.util.Collection |
|:---:|:---:|:---:|:---:|
| contains, containsAll, isEmpty, interator, remove, removeAll, retainAll, size, toArray, toString | clone, equals, finalize, getClass, hashCode, notify, notifyAll, wait | offer, peek, poll | contains, containsAll, equals, hashCode, isEmpty, iterator, remove, removeAll, retainAll, size, toArray |
