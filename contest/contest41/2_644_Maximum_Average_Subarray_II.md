## 644. Maximum Average Subarray II
Given an array consisting of n integers, find the contiguous subarray whose length is greater than or equal to k that has the maximum average value. And you need to output the maximum average value.

Example 1:
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation:
when length is 5, maximum average value is 10.8,
when length is 6, maximum average value is 9.16667.
Thus return 12.75.
Note:
    1 <= k <= n <= 10,000.
    Elements of the given array will be in range [-10,000, 10,000].
    The answer with the calculation error less than 10-5 will be accepted.
## Summary

## Solution

### Approach#1(TLE)
标准的暴力解法，把大于k到num.length全部查找比较一下
- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```java
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        double low = -10001, high = 10001;
        for(int rep = 0;rep < 100;rep++){
            double h = (low+high)/2;
            if(fun(h, nums, k)){
                low = h;
            }else{
                high = h;
            }
        }
        return low;
    }

    private boolean fun(double h, int[] nums, int k){
        int n = nums.length;
        double[] cum = new double[n+1];
        for(int i = 0;i < n;i++){
            cum[i+1] = cum[i] + nums[i] - h;
        }
        double min = Double.POSITIVE_INFINITY;
        for(int i = k-1;i < n;i++){
            min = Math.min(min, cum[i-(k-1)]);
            if(cum[i+1] - min >= 0)return true;
        }
        return false;
    }
}
```
### Approach#2(Accepted)
二分搜索
- 时间复杂度：O(nlog(10000))
- 空间复杂度：O(n)

```java
public class Solution{
    public double findMaxAverage(int[] nums, int k) {
        double low = -12345, high = 12345;
        for(int rep = 0;rep < 100;rep++){
            double h = (low+high)/2;
            if(ok(h, nums, k)){
                low = h;
            }else{
                high = h;
            }
        }
        return low;
    }

    boolean ok(double h, int[] nums, int k){
        int n = nums.length;
        double[] cum = new double[n+1];
        for(int i = 0;i < n;i++){
            cum[i+1] = cum[i] + nums[i] - h;
        }
        double min = Double.POSITIVE_INFINITY;
        for(int i = k-1;i < n;i++){
            min = Math.min(min, cum[i-(k-1)]);
            if(cum[i+1] - min >= 0)return true;
        }
        return false;
    }
}
```