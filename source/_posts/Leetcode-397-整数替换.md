---
title: Leetcode--397.整数替换
date: 2020-04-17 00:15:22
categories: Algorithm
tags: Leetcode
---

## 397. 整数替换

**题目：**

```
给定一个正整数 n，你可以做如下操作：
1. 如果 n 是偶数，则用 n / 2替换 n。
2. 如果 n 是奇数，则可以用 n + 1或n - 1替换 n。
n 变为 1 所需的最小替换次数是多少？
```

**示例：**

  ```
1. 输入： 8
   输出： 3
   解释： 8 -> 4 -> 2 -> 1
   
2. 输入： 7
   输出： 4
   解释：7 -> 8 -> 4 -> 2 -> 1
        或
        7 -> 6 -> 3 -> 2 -> 1
  ```

**思路：** 

递归思想，假设一个能返回最小步子的函数func(int n)

终止条件为：n=1时，返回0

n为偶数时，返回值为：(遍历次数 + 1) + func(n/2)

n为奇数时，返回值为：(遍历次数 + 1) + [func(n+1) , func(n-1)]的最小值

**代码：**

 ```java
public class IntegerReplacement_397 {
    private int integerReplacement(int n) {
        return (int) func(n);
    }

    private long func(long n) {
        if (n == 1) {
            return 0;
        }
        if (n % 2 == 0) {
            return func(n / 2) + 1;
        } else {
            return Math.min(func(n - 1), func(n + 1)) + 1;
        }
    }

    public static void main(String[] args) {
        IntegerReplacement_397 test = new IntegerReplacement_397();
        int n = 8;
        System.out.println(test.integerReplacement(n));
    }
}
 ```

