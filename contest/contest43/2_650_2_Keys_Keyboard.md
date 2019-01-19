## 650. 2 Keys Keyboard
Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

Copy All: You can copy all the characters present on the notepad (partial copy is not allowed).
Paste: You can paste the characters which are copied last time.
Given a number n. You have to get exactly n 'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get n 'A'.

Example 1:

```
Input: 3
Output: 3
Explanation:
Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.
```
Note:
1. The n will be in the range [1, 1000].
## Summary

## Solution

### Approach#1
因为只能执行`复制`和`黏贴`操作,所以对于所有质数只能一个个`复制A`因式分解 ，将所有因子相加即可，比如10 = 5*2 只需要七次， 再如 12 = 2*2*3 也是需要7次
- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```java
public class Solution {
    public int minSteps(int n) {
        if(n==1)return 0;
        if(isprime(n))return n;
        int[] t = new int[1000];
        int k = 0;
        for(int i=2;i<=n/2;){
            if(n%i==0){
                t[k++] = i;
                n /= i;
            }else{
                i++;
            }
        }
        if(n!=1)t[k++]=n;
        int cnt = 0;
        for(int i = 0;i<1000;i++){
            cnt+=t[i];
        }
        return cnt;
    }
    private boolean isprime(int n){
        for(int i = 2;i*i<=n;i++){
            if(n%i==0)return false;
        }
        return true;
    }
}
```
### Approach#2
动态规划，
- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```java
public class Solution {
    public int minSteps(int n) {
        int[] dp = new int[n+1];
        for (int i=2; i<=n; i++) {
            dp[i] = Integer.MAX_VALUE;
            for (int j=1; j*2<=i; j++) {
                if (0 == i%j) {
                    dp[i] = Math.min(dp[i], dp[j]+i/j);
                }
            }
        }
        return dp[n];
    }
}
```

### Approach#3
递归

```java
public class Solution {
    public int minSteps(int n) {
        if(n==1) return 0;
        for(int i=2;i*i<=n;i++){
            if(n%i==0) return i+minSteps(n/i);
        }
        return n;
    }
}
```