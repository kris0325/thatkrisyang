--- 
title:  151. Reverse Words in a String
description:  151. Reverse Words in a String

slug:  151. Reverse Words in a String

date: 2024-05-15
image: 151.png
categories:
    - leetcode
    - String
tags:
    - two-pointers
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---


<https://leetcode.com/problems/reverse-words-in-a-string/description/>

> 相同類型：
>344. Reverse String
<https://leetcode.com/problems/reverse-string/description/>

```
Reverse Words in a String
Category	Difficulty	Likes	Dislikes
algorithms	Medium (42.13%)	8216	5116
Tags
string

Companies
apple | bloomberg | microsoft | snapchat | yelp

Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

 

Example 1:

Input: s = "the sky is blue"
Output: "blue is sky the"
Example 2:

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
Example 3:

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
 

Constraints:

1 <= s.length <= 104
s contains English letters (upper-case and lower-case), digits, and spaces ' '.
There is at least one word in s.
 

Follow-up: If the string data type is mutable in your language, can you solve it in-place with O(1) extra space?
```

```
 /*
 * 思路: 
     solution1: 
       stack實現reverse
 *    1，先遍歷字符串數組，剪切掉space，取出word按順序存入stack；
 *    2，stack pop出world，加上space拼接成字符串
 * */
```

```java
// @lc code=start
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;
class Solution {
    public String reverseWords(String s) {
        //通过在分割字符串之前使用trim()去除首尾空格
        //，并使用正则表达式"\\s+"匹配多个空格，可以避免空字符串的问题
        String [] spStrings = s.trim().split("\\s+");
        Stack<String> stackString = new Stack();
        for(int i =0; i< spStrings.length; i++){
            stackString.push(spStrings[i]);
        }
        List<String> list = new ArrayList<>();
        while (!stackString.empty()) {
            list.add(stackString.pop());        
        }
        return String.join(" ", list);
    }
}
```

```
/*
 *   Follow-up: If the string data type is mutable in your language, can you
 * solve it in-place with O(1) extra space?
 * 
 *   思路：雙指針法
 *        與344. Reverse String思路一致，
 *    1.先剪切首尾空格與中間多餘空格
      2.先反轉字符串，這時單詞也被反轉了
      3.再反轉單詞

      注意：處理// 反转最后一个单词
 *
 * 
 * 
 * 
 * 
 * */
```



```java
class Solution {
    public String reverseWords(String s) {
        // 将字符串转换为字符数组
        char[] schar = s.toCharArray();
        // 字符数组的长度
        int length = schar.length;
        // 去除首尾和中间多余的空格
        int slow = 0; // 慢指针，记录新字符串的长度
        int fast = 0; // 快指针，遍历原始字符串
        while (fast < length) {
            // 跳过前导空格
            while (fast < length && schar[fast] == ' ') fast++;
            // 将非空字符移到慢指针位置
            if (slow > 0 && fast < length) {
                schar[slow++] = ' ';
            }
            // 将单词复制到新字符串
            while (fast < length && schar[fast] != ' ') {
                schar[slow++] = schar[fast++];
            }
        }
        
        // 反转整个字符串
        reverseString(schar, 0, slow - 1);
        
        // 反转各个单词
        int start = 0; // 单词起始位置
        for (int i = 0; i < slow; i++) {
            if (schar[i] == ' ') {
                // 反转单词
                reverseString(schar, start, i - 1);
                // 更新单词起始位置
                start = i + 1;
            }
        }
        // 反转最后一个单词
        reverseString(schar, start, slow - 1);
        
        // 将字符数组转换为字符串
        return new String(schar, 0, slow);
    }

    // 反转字符数组的指定区间
    public void reverseString(char[] schar, int start, int end) {
        while (start < end) {
            char tmp = schar[start];
            schar[start] = schar[end];
            schar[end] = tmp;
            start++;
            end--;
        }
    }
}
// @lc code=end
```

 



