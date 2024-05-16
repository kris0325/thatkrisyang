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

     
     solution2:
      雙指針法
      與344. Reverse String思路一致，
      1.先反轉字符串，這時單詞也被反轉了
      2.再反轉單詞，剪切空格
 *
 * 
 * 
 * 
 * 
 * */
```

```java
// @lc code=start
// import com.google.common.base.Splitter;`
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

// @lc code=end
```

