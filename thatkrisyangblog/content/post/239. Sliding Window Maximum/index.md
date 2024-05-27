--- 
title:  239. Sliding Window Maximum
description:  239. Sliding Window Maximum

slug:  239. Sliding Window Maximum

date: 2024-05-26
image: 239.png
categories:
    - leetcode
    - Stack
    - Queue
tags:
    - Stack
    - Queue
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/sliding-window-maximum/description/>

```
Sliding Window Maximum
Category	Difficulty	Likes	Dislikes
algorithms	Hard (46.57%)	17988	666
Tags
heap | sliding-window

Companies
amazon | google | zenefits

You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Example 2:

Input: nums = [1], k = 1
Output: [1]
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length
```
```
/**
  * 思路：队列实现
         1.用一个单调递增队列维护滑动窗口，队列最前面一个元素即为当前窗口的最大值，收集到数组；
         2.每次移动窗口，则添加当前元素入队列，那么队列最前面一个元素即为当前最大值，收集到数组；
         3.直到移动到目标数组的末尾，return收集最大值的数组
  **/
```

```java
class MyQueue{
    Deque<Integer> myDeque = new LinkedList<>();

    //将当前值推入队列（队尾），并移除所有比当前值小的元素
    public void push (int value){
        while(!myDeque.isEmpty() && value > myDeque.getLast()){
            myDeque.removeLast();
        }
        /* 错误入队列，这个方法是stack实现的队列，相当于将当前值推入队列（队首）了
           myDeque.push(value);
        **/
        myDeque.addLast(value);
    }

    //如果队列首部元素等于给定值，则移除它
    public void pop(int value){
        if(!myDeque.isEmpty() && myDeque.peekFirst() == value){
            myDeque.removeFirst();
        }
    }

    //返回队列首部元素，即当前窗口的最大值
    public Integer peek(){
        return myDeque.peekFirst();
    }

}


class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        MyQueue myDeque = new MyQueue();
        int[] result = new int[nums.length-k+1];
        int num = 0;
        
        //初始化第一个滑动窗口
        for(int i = 0; i< k; i++){
            //初始化滑动窗口入队列，并且构建的是单调队列，队列并不需要维护所有滑动窗口内的元素，
            //只需维护可能为最大值的元素，即保证队列从队尾到对首是单调递增即可
            myDeque.push(nums[i]);
        }

        result[num++] = myDeque.peek();
        
        // 处理滑动窗口
        for(int i= k; i < nums.length;i++){
            myDeque.pop(nums[i-k]);
            myDeque.push(nums[i]);
            result[num++] = myDeque.peek();
        }
        return result;
    }
}


// @lc code=end


```