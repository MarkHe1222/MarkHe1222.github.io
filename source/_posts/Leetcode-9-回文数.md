---
title: Leetcode-9-回文数
date: 2020-04-27 00:59:00
categories: Algorithm
tags: Leetcode

---

## 9. 回文数

**题目：**

```
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
```

**示例：**

```
1.
输入: 121
输出: true

2.
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

3.
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。

Ps:
进阶: 你能不将整数转为字符串来解决这个问题吗？
```

**思路：**

题意限制是`int`类型， 所以极大降低了难度，只要将正整数反转就可以得到想要的结果，关于数字反转，正如[7-整数反转]([https://markhe1222.github.io/2020/04/26/Leetcode-7-%E6%95%B4%E6%95%B0%E5%8F%8D%E8%BD%AC/](https://markhe1222.github.io/2020/04/26/Leetcode-7-整数反转/))当中描述的数学方法。

**代码：**

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x<0){
            return false;
        }
        int tmp = x;
        int n = 0;
        while(tmp != 0){
            n = n *10 + tmp %10;
            tmp = tmp /10;
        }
        return n == x;
    
    }
}
```

