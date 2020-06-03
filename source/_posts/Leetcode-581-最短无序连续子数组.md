---
title: Leetcode-581-最短无序连续子数组
date: 2020-05-04 00:58:14
categories: Algorithm
tags: Leetcode

---

## 581. 最短无序连续子数组

**题目：**

```
给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。
```

**示例：**

```
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```

**说明：**

```
说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。
```

思路：

思路1：根据题意和示例，第一想法就是复制一个数组，将一个数组排序，然后对比两个数组的元素，记录第一个和最后一个不一样的元素位置，然后用最后一个元素位置`-`第一个元素位置`+`1就可以得到答案。

```java
class Solution {
    public int findUnsortedSubarray(int[] nums) {
       if (nums == null || nums.length <= 1) {
            return 0;
        }
				//拷贝一份数组，进行排序
        int[] nums1 = Arrays.copyOf(nums, nums.length);
        Arrays.sort(nums1);
      	//第一个不同元素的位置
        int left = 0;
      	//最后一个不同元素的位置
        int right = 0;
      	//用来确定第一个不同元素的位置
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] - nums1[i] != 0) {
                count = count + 1;
                if (count == 1) {
                    left = i;
                }
                right = i;
            }
        }
        return count == 0?0:right-left+1;
    }
}
```

