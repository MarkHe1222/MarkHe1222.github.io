---
title: Leetcode-21-合并两个有序链表
date: 2020-04-24 00:53:25
categories: Algorithm 
tags: Leetcode

---

## 21. 合并两个有序链表

**题目：**

```
将两个升序链表合并为一个新的升序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。
```

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**思路：**

根据题意，两个待合并的链表本身是有序的，所以我们只要按顺序递归遍历两个链表，依次对比元素的大小，不需要进行完全排序。 

**代码：**

```java
public class MergeTwoLists_21 {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // 递归解释条件
        if(l1 == null) {
            return l2;
        }
        if(l2 == null){
            return l1;
        }
        // 比较两个元素的值，将小的链表的下一个元素继续和当前大的链表的值进行比较排序；
        // 并且依次返回递归小链表的头，最后拼接返回新的链表
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```

