## 264. Ugly Number II
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number, and n does not exceed 1690.

### Solution 1(Time Limit Exceeded)

```java
public class Solution {
    public int nthUglyNumber(int n) {
        if(n<=0)return 0;
        if(n==1)return 1;
        int cnt = 1, i = 2, ret = 0;
        while(true){
            if(cnt == n)break;
            if(isUglyNum(i)){
                cnt++;
                ret = i;
            }
            i++;
        }
        return ret;
    }
    private boolean isUglyNum(int n){
        if(n==1)return true;
        while(n%2==0)n/=2;
        while(n%3==0)n/=3;
        while(n%5==0)n/=5;
        return n==1;
    }
}
```

### Solution 2

```java
public class Solution {
    public int nthUglyNumber(int n) {
        if(n<=0)return 0;
        if(n==1)return 1;
        int[] dp = new int[n];
        dp[0] =  1;
        int t2= 0,t3=0,t5=0;
        for(int i = 1;i<n;i++){
            dp[i] = Math.min(2*dp[t2],Math.min(3*dp[t3],5*dp[t5]));
            if(dp[i]==2*dp[t2])t2++;
            if(dp[i]==3*dp[t3])t3++;
            if(dp[i]==5*dp[t5])t5++;
        }
        return dp[n-1];
    }
}
```