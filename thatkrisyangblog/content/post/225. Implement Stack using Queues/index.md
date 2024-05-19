--- 
title:  225. Implement Stack using Queues
description:  225. Implement Stack using Queues

slug:  225. Implement Stack using Queues

date: 2024-05-18
image: 225.png
categories:
    - leetcode
    - Stack
    - Queue
tags:
    - Stack
    - Queue
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/implement-stack-using-queues/description/>

```
Implement Stack using Queues
Category	Difficulty	Likes	Dislikes
algorithms	Easy (63.63%)	5965	1199
Tags
stack | design

Companies
bloomberg

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
Notes:

You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.
 

Example 1:

Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
 

Constraints:

1 <= x <= 9
At most 100 calls will be made to push, pop, top, and empty.
All the calls to pop and top are valid.
 

Follow-up: Can you implement the stack using only one queue?
```


```
 /*
 * 思路：2个队列实现栈，一个栈push时模拟stack的存储顺序，另一一个队列完全当作备份用
 *
 *
 *
 *    ***/
```


```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {
    Queue<Integer> queue;
    Queue<Integer> queueBackup;

    public MyStack() {
        queue = new LinkedList<>();
        queueBackup = new LinkedList<>();   
    }
    
    //加入元素时，即用queue模拟栈stack的存储顺序，将 queue依次压入queueBackup，
    //再将queueBackup的元素依次压入queue，这样保证x位于queue的第一个位置，即类似栈顶
    public void push(int x) {
        while (queue.size()>0) {
            queueBackup.add(queue.poll());
        } 
        queue.add(x);
        while (queueBackup.size()>0) {
            queue.add(queueBackup.poll());
        }
    }
    
    public int pop() {
        return queue.poll();
    }
    public int top() {
        return  queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}
```