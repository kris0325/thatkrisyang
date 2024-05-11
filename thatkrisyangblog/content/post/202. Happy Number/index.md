--- 

title: 202. Happy Number
description: 202. Happy Number

slug: 202. Happy Number

date: 2024-05-10
image: 202.png
categories:
    - leetcode
tags:
    - hashtable
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/happy-number/description/>

```
Happy Number
Category	Difficulty	Likes	Dislikes
algorithms	Easy (56.07%)	10182	1411
Tags
hash-table | math

Companies
airbnb | twitter | uber

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.
Return true if n is a happy number, and false if not.

 

Example 1:

Input: n = 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
Example 2:

Input: n = 2
Output: false
```

```
 /*
  * 思路：哈希表
         or it loops endlessly in a cycle which does not include 1,
         即表明n is happy时, 無限循環，那麼可以推斷，只要紀錄每次循環的sum，總有sum會發生重複，
         因此可以使用hashset收集每次循環的sum，然後判斷是否存在重複的值
  * 
 */
```

```java

// @lc code=start

import java.util.HashSet;

class Solution {
    public boolean isHappy(int n) {
        HashSet<Integer> sumsSet = new HashSet<>();

        // ishappy n == 1 ,  is not happy, sum會重複即 sumsSet.contains(n)，跳出
        while (n != 1 && !sumsSet.contains(n)) {
            sumsSet.add(n);
            n = getSum(n);
        }
        return n == 1;
    }

    int getSum(int n){
        int sum = 0;
        while (n > 0) {
          //先獲取最左邊低位數值
         int low = n % 10;
         sum += low *low;
         //去掉最左邊低位數值
         n = n / 10;
        }
        return sum;
    }
}
// @lc code=end


```
