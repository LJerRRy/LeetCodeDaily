## 647. Palindromic Substrings
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
Example 2:
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
Note:
The input string length won't exceed 1000.
## Summary

## Solution

### Approach#1
从中间向外进行判断。

```java
public class Solution {
    int count = 0;
    public int countSubstrings(String s) {
        if(s == null || s.length() == 0){
            return 0;
        }
        for(int i = 0; i < s.length(); i++){
            helper2(s, i, i);
            helper2(s, i , i + 1);
        }
        return count;
    }
    public void helper2(String s, int i, int j){
        while(i >= 0 && j < s.length()){
            if(s.charAt(i) != s.charAt(j)){
                return;
            }
            count++;
            i--;
            j++;
        }
    }
}
```
