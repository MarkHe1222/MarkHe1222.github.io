---
title: Leetcode-20-有效的括号
date: 2020-04-25 00:04:13
categories: Algorithm
tags: Leetcode

---

## 20.有效括号

**题目：**

```
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：
	1.左括号必须用相同类型的右括号闭合。
  2.左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。
```

**示例：**

```
1.
输入: "()"
输出: true
2.
输入: "()[]{}"
输出: true
3.
输入: "(]"
输出: false
4.
输入: "([)]"
输出: false
5.
输入: "{[]}"
输出: true
```

**思路：**

思路1: 根据括号的属性，需要成对匹配，并且可以嵌套使用。由此可以联想到栈的特点，先进后出。 更具括号的前半边，可以让预期的后半边的括号入栈，最后对比栈内的元素，如果符合要求就出栈，最终栈为空的话，符合条件。

**代码：**

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        for(Character c: s.toCharArray()) {
            // 根据括号前半边，让预期的后半边括号入栈
            if(c == '('){
                stack.push(')');
            } else if (c == '[') {
                stack.push(']');
            } else if (c == '{') {
                stack.push('}');
            } else if (stack.isEmpty() || !c.equals(stack.pop())) { // 对比预期的后半边括号，符合条件出栈
                return false;
            }
        }
        return stack.isEmpty();
    }
}
```

思路2: 后面看到另外一种方法，角度特别新奇。可能运行时间比较长，但是也是很有意义。因为符合条件的括号，无论如何都会有一对是在一起的，如果我们和玩连连看的游戏那样，将最先符合条件的那对括号先抵消，那么如此遍历抵消下去，最终字符串为空的话，则符合条件。

**代码：**

```java
class Solution {
    public boolean isValid(String s) {
        while (s.contains("()") || s.contains("{}") || s.contains("[]")) {
            s = s.replace("()", "");
            s = s.replace("{}", "");
            s = s.replace("[]", "");
        }
        return "".equals(s);
    }
}
```

