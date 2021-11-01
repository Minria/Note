

# 链表

## 206.反转链表

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

# 动态规划

## 509. 斐波那契数

**斐波那契数**，通常用 `F(n)` 表示，形成的序列称为 **斐波那契数列** 。该数列由 `0` 和 `1` 开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给你 `n` ，请计算 `F(n)` 。

```
输入：2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

```
输入：3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

```
输入：4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

提升

- `0 <= n <= 30`

建立一个数组`dp[n]`

意义：`dp[i]`代表`F(i)`的值

转移方程：无条件转移`dp[i]=dp[i-1]+dp[i-2]`

边界条件：`dp[0]=0,dp[1]=1`

## 1480. 一维数组的动态和

给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。请返回 nums 的动态和。

```
输入：nums = [1,2,3,4]
输出：[1,3,6,10]
解释：动态和计算过程为 [1, 1+2, 1+2+3, 1+2+3+4] 。
```

```
输入：nums = [1,1,1,1,1]
输出：[1,2,3,4,5]
解释：动态和计算过程为 [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1] 。
```

```
输入：nums = [3,1,2,10,1]
输出：[3,4,6,16,17]
```

提示

- `1 <= nums.length <= 1000`
- `-10^6 <= nums[i] <= 10^6`

**分析**

看到计算过程我们需要计算出所有的动态和

我们要计算第`i`个元素的动态和那我们需要知道什么？我们需要第`i-1`个动态和，然后加上`nums[i]`的值即可

建立一个`dp[nums.length]`数组

意义:`dp[i]`代表下标为i的动态和

转移方程：无条件条件`dp[i]=dp[i-1]+nums[i]`

边界条件：下标为0时前面没有元素，`dp[0]=nums[0]`

```java
class Solution {
    public int[] runningSum(int[] nums) {
        int[] dp=new int[nums.length];
        dp[0]=nums[0];
        for(int i=1;i<nums.length;++i){
            dp[i]=dp[i-1]+nums[i];
        }
        return dp;
    }
}
```





