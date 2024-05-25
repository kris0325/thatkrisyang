--- 
title:  150. Evaluate Reverse Polish Notation
description:  150. Evaluate Reverse Polish Notation

slug:  150. Evaluate Reverse Polish Notation

date: 2024-05-24
image: 150.png
categories:
    - leetcode
    - Stack
tags:
    - Stack
weight: 1       # You can add weight to some posts to override the default sorting (date descending)
---
<https://leetcode.com/problems/evaluate-reverse-polish-notation/description/>

```
Evaluate Reverse Polish Notation
Category	Difficulty	Likes	Dislikes
algorithms	Medium (51.37%)	7556	1069
Tags
stack

Companies
linkedin

You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.
 

Example 1:

Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
Example 2:

Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
Example 3:

Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
 

Constraints:

1 <= tokens.length <= 104
tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

```


```
 /**
  * 思路：栈实现你波兰表达式（后缀表示法）
 */
```

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stackRPN = new Stack<>();
        List<String> operators = Arrays.asList(
            "+","-","*","/");
        for(int i = 0; i< tokens.length; i++){
            if(!operators.contains(tokens[i])){
                stackRPN.push(Integer.valueOf(tokens[i]));
            } else{
                int right= Integer.valueOf(stackRPN.pop()) ;
                int left = Integer.valueOf(stackRPN.pop());
                if("+".equals(tokens[i]))stackRPN.push(left + right);
                if("-".equals(tokens[i]))stackRPN.push(left - right);
                if("*".equals(tokens[i]))stackRPN.push(left * right);
                if("/".equals(tokens[i]))stackRPN.push(left / right);
            }
        }
        return stackRPN.pop();
    }
}
```