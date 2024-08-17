---
title: sliding window
description: 滑動窗口
slug: sliding window
date: 2024-08-12
image: slidingwindow.png
categories:
    - leetcode
tags:
    - sliding window
    
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---

# 什麼是滑動窗口 Sliding Window？
滑動窗口算法，可以用於解決數組，字符串等子元素問題，它可以將嵌套的循環問題轉化為單循環問題，降低時間複雜度。

# 如何識別滑動窗口算法題型？
1.連續的元素，例如String， Subarray，LinkedList
2.min, max, longest,shortest, keyword

**注意：和回溯算法問題區分，回溯問題一般是求有多少種組合，排列，
而滑動窗口是最大，最小，最長**

# 算法模板
```java
//滑動窗口模板（進，出，算）
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    //map表示當前滑動窗口
    Map<Character, Integer> map = new HashMap<>();
    int left=0, result = 0;
    for (int i =0; i<s.length();i++){
        char rightChar = s.charAt(i);
        //1.進：當前遍歷的i（右邊界）進入窗口
        map.put(rightChar, map.getOrDefault(rightChar,0)+1);
        //2.出：當前窗口不符合條件時left（左邊界）持續推出窗口
        while (map.keySet().size()){
            char leftChar = s.charAt(left);
            map.put(leftChar,map.get(leftChar)-1);
            if(map.get(leftChar)==0){
                map.remove(leftChar);
            }
            //左邊界持續右移
            left++;
        }
        //3.算：滿足條件時，計算valid窗口的結果
        result = Math.max(result, i-left);
    }
    return result;
} 
```

# leetcode題單
```
3.Longest Substring Without Repeating Characters
159. Longest Substring with At Most Two Distinct Characters
340.Longest Substring with At Most K Distinct Characters
395.Longest Substring With At Least K Repeating Characters
424.Longest Repeating Character Replacement
209.Minimum Size Subarray Sum
76.Minimum Window Substring
992.SubarraysWithKDifferentIntegers
1248.CountNumberOfNiceSubarrays

```
[sliding window 滑動窗口](https://docs.google.com/spreadsheets/d/1TovJdSfOYzjvczAjuC1BEtsYRzosvfC3iY6gQN_4Tyc/edit?usp=sharing)