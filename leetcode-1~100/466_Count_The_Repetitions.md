# 466. Count The Repetitions

Define S = [s,n] as the string S which consists of n connected strings s. For example, ["abc", 3] ="abcabcabc".

On the other hand, we define that string s1 can be obtained from string s2 if we can remove some characters from s2 such that it becomes s1. For example, “abc” can be obtained from “abdbec” based on our definition, but it can not be obtained from “acbbe”.

You are given two non-empty strings s1 and s2 (each at most 100 characters long) and two integers 0 ≤ n1 ≤ 106 and 1 ≤ n2 ≤ 106. Now consider the strings S1 and S2, where S1=[s1,n1] and S2=[s2,n2]. Find the maximum integer M such that [S2,M] can be obtained from S1.

Example:

```json
Input:
s1="acb", n1=4
s2="ab", n2=2

Return:
2
```

## Solution 1 (Java)

1. 根据题意，很简单就能想到，其实只需要计算s1字符串中包含多少个s2字符串即可，例如`s1`字符串中有`n`个`s2`字符串，那么最后答案就为`n * n2 / n2`取整
2. 以上这个思路是错误的的，没有把拼接的字符串算上，比如`s1 = "caabaa" n1 = 2`,`s2 = "baac" n2 = 1`，按照上面的思路计算的结果应该为0，其实可以发现这种情况是属于将s1字符串拼接起来才能组成s2，所以计算的时候把模拟拼接，即计算出字符串`s1*n2`字符串中有多少个s2,记为n，然后算出结果，结果为`n / n2`取整

```java
class Solution {
    public int getMaxRepetitions(String s1, int n1, String s2, int n2) {
        if (s1.length() == 0) return 0;
        int l1 = s1.length(), l2 = s2.length();
        int count = 0;
        for (int i = 0, j = 0; i < l1*n1; i++ ) {
            int h = i;
            if (h>= l1) {
                h = h % l1;
            }
            if (s1.charAt(h) == s2.charAt(j)){
                j++;
                if (j == l2) {
                    count += 1;
                    j = 0;
                }
            }
        }
        if (n1 == 0) return 0;
        return count / n2;
    }
}
```