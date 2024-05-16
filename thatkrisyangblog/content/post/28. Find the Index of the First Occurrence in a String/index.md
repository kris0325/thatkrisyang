--- 
title:  28. Find the Index of the First Occurrence in a String
description:  28. Find the Index of the First Occurrence in a String

slug:  28. Find the Index of the First Occurrence in a String

date: 2024-05-15
image: 28.png
categories:
    - leetcode
    - String
tags:
    - two-pointers
    - sliding window
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

<https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/>


```
Find the Index of the First Occurrence in a String
Category	Difficulty	Likes	Dislikes
algorithms	Easy (42.25%)	5645	390
Tags
two-pointers | string

Companies
apple | facebook | microsoft | pocketgems

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

 

Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
Example 2:

Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
 

Constraints:

1 <= haystack.length, needle.length <= 104
haystack and needle consist of only lowercase English characters.
```

```
 /**
  * 思路：滑動窗口 / 雙指針法，
                   只是左右指針同步移動，haystack.substring(i, i+needle.length())

        1.needle.length > haystack,直接return -1;
        2.從haystack的起始位置i=0開始,取needle.length長度子字符串與needle比較，
          字符串不相同，則滑動needle.length長度繼續比較，直到i到達haystack.length-needle.length位置，
          字符串相同，則return 位置i;
  **/
```

```java
// @lc code=start
class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack.length()<needle.length()){
            return -1;
        }
        for(int i = 0; i <= haystack.length()-needle.length();i++ ){
            if(needle.equals(haystack.substring(i, i+needle.length()))){
                return i;
            }
        }
        return -1;
    }
}
// @lc code=end
```