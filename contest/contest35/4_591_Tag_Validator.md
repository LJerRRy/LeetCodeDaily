## 591. Tag Validator
题目太长了，大意就是给定字符串进行xml解析，判断是否是符合条件的xml
## Summary

## Solution

### Approach#1
用栈来解题，解题关键在于：
1. `<!, </`开始的时，栈中必须有值，理由在于`<![CDATA`必须要在Tag里面，即栈中必须有值
2. Tag标签长度必须1~9，而且必须是大写字母
3. 必须有个外部标签，如果没有则不符合条件，如`<A></A><B></B>`虽然满足其他条件但是它仍然不符合条件。

- 时间复杂度：O(n) n为字符串长度
- 空间复杂度：O(n) 栈的深度最糟糕（最多）为n/3,比如`<A><B><C><D>`，栈深=12/3 = 4;

```java
public class Solution {
    public boolean isValid(String code) {
        if (code == null||code.length()==0||code.charAt(0)!='<') {
            return false;
        }
        Stack<String> s = new Stack<>();
        int i = 0;
        boolean res = false;
        while (i<code.length()){
            if(code.charAt(i)=='<'&&i<code.length()-1&&code.charAt(i+1)=='!'){
                if(s.isEmpty()){
                    break;
                }
                i++;
                int t = code.indexOf("[CDATA[",i);
                if(t==-1) {
                    break;
                }
                t = code.indexOf("]]>", t);
                if(t==-1) {
                    break;
                }
                i = t+3;
            }else if(code.charAt(i)=='<'&&i<code.length()-1&&code.charAt(i+1)=='/'){
                if(s.isEmpty()){
                    break;
                }
                int t = code.indexOf(">",i+1);
                if(t==-1) {
                    break;
                }
                if(!s.pop().equals(code.substring(i+2,t))){
                    break;
                }
                i = t+1;
                if(s.isEmpty())break;
            }else if(code.charAt(i)=='<'&&i<code.length()-6){
                i++;
                int t = code.indexOf(">", i+1);
                String tmp = code.substring(i,t);
                if(!isVailidTag(tmp)){
                    break;
                }
                s.push(tmp);
                i = t+1;
            }else if(code.charAt(i)=='<') {
                break;
            }else {
                while (i<code.length()&&code.charAt(i)!='<')i++;
            }
        }
        if(i>=code.length()&&s.isEmpty())res = true;
        return res;
    }

    private boolean isVailidTag(String s){
        if(s==null||s.length()>9||s.length()<1)return false;
        for(char c:s.toCharArray()){
            if(c>='A'&&c<='Z')continue;
            return false;
        }
        return true;
    }
}
```
### Approach#2
用正则表达式，具体解释可以看参考资料中链接。
- 时间复杂度：未知，因为是用的正则表达式
- 空间复杂度：O(n)

```java
import java.util.regex.*;
public class Solution {
    Stack < String > stack = new Stack < > ();
    boolean contains_tag = false;
    public boolean isValidTagName(String s, boolean ending) {
        if (ending) {
            if (!stack.isEmpty() && stack.peek().equals(s))
                stack.pop();
            else
                return false;
        } else {
            contains_tag = true;
            stack.push(s);
        }
        return true;
    }
    public boolean isValid(String code) {
        String regex = "<[A-Z]{0,9}>([^<]*(<((\\/?[A-Z]{1,9}>)|(!\\[CDATA\\[(.*?)]]>)))?)*";
        if (!Pattern.matches(regex, code))
            return false;
        for (int i = 0; i < code.length(); i++) {
            boolean ending = false;
            if (stack.isEmpty() && contains_tag)
                return false;
            if (code.charAt(i) == '<') {
                if (code.charAt(i + 1) == '!') {
                    i = code.indexOf("]]>", i + 1);
                    continue;
                }
                if (code.charAt(i + 1) == '/') {
                    i++;
                    ending = true;
                }
                int closeindex = code.indexOf('>', i + 1);
                if (closeindex < 0 || !isValidTagName(code.substring(i + 1, closeindex), ending))
                    return false;
                i = closeindex;
            }
        }
        return stack.isEmpty();
    }
}
```


## 参考资料
1. [591. Tag Validator](https://leetcode.com/articles/tag-validator/)