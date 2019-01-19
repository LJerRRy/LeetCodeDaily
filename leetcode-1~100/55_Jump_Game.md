## 55. Jump Game
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

## Solution
比45题要简单，如果有第45题的做题经验，这题久相对容易多了。

### Solution1
从前往后判断能跳到的最大距离。

```java
public class Solution {
    public boolean canJump(int[] nums) {
        if(nums==null||nums.length==0)return false;
        int max = 0;
        for (int i = 0; i<=max;i++){
            if(i==nums.length-1)break;
            if(nums[i]+i>max)max = nums[i]+i;
        }
        return max>=nums.length-1;
    }
}
```

### Solution2
从后往前判断最小，判断能否到达1.

```java
public class Solution {
    public boolean canJump(int[] nums) {
     
        int lastPos = nums.length - 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            if (i + nums[i] >= lastPos) {
                lastPos = i;
            }
        }
        return lastPos == 0;
    }
}
```