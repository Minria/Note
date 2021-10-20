



## 1. 两数之和

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i,j,k=0;
        int[] answer={-1,-1};
        for(i=0;i<nums.length-1;++i){
            for(j=i+1;j<nums.length;++j){
                if(nums[i]+nums[j]==target){
                    answer[0]=i;
                    answer[1]=j;
                    k=1;
                    break;
                }
            }
            if(k==1){
                break;
            }
        }
        return answer;
    }
}
```

![Snipaste_2021-10-17_18-32-21](https://gitee.com/wang-fuming/dawning/raw/master/202110171832541.png)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashtable = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; ++i) {
            if (hashtable.containsKey(target - nums[i])) {
                return new int[]{hashtable.get(target - nums[i]), i};
            }
            hashtable.put(nums[i], i);
        }
        return new int[0];
    }
}
```

![Snipaste_2021-10-17_18-36-52](https://gitee.com/wang-fuming/dawning/raw/master/202110171837736.png)

## 33. 搜索旋转排序数组

```java
class Solution {
    public int search(int[] nums, int target) {
        for(int i=0;i<nums.length;i++){
            if(nums[i]==target){
                return i;
            }
        }
        return -1;
    }
}
```

