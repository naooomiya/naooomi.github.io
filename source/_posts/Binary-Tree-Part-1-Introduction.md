---
title: Binary Tree | Part 1 Introduction
date: 2020-02-05 21:48:09
tags:
    - [Binary Tree]
    - [Tree]
    - [Data Structure]

categories:
    - [Binary Tree]
    - [Data Structure]

---


### Trees
Unlike Arrays, Linked List, Stack and Queues, which are linear data structures, trees are hierarchical data structures in which each node has at most two children generally referred as left child and right child.

<!-- more -->

#### Each node contains three components:
- Pointer to the left subtree
- Pointer to the right subtree
- Data element

The topmost node in the tree is called the root. An empty tree is represented by NULL pointer.
A representation of binary tree is shown:

![Tree](https://i.imgur.com/YwhtrF8.png)

### Binary Tree: Common Terminologies
- **Root**: Topmost node in a tree
- **Parent**: Every node(excluding a root) in a tree is connected by a directed edge from exactly one other node. This node is called a parent
- **Child**: A node directly connected to another node when moving away from the root.
- **Leaf/External node**: Node with no children
- **Internal node**: Node with atleast one children
- **Depth of a node**: Number of edges from root to the node
- **Height of a node**: Number of edges from the node to the deepest leaf. Height of the tree is the height of the root. 

In the below binary tree we see that root node is **A**. The tree has 10 nodes with 5 internal nodes, i.e, **A, B, C, E, G** and 5 external nodes, i.e, **D, F, H, I, J**. The height of the tree is 3. **B** is the parent of **D** and **E** while **D** and **E** are children of **B**
	
![Binary Tree](https://i.imgur.com/LCKbt9l.png)
	
### Advantages of Trees
Trees are so useful and frequently used, because they have some very serious advantages:
- Trees reflect structural relationships in the data
- Trees are used to represent hierarchies
- Trees provide an efficient insertion and searching
- Trees are very flexible data, allowing to move subtrees around with minimum effort

### Types of Binary Trees(Based on Structure)
- **Rooted binary tree**: It has a root node and every node has atmost two children.
- **Full binary tree**: It is a tree in which every node in the tree has either 0 or 2 children.
	- The number of nodes, *n*, in a full binary tree is atleast *n = 2h - 1*, and atmost *n = 2^(h+1) − 1*, where *h* is the height of the tree
	- The number of leaf nodes *l*, in a full binary tree is number, L of internal nodes + 1, i.e, *l = L + 1*

![Full Binary Tree](https://i.imgur.com/Q6CSO5w.png)

- **Perfect binary tree**: it is a binary tree in which all interior nodes have two children and all leaves have the same depth or same level.
	- A perfect binary tree with *l* leaves has *n = 2l - 1* nodes
	- In perfect full binary tree, *l = 2h* and *n = 2h + 1 - 1*, where *n* is number of nodes, *h* is height of tree and *l* is number of leaf nodes. 

![Perfect Binary Tree](https://i.imgur.com/3jkMB9k.png)
	
- **Complete binary tree**: It is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible. 
	- The number of internal nodes in a complete binary tree of n nodes is floor(n/2)

![Complete Binary Tree](https://i.imgur.com/mLkz9t1.png)
	
- **Balanced binary tree**: A binary tree is height balanced if it satisfies the following constraints:
	- The left and right subtrees' heights differ by at most one, AND
	- The left subtree is balanced, AND
	 The right subtree is balanced

![Balanced Binary Tree](https://i.imgur.com/sLbNCFJ.png)

- Degenerate tree: It is a tree is where each parent node has only one child node. It behaves like a linked list. 

![Degenerate Tree](https://i.imgur.com/97qURYt.png)

### Traversals
A traversal is a process that visits all the nodes in the tree. Since a tree is nonlinear data structure, there is no unique traversal. We will consider several traversal algorithms with we group in the following two kinds
- **Depth-First Traversal(DFT)**
- **Breadth-First Traversal(BFT)**

There are three different types of depth-first traversals:
- **PreOrder traversal** - visit the parent first and then left and right children;
- **InOrder traversal** - visit the left child, then the parent and the right child;
- **PostOrder traversal** - visit left child, then the right child and then the parent;

There is only one kind of breadth-first traversal - **the level order traversal**. This traversal visits nodes by levels from top to bottom and from left to right.

As an example consider the following tree and its four traversal:

![Example](https://i.imgur.com/5A0q3Z1.png)

**PreOrder** - 8, 5, 9, 7, 1, 12, 2, 4, 11, 3
**InOrder** - 9, 5, 1, 7, 2, 12, 8, 4, 3, 11
**PostOrder** - 9, 1, 2, 12, 7, 5, 3, 11, 4, 8
**LevelOrder** - 8, 5, 4, 9, 7, 11, 1, 12, 3, 2


