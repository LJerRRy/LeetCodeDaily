## 643. Maximum Average Subarray I
Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.
**Example 1:**
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
Note:
1 <= k <= n <= 30,000.
Elements of the given array will be in the range [-10,000, 10,000].
## Summary
求给定数组和一个k值，求连续k个数的平均数最大值
## Solution

### Approach#1
先求数组和
- 时间复杂度：O(n)
- 空间复杂度：O(n)

```java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int len = nums.length;
        double[] sum = new double[len];
        sum[0] = nums[0];
        for(int i = 1;i<len;i++){
            sum[i]=sum[i-1]+nums[i];
        }
        double res = sum[k-1];
        for(int i = 0;i<len-k;i++){
            res = Math.max(res, sum[i+k]-sum[i]);
        }
        return res / k;
    }
}
```
### Approach#2
移动窗口，窗口大小为k
- 时间复杂度：O(n)
- 空间复杂度：O(1)

```java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        long s = 0;
        long max = Long.MIN_VALUE;
        for(int i = 0;i < nums.length;i++){
            s += nums[i];
            if(i >= k-1){
                max = Math.max(max, s);
                s -= nums[i-(k-1)];
            }
        }
        return (double)max / k;
    }
}
```