



### 206.反转链表

```
1->2->3->4->5->null
5->4->3->2->1->null
```

**方法1**

可以考虑采用头插法重新建立一个链表

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head==null||head.next==null){
            return head;
        }
        ListNode newHead=new ListNode(head.val);
        newHead.next=null;
        head=head.next;
        while(head!=null){
            ListNode p1=new ListNode(head.val);
            p1.next=newHead;
            newHead=p1;
            head=head.next;
        }
        return newHead;
    }
}
```



时间复杂度：O(n)

空间复杂度：O(n)

**方法2**

从前往后遍历，每次改变两个结点的顺序，需要注意标记下一个结点，避免丢失

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

时间复杂度：O(n)

空间复杂度：O(1)

