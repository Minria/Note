# 基础数据结构

## 链表

### 147. 对链表进行插入排序

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

## 算法

## 动态规划

### 509. 斐波那契数

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

提示

- `0 <= n <= 30`

建立一个数组`dp[n]`

意义：`dp[i]`代表`F(i)`的值

转移方程：无条件转移`dp[i]=dp[i-1]+dp[i-2]`

边界条件：`dp[0]=0,dp[1]=1`

```java
class Solution {
    public int fib(int n) {
        if(n==0) return 0;
        int[] dp=new int[n+1];
        dp[0]=0;
        dp[1]=1;
        for(int i=2;i<n+1;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
}
```

------

**优化问题**

动态规划很难在时间上进行优化，很多都是在空间上进行优化

上述解法时间复杂度O(n);空间复杂度O(n)。

那要怎么才能优化呢？

我们发现我们计算`dp[i]=dp[i-1]+dp[i-2]`只用到三个数据，并且我们在最后输出一个数据，我们就可以从这里开始优化

```java
class Solution {
    public int fib(int n) {
        if(n<=1){
            return n;
        }
        int p=0,q=0,r=1;
        for(int i=2;i<=n;i++){
            p=q;
            q=r;
            r=q+p;
        }
        return r;
    }
}
```

时间复杂度O(n);空间复杂度O(1)。

### 1480. 一维数组的动态和

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

由于dp数组每个元素需要故不能在空间上进行优化。

### 1137. 第 N 个泰波那契数

泰波那契序列 Tn 定义如下： 

T<sub>0</sub> = 0, T<sub>1</sub> = 1, T<sub>2</sub> = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

给你整数 n，请返回第 n 个泰波那契数 Tn 的值。

```
输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```

```
输入：n = 25
输出：1389537
```

**提示：**

- `0 <= n <= 37`
- 答案保证是一个 32 位整数，即 `answer <= 2^31 - 1`。

建立`dp[n+1]`数组

意义：`dp[i]`代表第i个的值

转移方程：`dp[i]=dp[i-1]+dp[i-2]+dp[i-3]`

边界条件：`dp[0]=0,dp[1]=1,dp[2]=1`









