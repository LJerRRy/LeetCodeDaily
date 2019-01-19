## 91. Decode Ways
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.


### Solution 1
用dp即可，状态方程
- i-1 == '0' 分两种情况，一种是不符合解码情况
- i-2 == '1' || i-2=='2'&&i-1<'7' 这在i-1不等于'0'的条件下。

```java
public class Solution {
    public int numDecodings(String s) {
        if(s==null||s.length()==0|| s.charAt(0)=='0')return 0;
        int[] dp = new int[s.length()+1];
        dp[0] = 1;
        dp[1]=1;
        for (int i = 2; i < s.length() + 1; i++) {
            if(s.charAt(i-1)=='0'){
                if(s.charAt(i-2)!='1'&&s.charAt(i-2)!='2'){
                    return 0;
                }else {
                    dp[i] = dp[i-2];
                }
            }else if (s.charAt(i - 2)=='1'||s.charAt(i-2)=='2'&&s.charAt(i-1)<'7') {
                dp[i] = dp[i - 2] + dp[i - 1];
            } else{
                dp[i] = dp[i - 1];
            }
        }
        return dp[s.length()];
    }
}
```

### Solution 2
discuss 上的方法，其实就是dp的思路

```java
int numDecodings(string s) {
    if (!s.size() || s.front() == '0') return 0;
    // r2: decode ways of s[i-2] , r1: decode ways of s[i-1] 
    int r1 = 1, r2 = 1;
    
    for (int i = 1; i < s.size(); i++) {
        // zero voids ways of the last because zero cannot be used separately
        if (s[i] == '0') r1 = 0;

        // possible two-digit letter, so new r1 is sum of both while new r2 is the old r1
        if (s[i - 1] == '1' || s[i - 1] == '2' && s[i] <= '6') {
            r1 = r2 + r1;
            r2 = r1 - r2;
        }

        // one-digit letter, no new way added
        else {
            r2 = r1;
        }
    }

    return r1;
}
```