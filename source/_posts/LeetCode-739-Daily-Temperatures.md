---
title: '[LeetCode] 739. Daily Temperatures'
date: 2019-12-18 13:10:49
tags:
    - [LeetCode (Medium)]
    - [Stack]

categories:
    - [LeetCode Medium]
    - [Stack]
---

### Description:
Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

<!-- more -->

#### Note: 
- The length of temperatures will be in the range [1, 30000]. 
- Each temperature will be an integer in the range [30, 100].

---

### Solution One : Stack
#### Explaination
1. Process indices i in descending order. We'll keep a stack of indices such that T[stack[-1]] < T[stack[-2]] < ..., where stack[-1] is the top of the stack, stack[-2] is second from the top, and so on.
2. We will maintain this invariant as we process each temperature. 
3. After, it is easy to know the next occurrence of a warmer temperature: it's simply the top index in the stack.
4. Here is an example of the contents of the stack as work through T = [73, 74, 75, 71, 69, 72, 76, 73] in reverse order, at the end of the loop (after adding T[i]). For clarity, stack only contains indices i, but we'll write the value of T[i] beside it in brackets, such as o (73).
	
> When i = 7, stack = [7 (73)]. ans[i] = 0.
When i = 6, stack = [6 (76)]. ans[i] = 0.
When i = 5, stack = [5 (72), 6 (76)]. ans[i] = 1.
When i = 4, stack = [4 (69), 5 (72), 6 (76)]. ans[i] = 1.
When i = 3, stack = [3 (71), 5 (72), 6 (76)]. ans[i] = 2.
When i = 2, stack = [2 (75), 6 (76)]. ans[i] = 4.
When i = 1, stack = [1 (74), 2 (75), 6 (76)]. ans[i] = 1.
When i = 0, stack = [0 (73), 1 (74), 2 (75), 6 (76)]. ans[i] = 1.


Run the below code, you can get some explaination output. 
```java
public class dailyTemperatures {
    public int[] daily_Temperatures(int[] T) {
        int[] result = new int[T.length];
        System.out.println("Initial result array : " + Arrays.toString(result));
        Stack<Integer> stack = new Stack<>();
        System.out.println("Initial stack : " + Arrays.toString(stack.toArray()) + '\n');
        
        for (int i = T.length - 1; i >= 0 ; --i)
        {
        	System.out.println("When i is " + i + " | Now stack is : " + Arrays.toString(stack.toArray()) + " ");

        	while (!stack.isEmpty() && T[i] >= T[stack.peek()]) 
        	{
            	System.out.println("Now T[" + i + "] = " + T[i] + ". The top of the stack is : " + stack.peek());
            	System.out.println("T[" + stack.peek() + "] = " + T[stack.peek()]);
            	System.out.println("Because T[" + i + "](" + T[i] + ") >= T[" + stack.peek() + "](" + T[stack.peek()]+ "), so " + stack.peek() + " will be removed from stack.");
            	System.out.print("Now the new stack after removing " + stack.peek() + " is : ");
            	stack.pop();
            	System.out.print(Arrays.toString(stack.toArray()) + '\n');
        	}
        	result[i] = stack.isEmpty() ? 0 : stack.peek() - i;
            if (result[i] == 0)
                System.out.print("Because the stack is empty, so ");
            else
            	System.out.print("The stack is not empty, result[" + i + "] will be (the top element from the stack - 1), so ");
            System.out.println("result[" + i + "] = " + result[i]);
            stack.push(i);
            System.out.println(i + " will be pushed to the stack, now the stack is : " + Arrays.toString(stack.toArray()));
            System.out.println("The result for this loop is : " + Arrays.toString(result));
            System.out.println();
        }
        
    	return result;
    }
    
    public static void main(String[] args) {
    	dailyTemperatures temp = new dailyTemperatures();
    	int[] T = {73, 74, 75, 71, 69, 72, 76, 73};
    	
    	int [] result = temp.daily_Temperatures(T);
    	System.out.println("result is : " + Arrays.toString(result));
    }
}
```

The output of above code

```
Initial result array : [0, 0, 0, 0, 0, 0, 0, 0]
Initial stack : []

When i is 7 | Now stack is : [] 
Because the stack is empty, so result[7] = 0
7 will be pushed to the stack, now the stack is : [7]
The result for this loop is : [0, 0, 0, 0, 0, 0, 0, 0]

When i is 6 | Now stack is : [7] 
Now T[6] = 76. The top of the stack is : 7
T[7] = 73
Because T[6](76) >= T[7](73), so 7 will be removed from stack.
Now the new stack after removing 7 is : []
Because the stack is empty, so result[6] = 0
6 will be pushed to the stack, now the stack is : [6]
The result for this loop is : [0, 0, 0, 0, 0, 0, 0, 0]

When i is 5 | Now stack is : [6] 
The stack is not empty, result[5] will be (the top element from the stack - 1), so result[5] = 1
5 will be pushed to the stack, now the stack is : [6, 5]
The result for this loop is : [0, 0, 0, 0, 0, 1, 0, 0]

When i is 4 | Now stack is : [6, 5] 
The stack is not empty, result[4] will be (the top element from the stack - 1), so result[4] = 1
4 will be pushed to the stack, now the stack is : [6, 5, 4]
The result for this loop is : [0, 0, 0, 0, 1, 1, 0, 0]

When i is 3 | Now stack is : [6, 5, 4] 
Now T[3] = 71. The top of the stack is : 4
T[4] = 69
Because T[3](71) >= T[4](69), so 4 will be removed from stack.
Now the new stack after removing 4 is : [6, 5]
The stack is not empty, result[3] will be (the top element from the stack - 1), so result[3] = 2
3 will be pushed to the stack, now the stack is : [6, 5, 3]
The result for this loop is : [0, 0, 0, 2, 1, 1, 0, 0]

When i is 2 | Now stack is : [6, 5, 3] 
Now T[2] = 75. The top of the stack is : 3
T[3] = 71
Because T[2](75) >= T[3](71), so 3 will be removed from stack.
Now the new stack after removing 3 is : [6, 5]
Now T[2] = 75. The top of the stack is : 5
T[5] = 72
Because T[2](75) >= T[5](72), so 5 will be removed from stack.
Now the new stack after removing 5 is : [6]
The stack is not empty, result[2] will be (the top element from the stack - 1), so result[2] = 4
2 will be pushed to the stack, now the stack is : [6, 2]
The result for this loop is : [0, 0, 4, 2, 1, 1, 0, 0]

When i is 1 | Now stack is : [6, 2] 
The stack is not empty, result[1] will be (the top element from the stack - 1), so result[1] = 1
1 will be pushed to the stack, now the stack is : [6, 2, 1]
The result for this loop is : [0, 1, 4, 2, 1, 1, 0, 0]

When i is 0 | Now stack is : [6, 2, 1] 
The stack is not empty, result[0] will be (the top element from the stack - 1), so result[0] = 1
0 will be pushed to the stack, now the stack is : [6, 2, 1, 0]
The result for this loop is : [1, 1, 4, 2, 1, 1, 0, 0]

result is : [1, 1, 4, 2, 1, 1, 0, 0]
```

