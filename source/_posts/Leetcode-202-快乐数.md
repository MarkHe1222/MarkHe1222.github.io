---
title: Leetcode-202-快乐数
date: 2020-05-06 01:19:36
categories: Algroithm 
tags: Leetcode

---

## 202. 快乐数

**题目：**

```
编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。如果 可以变为  1，那么这个数就是快乐数。

如果 n 是快乐数就返回 True ；不是，则返回 False 。
```

**示例：**

```
输入：19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

**思路：**

思路1：找了一下关于快乐数定义的资料，不符合快乐数定义的数即为非快乐数，有定义为`不是快乐数的数称为不快乐数（unhappy number），所有不快乐数的数位平方和计算，最後都会进入 4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4 的循环中。`所以会出现类似回文的那种循环重复。典型的思想就是将出现过的数字都保存下来，如果出现重复的数字并且这个数字不为`1`的话，则此数字为非快乐数。

**代码：**

```java
public class HappyNumber_202 {
    public boolean isHappy(int n) {
        Set<Integer> visited = new HashSet<>();
        while (n != 1 && !visited.contains(n)) {
          	// 未出现过的数字放入set中
            visited.add(n);
            n = squareSum(n);
        }
        return n == 1;
    }

    private int squareSum(int num) {
        int squareSum = 0;
      	// 按要求计算平方和
        while (num != 0) {
            squareSum += (num % 10) * (num % 10);
            num /= 10;
        }
        return squareSum;
    }
}
```

思路2: 网上看到一个非常巧妙（因为节省了`Set`,所以执行时间更短）的解法，根据非快乐数和快乐数的定义，可以找出规律：无论是否为快乐数，该数字最终都会进入一个循环。所以可以用快慢指针的思想，进行计算，这样两个数最终都会相遇。

```java
class Solution {
    public boolean isHappy(int n) {
        int fast = n;
        int slow = n;
        do{
          	// 慢指针
            slow = squareSum(slow);
            fast = squareSum(fast);
          	// 执行2次，为快指针
            fast = squareSum(fast);
        } while (slow != fast);
        return fast == 1;
    }

    private int squareSum(int num) {
        int squareSum = 0;
        while (num != 0) {
            squareSum += (num % 10) * (num % 10);
            num /= 10;
        }
        return squareSum;
    }
}
```

