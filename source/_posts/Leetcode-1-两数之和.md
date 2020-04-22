---
title: Leetcode-1-两数之和
date: 2020-04-21 22:06:33
categories: Algorithm
tags: Leetcode

---

## 1. 两数之和

**题目： **

```
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
```

**示例：**

```给定 nums = [2, 7, 11, 15], target = 9
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

**思路：**

思路1:

比较传统的思路，按顺序多次遍历数组进行查询，看是数组中是否有符合条件的答案。但是两个for循环的嵌套大大地提高了算法的时间复杂度。

**代码：**

```java
public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];
        for (int i=0; i < nums.length; i++) {
            int j = target - nums[i];
            for (int x = i+1; x < nums.length; x++) {
                if (j == nums[x]) {
                    res[0] = i;
                    res[1] = x;
                    return res;
                }
            }
        }
        return res;
    }
}
```

思路2:

为了减少思路1当中的for循环嵌套，可以考虑是否利用一个map来记录数组值和对应的位置索引？ 考虑到每次循环记录的是我们已有元素的遍历，根据题意，我们可以在map当中记录每个元素对应补数的值，这样遍历下一个数组元素时，就可以判断满足条件的值是否在map当中存在。可以大大降低算法的时间复杂度。

**代码：**

```java
import java.util.HashMap;

public class TwoSum {
    public int[] twoSum(int[] nums, int target) {
        int[] res = new int[2];

        HashMap<Integer, Integer> kv = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (kv.containsKey(nums[i])) {
                res[0] = i;
                res[1] = kv.get(nums[i]);
            }
            // 将遍历过的数组元素的补数和下标事先保存
          	// 以便下次遍历的时候可以判断当前补数是否存在
            kv.put(target - nums[i], i);
        }
        return res;
    }
}
```

