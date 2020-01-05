---
title: Dynamic Programming | Part 1 Overlapping Subproblems Property in DP
date: 2020-01-05 17:33:47
tags:
    - [Data Structure]
    - [Dynamic Programming]
categories:
    - [Data Structure]
    - [Dynamic Programming]
---


### Introduction - Dynamic Programming
*Dynamic Programming* is an algorithmic paradigm that solves a given complex problem by breaking it into subproblems and stores the results of subproblems to avoid computing the same results again. Following are the two main properties of a problem that suggests that the given problem can be solved using Dynamic Programming.

<!-- more -->

- Overlapping Subproblems(This part)
- Optimal Substructure(Next part)

### Overlapping Subproblems
Like Divide and Conquer, Dynamic Programming combines solutions to sub-problems. DP is mainly used when solutions of same subproblems are needed again and again. In DP, computed solutions to subproblems are stored in a table so that these don't have to be recomputed. So DP is not useful when there are no common(overlapping) subproblems because there is no point storing the solutions if they are not needed again. For example, Binary Search doesn't have common subproblems. If we take an example of following recursive program for Fibonacci Numbers, there are many subproblems which are solved again and again. 

```java
/* simple recursive program for Fibonacci numbers */
int fib(int n) 
{ 
   if ( n <= 1 ) 
      return n; 
   return fib(n-1) + fib(n-2); 
}
```

#### Recursion tree for execution of fib(5)
![Recursion tree for execution of fib(5)](https://i.imgur.com/hOFtfJ4.png)

We can see that the function fib(3) is being called 2 times. If we would have stored the value of fib(3), then instead of computing it again, we could have reused the old stored value. There are following two different ways to store the values so that these values can be reused: 

##### a) Memoization (Top Down)
The memoized program for a problem is similar to the recursive version with a small modification that it look into a lookup table before computing solutions. We initialize a lookup array with all initial values as NIL. Whenever we need the solution to a subproblem, we first look into the lookup table. If the precomputed value is there then we return that value, otherwise, we calculate the value and put the result in the lookup table so that it can be reused later. 

###### The Algorithm:
- Initialize a lookup array/table with all its elements as NIL
    - NIL is simply a constant value, e.g. -1, that signifies absence of a solution
- Call the recursive function f(n) to solve for 'n' using memoization
	-  At every step i, f(i) performs the following steps:
	- Checks whether table[i] is NIL or not
	- If it's not NIL, f(i)returns the value 'table[i]'
	- If it's NIL; and 'i' satisfies the base condition, we update the lookup table with the base value and return the same. 
	- If it's NIL and 'i' does not satisfy the base condition, then f(i) splits the problem 'i' into subproblems and recursively calls itself to solve them.
	- After the recursive calls return, f(i) combines the solutions to subproblems, updates the lookup table and returns the solution for problem 'i'

###### Memoized example for nth Fibonacci Number: 

```java
public class Fibonacci {
    final int MAX = 100;
    final int NIL = -1;
    
    int lookup[] = new int[MAX];
    
    /*Function to initialize NIL values in lookup table*/
    private void _initialize()
    {
        for (int i = 0; i < MAX; i++)
            lookup[i] = NIL;
    }
    
    /*Function for nth Fibonacci number*/
    private int fib(int n)
    {
        if (lookup[n] == NIL)
        {
            if (n <= 1)
                lookup[n] = n;
            else
                lookup[n] = fib(n-1) + fib(n-2);
        }
        return lookup[n];
    }
    
    public static void main(String[] args)
    {
        Fibonacci f = new Fibonacci();
        int n = 40;
        f._initialize();
        System.out.println("Fibonacci number is : " + f.fib(n));
    }
}
```

> Output: 
Fibonacci number is : 102334155

##### b) Tabulation (Bottom Up)
The tabulated program for a given problem build a table in bottom up fashion and returns the last entry from table. For example, for the same Fibonacci number, we first calculate fib(0) then fib(1) then fib(2) then fib(3) and so on. So literally, we are building the solutions of subproblems bottom-up. 

###### The algorithm:
- Build the lookup table in bottom up fashion
- After the table is built, simply return table[n]

###### Steps:
1. We begin with initializing the base values of 'i'
2. Next, we run a loop that iterates over the remaining values of 'i'
3. At every iteration i, f(n) updates the ith entry in the lookup table by combining the solutions to the previously solved subproblems
4. Finally, f(n) returns table[n]

Tabulated Example for nth Fibonacci Number:

```java
/*Java program for Tabulated version*/
public class Fibonacci {
    private int fib(int n)
    {
        int f[] = new int[n+1];
        f[0] = 0;
        f[1] = 1;
        
        for (int i = 2; i <= n; i++)
            f[i] = f[i-1] + f[i-2];
        return f[n];
    }
    
    public static void main(String[] args)
    {
        Fibonacci f = new Fibonacci();
        int n = 9;
        System.out.println("Fibonacci number is : " + f.fib(n));
    }
}
```

> Output:
Fibonacci number is : 34

Both Tabulated and Memoized store the solutions of subproblems. In Memoized version, table is filled on demand while in Tabulated version, starting from the first entry, all entries are filled one by one. Unlike the Tabulated version, all entries of the lookup table are not necessarily filled in Memoized version. For example, Memorized solution of the LCS problem doesn't necessarily fill all entries. 

### Comparation
#### Tabulation
- Works in bottom up fashion
- Avoids multiple lookups, thus, saves function call overhead time

#### Memoization
- Works in top down fashion
- Sometimes, avoids computing solutions to subproblems that are not needed, e.g., Longest Common Subsequence
- Sometimes, more intuitive to write, e.g., Matrix Chain Multiplication
