# 哈希表

**1. 两数之和**

思路：

1. 建立key-value表，key存数组值，value存下标；
2. 进行遍历数组，查看哈希表是否存在target-num值
3. 如果存在，找到就返回结果;没有找到，将当前信息加入哈希表中，执行步骤2

# 链表

## 1-10

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

**61. 旋转链表**

```
输入：head = [1,2,3,4,5], k = 2
输出：[4,5,1,2,3]
```

```
head = [0,1,2], k = 4
输出：[2,0,1]
```

思路：

将链表从倒数k个位置阶段

不过需要提前知道链表的长度

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head==null) return head;
        int n=0;
        ListNode cur=head;
        // 计算链表长度
        while(cur!=null){
            cur=cur.next;
            n++;
        }
        // 如果旋转整数倍就相当于没有旋转
        if(k%n==0) return head;
        // 如果k过大
        else k=k%n;
        //开始分段并且找到最后一个节点
        cur=head;
        ListNode pre=head;
        while(k>0){
            cur=cur.next;
            k--;
        }
        while(cur.next!=null){
            pre=pre.next;
            cur=cur.next;
        }
        cur.next=head;
        head=pre.next;
        pre.next=null;
        return head;
    }
}
```

**82. 删除排序链表中的重复元素 II**

思路1：

- 步骤1：判断当前节点和后一个节点的值是否相同，这需要保证两个节点都存在
- 步骤2：如果相同，用一个数记录，后面遇到这个数都跳过，相当于删除
- 步骤3：如果不同，将该节点加入新节点，重复步骤1
- 注意1：如果当前节点为空，说明链表遍历完，可以退出
- 注意2：后一个节点为空，这是最后一个节点，可以直接加入。为什么排除和前面重复的情况---直接删除
- 注意3：新链表尾为空

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode cur = head;
        ListNode dum = new ListNode(0);
        ListNode p = dum;
        while(cur!=null){
            if(cur.next==null){
                p.next = cur;
                cur = cur.next;
                p = p.next;
                //为什么这里不用标记尾为空？
            }else{
                if(cur.val==cur.next.val){
                    int num = cur.val;
                    while(cur!=null&&cur.val==num){
                        cur = cur.next;
                    }
                }else{
                    p.next = cur;
                    cur = cur.next;
                    p = p.next;
                    //为什么z
                    p.next = null;
                }
            }
        }
        return dum.next;
    }
}
```



思路2：

- 将链表填一个头节点，一个指针指向头节点，表明该指针以前都是处理好的
- 如果后一个节点后两个节点不为空，且值不相等，加入
- 如果相等，标记值，删除后一个节点

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null||head.next==null) {
            return head;
        }
        ListNode dumb = new ListNode(0, head);
        ListNode cur = dumb;
        while(cur.next!=null&&cur.next.next!=null){
            if(cur.next.val==cur.next.next.val){
                int x=cur.next.val;
                while(cur.next!=null&&cur.next.val==x){
                    cur.next=cur.next.next;
                }
            }else{
                cur=cur.next;
            }
        }
        return dumb.next;
    }
}
```

**83. 删除排序链表中的重复元素**

思路：

- 双指针，如果指向链表1的元素值和链表2的值相同，跳过，不一样，就加入

## 11-20

**86. 分隔链表**

给你一个链表的头节点 head 和一个特定值 x ，请你对链表进行分隔，使得所有 小于 x 的节点都出现在 大于或等于 x 的节点之前。

你应当 保留 两个分区中每个节点的初始相对位置。

思路：

- 先准备两个链表，对原链表进行遍历，如果值大于x加入链表2，反之加入链表1，然后对两个链表进行拼接处理

**92. 反转链表2**

给你单链表的头指针 head 和两个整数 left 和 right ，其中 left <= right 。请你反转从位置 left 到位置 right 的链表节点，返回 反转后的链表 。

思路：

- 可以找到[left,right]的链表，对其整体反转，然后再拼接链表
- 需要找到下标为left-1和right-1的节点，然后把链表分割三部分

```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy=new ListNode();
        dummy.next=head;
        ListNode p;
        ListNode p1=dummy,p2,p3=null;
        for(int i=1;i<left;i++){
            p1=p1.next;
        }
        //p1指向left-1
        //p指向left
        p=p1.next;
        p2=p1.next;
        ListNode pre=null;
        for(int i=left;i<=right;i++){
            p3=p2.next;
            p2.next=pre;
            pre=p2;
            p2=p3;
        }
        p1.next=pre;
        p.next=p2;
        return dummy.next;
    }
}
```

**109.有序链表转换为二叉平衡搜索树**

```java
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
       List<Integer> list=new ArrayList<>();
       ListNode p=head;
       while(p!=null){
           list.add(p.val);
           p=p.next;
       }
       return buildBST(list,0,list.size()-1); 
    }
    private TreeNode buildBST(List<Integer> list,int left,int right){
        if(left>right){
            return null;
        }
        int mid=(left+right)/2;
        TreeNode root=new TreeNode(list.get(mid));
        root.left=buildBST(list,left,mid-1);
        root.right=buildBST(list,mid+1,right);
        return root;
    }
}
```



# 堆

**215. 数组中的第K个最大元素**

思路：

- 小堆就是队首元素最小，大堆就是队头元素最大
- 第k大就是前k最大中最小的，需要建立一个小堆
- 如果当前元素比队首元素大或者堆没有满，就进堆。



**33. 搜索旋转排序数组**

思路1：

- 先二分，判断在那一段，然后继续二分查找
- 将数组一分为二，其中一定有一个是有序的，另一个可能是有序，也能是部分有序。
- 此时有序部分用二分法查找。无序部分再一分为二，其中一个一定有序，另一个可能有序，可能无序。就这样循环.

```java
class Solution {
    public int search(int[] nums, int target) {
        int n = nums.length;
        if (n == 0) {
            return -1;
        }
        if (n == 1) {
            return nums[0] == target ? 0 : -1;
        }
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[0] <= nums[mid]) {
                if (nums[0] <= target && target < nums[mid]) {
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            } else {
                if (nums[mid] < target && target <= nums[n - 1]) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        return -1;
    }
}
```



**34. 在排序数组中查找元素的第一个和最后一个位置**

不存在返回[-1,-1]

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

思路：

- 二分查找之区间查找，不存在就返回[-1,-1]
- 由于采用[)的方式也需要打补丁进行修改，我们采用[]的方式

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int left = leftBound(nums,target);
        int right = rightBound(nums,target);
        return new int[]{left,right};
    }
    private int leftBound(int[] nums,int target){
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = (left + right)>>>1;
            if(nums[mid] == target){
                right = mid - 1;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        if(left >= nums.length || nums[left] != target){
            return -1;
        }
        return left;
    }
    private int rightBound(int[] nums,int target){
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = (left + right)>>>1;
            if(nums[mid] == target){
                left = mid + 1;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        if(right < 0 ||nums[right] != target){
            return -1;
        }  
        return right;
    }
}
```

**35. 搜索插入位置** 

不存在就找到插入的位置

思路：

- 如果不存在就需要找到插入位置，不能仅仅返回-1，这需要区间搜索
- 采用左边界搜索（why?)

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = (left+right)>>>1;
            if(nums[mid]==target){
                return mid;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return left;
    }
}
```

74.搜索二维矩阵

思路：

- 在内存上的排列仍然是“一维递增”的
- 可以通过映射来修改下标来正常访问

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int low = 0, high = m * n - 1;
        while (low <= high) {
            int mid = (high - low) / 2 + low;
            int x = matrix[mid / n][mid % n];
            if (x < target) {
                low = mid + 1;
            } else if (x > target) {
                high = mid - 1;
            } else {
                return true;
            }
        }
        return false;
    }
}
```



**704. 二分查找**

```java

```



# KMP算法

```java
//暴力算法
class Solution {
    public int strStr(String haystack, String needle) {
        int n1=haystack.length();
        int n2=needle.length();
        if(n2==0) return 0;
        for(int i=0;i<=n1-n2;i++){
            if(haystack.charAt(i)==needle.charAt(0)){
                int j=0;
                for(;j<n2;j++){
                    if(haystack.charAt(i+j)!=needle.charAt(j)){
                        break;
                    }
                }
                if(j==n2){
                    return i;
                }
            }
        }
        return -1;
    }
}
```

KMP算法是一种改进的字符串匹配算法，由D.E.Knuth，J.H.Morris和V.R.Pratt提出的，因此人们称它为克努特—莫里斯—普拉特操作（简称KMP算法）。KMP算法的核心是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体实现就是通过一个next()函数实现，函数本身包含了模式串的局部匹配信息。KMP算法的时间复杂度O(m+n) [1] 。

与暴力算法不同的是，匹配失败后

<font color="red">**主串的指针不回退，字串的指针回退到某个位置**</font>

<font color="green">**1、字符串的前缀、后缀和部分匹配值**</font>

前缀：除了最后一个字符外，所有的头部字符串

后缀：除了第一个字符外，所有的尾部字符串

部分匹配值：前缀和后缀的最长相等前后长度

对于`ababa`

'a'的前缀和后缀都为空集，最长相等前后缀长度为0。

'ab'的前缀为{a}，后缀为{b}，最长相等前后缀长度为0。

'ab'的前缀为{a,ab}，后缀为{a, b a }, { a, ab}门{a,ba}={a}，最长相等前后缀长度为1。

'abab'的前缀{a,ab,aba}n后缀{b,ab,bab}={ab}，最长相等前后缀长度为2。

'ababa'的前缀{a,ab,aba,abab},后缀{a,ba,aba,baba}={a,aba}，公共元素有两个，最长相等前后缀长度为3。

匹配值分别为00123

| 下标 | 0    | 1    | 2    | 3    | 4    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 数值 | 0    | 0    | 1    | 2    | 3    |

将数值右移

| 下标 | 0    | 1    | 2    | 3    | 4    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 数值 | -1   | 0    | 0    | 1    | 2    |

引出next数组

<font color="green">**2、next数组的求解**</font>

对于next求解，我们一般假设next[i]=k,然后递推得到next[i+1]

![Snipaste_2022-01-02_19-03-11](D:\汪福明\Desktop\Snipaste_2022-01-02_19-03-11.png)

当i=4是，next[4]的数值是1

这就默认了<font color="purple">**p<sub>0</sub>...p<sub>k-1</sub>=p<sub>i-k</sub>...p<sub>i-1</sub>**</font>

> 可以在后面的i=7，8，9，10进行验证

当p<sub>k</sub>==p<sub>i</sub>时，next[i+1]=k+1;

当p<sub>k</sub>!=p<sub>i</sub>需要回退，我们以i==5求next[6]为例

next[5]==2

p<sub>2</sub>=c, p<sub>5</sub>=a,继续回退，next[2]=0,p<sub>0</sub>=a，这是两者相等

next[6]=k+1=0+1=1;

# 动态规划

动态规划是分治思想的延续，通俗来说就是大事化小，小事化了

在将大问题化为小问题时，保存对这些小问题已经处理好的结果，以供后面使用

1、定义状态

2、转移方程

3、终止条件

# 背包问题

## 01背包问题

题目：有N 件物品和一个容量为V 的背包。放入第i件物品耗费的费用是A[i]，得到的价值是W[i]。求解将哪些物品装入背包可使价值总和最大。

这是基本背包问题，其特点是:<font color="red">**每种物品仅有一件，可以选择放或不放。**</font>

<font color="Magenta">**定义状态**</font>：`dp[i][j]`表示背包容量为j时前i物品所所得最大值

<font color="Magenta">**转移方程**</font>：`dp[i][j]=Math.max(dp[i-1][j],dp[i-1][j-A[i]]+W[i])`

<font color="Magenta">**初始条件**</font>：

1、如果需要**包满**的最大值，`dp[0][0]=0,dp[0][other]=Integer.MIN_VALUE;`

很简单，当没有放东西时，包的价值为0，如果空间大于0，那么就会有**空余空间没有使用**

2、如果只需要最大值`dp[0][all]=0,dp[all][0]=0`

<font color="Magenta">**终止条件**</font>：

```java
for i <- 1 to N
    for j <- 1 to V
```



时间复杂度：O(mn)，空间复杂度：O(mn)

<font color="Magenta">**优化问题**</font>：

二维通常可以优化为以为，我们发现数据都是对**上一行进行变化**

我们就可以直接用一个一维数组来存储数组

需要注意的是，二维转换一维数组后遍历顺序需要改变

`dp[j]=Math.max(dp[j],dp[j-A[i]]+w[i])`

## 完全背包问题

题目：有N 件物品和一个容量为V 的背包。放入第i 件物品耗费的费用是A[i]，得到的价值是W[i]。求解将哪些物品装入背包可使价值总和最大。求解：将哪些物品装入背包，可使这些物品的耗费的费用总和不超过背包容量，且价值总和最大。

这个问题非常类似于01 背包问题，所不同的是每种物品有无限件。

# 快速乘、快速幂

```c
int quickMulti(int A, int B) {
    int ans = 0;
    for ( ; B; B >>= 1) {
        if (B & 1) {
            ans += A;
        }
        A <<= 1;
    }
    return ans;
}
```

```java
public double quickMul(double x, long N) {
    if (N == 0) {
        return 1.0;
    }
    double y = quickMul(x, N / 2);
    return N % 2 == 0 ? y * y : y * y * x;
}
//妙到家了
public double quickMul(double x, long N) {
    double ans = 1.0;
        // 贡献的初始值为 x
    double x_contribute = x;
        // 在对 N 进行二进制拆分的同时计算答案
    while (N > 0) {
        if (N % 2 == 1) {
            // 如果 N 二进制表示的最低位为 1，那么需要计入贡献
            ans *= x_contribute;
        }
        // 将贡献不断地平方
        x_contribute *= x_contribute;
        // 舍弃 N 二进制表示的最低位，这样我们每次只要判断最低位即可
       N /= 2;
    }
    return ans;
}
```

# 贪心算法

贪心算法（又称贪婪算法）是指，在对问题求解时，总是做出在当前看来是最好的选择。也就是说，不从整体

最优上加以考虑，他所做出的是在某种意义上的局部最优解。

贪心选择是指所求问题的整体最优解可以通过一系列局部最优的选择，即贪心选择来达到。这是贪心算法可行

的第一个基本要素。

当一个问题的最优解包含其子问题的最优解时，称此问题具有最优子结构性质。运用贪心策略在每一次转化时
都取得了最优解。问题的最优子结构性质是该问题可用贪心算法求解的关键特征。贪心算法的每一次操作都对
结果产生直接影响。贪心算法对每个子问题的解决方案都做出选择，不能回退。

贪心算法的基本思路是从问题的某一个初始解出发一步一步地进行，根据某个优化测度，每一步都要确保能获

得局部最优解。每一步只考虑一个数据，他的选取应该满足局部优化的条件。若下一个数据和部分最优解连在

一起不再是可行解时，就不把该数据添加到部分解中，直到把所有数据枚举完，或者不能再添加算法停止。

实际上，贪心算法适用的情况很少。一般对一个问题分析是否适用于贪心算法，可以先选择该问题下的几个实

际数据进行分析，就可以做出判断。

# 海量数据处理
