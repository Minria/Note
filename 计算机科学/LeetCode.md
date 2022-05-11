# 哈希表

**1. 两数之和**

思路：

1. 建立key-value表，key存数组值，value存下标；
2. 进行遍历数组，查看哈希表是否存在target-num值
3. 如果存在，找到就返回结果;没有找到，将当前信息加入哈希表中，执行步骤2

# 链表

**2. 两数相加**

思路：

- 两个链表的数都是逆序的，可以通过末位运算以及进位进行尾插法建立链表
- 注意，在两个链表都加完后仍产生进位，这个也需要考虑

**19. 删除链表的倒数第 N 个结点**

思路：

- 先给链表添加一个头节点便于运算操作
  - 双指针，快指针指向head，慢指针指向头节点（why？），让快指针先走n步
- 让两个指针同时走，直到快指针走到null处
- 慢指针**指向要删除节点的前一个节点**（reason）

**21. 合并两个有序链表**

思路：

- 新链表方便操作添加一个头节点
- 对两个链表进行归并排序，知道其中一个链表为空的时候
- 将另一个不为空的链表接到后面

**23. 合并K个升序链表**

方法1：

采用21题思路，进行两两合并

时间复杂度O(k^2^n)

空间复杂度O(1)

方法2：

采用优先级队列，将所有的节点都加入一个优先级队列，然后出队组成链表

时间复杂度O(kn×log k)

空间复杂度O(kn)

方法3：

采用归并排序思想

**24. 两两交换链表中的节点**

![Snipaste_2022-05-11_22-37-21](../picture/leetcode/Snipaste_2022-05-11_22-37-21.png)

为了方便操作，首先给链表加上一个头节点

我们将链表截断，三部分，已经完成交换的，正要交换的，将要交换的

最开始是，添加的节点就是已经交换，1，2就是正要交换，3，4是将要交换

需要注意的是，如果没有两个节点就终止交换

**25. K 个一组翻转链表**

这个题是上一个题的进一步拓展

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if(head==null) return null;
        ListNode dummy = new ListNode();
        dummy.next = head;
        ListNode p1=dummy;
        while(true){
            // p1代表已经反转好的最后一个节点
            // p2是正在反转的第一节点
            // p3是正在反转的最后节点
            ListNode p2=p1.next;
            ListNode p3=p2;
            int tmp=k;
            while(tmp>1&&p3!=null){
                p3=p3.next;
                tmp--;
            }
            // 表明正在反转的节点数不足k个
            if(p3==null){
                break;
            }
            // p4是将要反转的节点
            ListNode p4=p3.next;
            p1.next=null;
            p3.next=null;
            // 反转
            p1.next=reverse(p2);
            //更新
            p2.next=p4;
            p1=p2;
        }
        return dummy.next;
    }
    // 反转链表
    private ListNode reverse(ListNode head){
        if(head==null){
            return null;
        }
        ListNode pre=null;
        ListNode cur=head;
        while(cur!=null){
            ListNode curNext = cur.next;
            cur.next=pre;
            pre=cur;
            cur=curNext;
        }
        return pre;
    }
}
```

