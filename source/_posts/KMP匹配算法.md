---
title: KMP匹配算法
date: 2020-06-14 21:04:06
categories: Algorithm
tags: Java
---

好几次遇到关于KMP匹配算法的使用，但是每次看到以后都忘了，所以这里做个记录。

在B站看到三哥的2个视频，算是讲KMP最简单通俗的视频了：

1. [KMP算法原理和流程](https://www.bilibili.com/video/BV1kJ411u7pt)
2. [如何创建next数组(前缀)](https://www.bilibili.com/video/BV1iJ411u74L?t=350)

上代码：

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (haystack == null || needle == null || haystack.length() < needle.length()) {
            return -1;
        }

        if ((haystack.length() == 0 && needle.length() == 0) || (haystack.length() > 0 && needle.length() == 0)) {
            return 0;
        }
        
        // KMP的核心，先创建next数组
        int[] next = genNext(needle);

        for (int i = 0, j = 0; i < haystack.length(); i++) {
            while (j > 0 && haystack.charAt(i) != needle.charAt(j)) {
                j = next[j - 1];
            }

            if (haystack.charAt(i) == needle.charAt(j)) {
                j++;
            }

            if (j == needle.length()) {
                return i - (j - 1);
            }
        }
        return -1;
    }
    
    private int[] genNext(String needle) {
        int[] next = new int[needle.length()];
        if (needle.length() == 0) {
            return next;
        }
        next[0] = 0;

        for (int i = 1, j = 0; i < needle.length(); i++) {
            while (j > 0 && needle.charAt(i) != needle.charAt(j)) {
                j = next[j - 1];
            }

            if(needle.charAt(i) == needle.charAt(j)) {
                j++;
            }
            next[i] = j;
        }
        return next;
    }
}
```

