--- 
title: 344. Reverse String
description: 344. Reverse String

slug: 344. Reverse String

date: 2024-05-13
image: 344.png
categories:
    - leetcode
    - String
tags:
    - two-pointers
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/reverse-string/description/>


```
 /**
  * 思路：双指针算法
     本题要求使用原地算法 in-place算法 with O(1) extra memory，不能使用额外内存，所以考虑使用双指针算法，
     left,right指针分别指向数组首尾，
     使用临时变量tmp暂存 s[left]，然后交换首尾元素，
     然后左右指针收缩。

     扩展：本题如果不要求使用in-place算法，可以通过stack先进后出的数据结构实现求解
 */
```


```java
// @lc code=start
class Solution {
    public void reverseString(char[] s) {
        int left = 0; 
        int right = s.length-1;
        while (left < right) {
            char tmp = s[left];
            s[left] = s[right];
            s[right] = tmp;
            left++;
            right--;
        }
    }
}
// @lc code=end

```

