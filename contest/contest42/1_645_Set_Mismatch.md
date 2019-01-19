## 645. Set Mismatch
The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

Example 1:
Input: nums = [1,2,2,4]
Output: [2,3]
Note:
1. The given array size will in the range [2, 10000].
2. The given array's numbers won't have any order.
## Summary
## Solution
分别求出重复的值和所缺失的值即可，由于数组大小只有一万，时间复杂度O(n^2)的算法也能AC
### Approach#1

```java
public class Solution {
    public int[] findErrorNums(int[] nums) {
        int sum = 0;
        Arrays.sort(nums);
        int t = 0, m = 0;
        for(int i = 0;i<nums.length;i++){
            if(i!=nums.length-1){
                if(nums[i]==nums[i+1]){
                    t = nums[i];
                }
            }
            sum += nums[i];
        }
        int total = (nums.length+1)*nums.length/2;
        if(total > sum){
            m = total - sum +t;
        }else{
            m = t - sum + total;
        }
        return new int[]{t, m};       
    }
}
```
### Approach#2
HashSet求重复的值

```java
public class Solution {
    public int[] findErrorNums(int[] nums) {
        int n = nums.length;
        int num1 = -1;
        int sum = 0;
        HashSet<Integer> set = new HashSet<>();
        for(int num : nums){
            if(set.contains(num)){
                num1 = num;
        
            }else{
                set.add(num);
            }
            sum += num;
        }
        
        int diff = (1 + n) * n / 2 - sum;
        return new int[]{num1, num1 + diff};
    }
}
```