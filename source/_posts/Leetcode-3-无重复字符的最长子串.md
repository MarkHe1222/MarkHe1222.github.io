---
title: Leetcode-3-无重复字符的最长子串
date: 2020-05-04 00:40:41
categories: Algorithm
tags: Leetcode

---

## 3.  无重复字符的最长子串

**题目：**

```
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
```

**示例：**

```
1.
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

2.
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

3.
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**思路：**

如示例3所示，但要求的是子串，而不是子序列，也就是说我们答案中的字符不应该有重复出现的。可以考虑使用字典，将出现过的字符以及字符出现的位置记录下来，同时将两个字符重复出现的位置记录下来，最后记录最大值。

**代码：**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.length() == 0) {
            return 0;
        }
        Map<Character, Integer> dict = new HashMap<>();
        int tmp = -1;
        int res = 0;
        for(int i=0; i< s.length(); i++){
            //如果字符重复出现，拿出第一次出现的位置
            if(dict.containsKey(s.charAt(i))){
                tmp = Math.max(dict.get(s.charAt(i)), tmp);
            }
            //当前重复字符的长度与之前的结果对比，保留最大长度
            res = Math.max(res, i-tmp);
          	//将每个字符以及位置都保存到字典当中
            dict.put(s.charAt(i), i);
        }
        return res;
    
    }
}
```

