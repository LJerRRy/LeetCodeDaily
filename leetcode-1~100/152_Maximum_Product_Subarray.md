## 152. Maximum Product Subarray

### Solution 1
分别记录前一次最大的值和最小值，保存在d和p数组中。

```java
public class Solution {
    public int maxProduct(int[] nums) {
        if (nums==null||nums.length==0)return 0;
        int max = nums[0];
        int[] d = new int[nums.length], p = new int[nums.length]; 
        d[0] = nums[0];
        p[0] = nums[0];
        for(int i = 1;i<nums.length;i++){
            d[i] = Math.max(Math.max(nums[i]*d[i-1],p[i-1]*nums[i]),nums[i]);
            p[i] = Math.min(Math.min(nums[i]*d[i-1],p[i-1]*nums[i]),nums[i]);
            max = Math.max(d[i], max);
        }
        return max;
    }
}
```
### Solution 2
由于dp中只用到前一次迭代的值，所以可以只用保存前一次的计算结果即可。

```java
public class Solution {
    public int maxProduct(int[] nums) {
        if (nums==null||nums.length==0)return 0;
        int max = nums[0], minCur = nums[0], maxCur = nums[0];
        for(int i = 1;i<nums.length;i++){
            // 这里必须用临时变量暂存最大和最小的值，原因在于，maxCur的值已经更新了，再计算minCur的时候已经用的当前的最大值进行计算。
            //maxCur = Math.max(Math.max(nums[i]*maxCur,minCur*nums[i]),nums[i])
            //minCur = Math.min(Math.min(nums[i]*maxCur,minCur*nums[i]),nums[i])
            int a = Math.max(Math.max(nums[i]*maxCur,minCur*nums[i]),nums[i]);
            int b = Math.min(Math.min(nums[i]*maxCur,minCur*nums[i]),nums[i]);
            max = Math.max(a, max);
            maxCur = a;
            minCur = b;
        }
        return max;
    }
}
```