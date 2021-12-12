### 对链表进行插入排序

对链表进行插入排序。

插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。
每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

插入排序算法：

插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
重复直到所有输入数据插入完为止。

```
输入: 4->2->1->3
输出: 1->2->3->4
```

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

------

插入排序我们知道，将数据分为已排序和为未排序两部分，我们要求从小到大排列，将未排序的第一个和已排序最后一个比较大小，如果大于就将这个划分到已排序，否则在前面找到合适位置插入，并将元素后移一位。

对链表的操作可能难理解一些

![Snipaste_2021-11-16_17-10-18](https://gitee.com/wang-fuming/dawning/raw/master/202111161710438.png)

```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode dummyHead = new ListNode(0);
        dummyHead.next = head;
        ListNode lastSorted = head, curr = head.next;
        while (curr != null) {
            if (lastSorted.val <= curr.val) {
                lastSorted = lastSorted.next;
            } else {
                ListNode prev = dummyHead;
                while (prev.next.val <= curr.val) {
                    prev = prev.next;
                }
                lastSorted.next = curr.next;
                curr.next = prev.next;
                prev.next = curr;
            }
            curr = lastSorted.next;
        }
        return dummyHead.next;
    }
}
```



## 摩尔投票法

