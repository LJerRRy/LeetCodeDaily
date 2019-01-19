## 611. Valid Triangle Number
Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.
## Summary

## Solution

### Approach#1
比赛的时候记得我这样做是TLE，可现在居然AC了
- 时间复杂度：O(n^3)
- 空间复杂度：O(1)

```java
public class Solution {
    public int triangleNumber(int[] nums) {
        if(nums==null||nums.length<3)return 0;
        int res = 0, n = nums.length,cur = 0;;
        Arrays.sort(nums);
        for(int i = 0;i<n-2;i++){
            for(int j = i+1;j<n-1;j++){
                for(int k = j+1;k<n;k++){
                    if(nums[i]+nums[j]>nums[k])cur++;
                    else{
                        break;
                    }
                }
            }
        }
        return cur;
    }
}
```
### Approach#2
the idea copy from discuss!
- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

```java
public class Solution {
    public int triangleNumber(int[] nums) {
        if(nums==null||nums.length<3)return 0;
        int res = 0, n = nums.length,cur = 0;;
        Arrays.sort(nums);
        for(int i = 0;i<n-2;i++){
            for(int j = i+1;j<n-1;j++){
                for(int k = j+1;k<n;k++){
                    if(nums[i]+nums[j]>nums[k])cur++;
                    else{
                        break;
                    }
                }
            }
        }
        return cur;
    }
}
```