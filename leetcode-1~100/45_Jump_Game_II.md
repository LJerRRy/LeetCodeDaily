## 45 Jump Game II
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = [2,3,1,1,4]

The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

Note:
You can assume that you can always reach the last index.

### Solution 1(TLE)
- Time Complexity: O(n^2)
- Space Complexity: O(1)

```java
public class Solution {
    public int jump(int[] nums) {
        if (nums==null||nums.length<2)return 0;
        int[] dp = new int[nums.length];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for (int i = 1; i < nums.length; i++) {
            int j = i-1;
            while(j>=0){
                if(nums[j]+j>=i) {
                    dp[i] = Math.min(dp[i], dp[j] + 1);
                }
                j--;
            }
        }
        return dp[nums.length-1];
    }
}
```

### Solution 2(AC)
层次的概念。

```java
public class Solution {
    public int jump(int[] nums) {
        if(nums==null||nums.length < 2)return 0;
        int lastmax =0, curmax = 0, res = 0;
        for(int i = 0;i < nums.length;i++){
            curmax = Math.max(curmax, nums[i] + i);
            if(i==lastmax){
                res++;
                lastmax = curmax;
                // 不需要讲curmax设为0，因为下一次迭代的值一定大于当前的curmax
                // curmax = 0;
            }
        }
        return res;
    }
}
```