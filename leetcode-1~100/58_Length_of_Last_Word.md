## 58. Length of Last Word
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.
## Solution
### Solution1

```java
public class Solution {
    public int lengthOfLastWord(String s) {
        if(s==null||s.length()==0)return 0;
        String[] strs = s.split(" ");
        if(strs == null||strs.length==0)return 0;
        return strs[strs.length-1].length();
    }
}
```

### Solution2

```java
public class Solution {
    public int lengthOfLastWord(String s) {
        s = s.trim();
        if(s==null||s.length()==0)return 0;
        int cnt = 0;
        for(int i = s.length()-1;i>=0;i--){
            if(s.charAt(i)==' '){
                break;
            }
            cnt++;
        }
        return cnt;
    }
}
```