## 67. Add Binary
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

### Solution1(java.lang.NumberFormatException)
数超过integer最大值了。

```java
public class Solution {
    public String addBinary(String a, String b) {
        int aa = Integer.parseInt(a, 2);
        int bb = Integer.parseInt(b, 2);
        return Integer.toBinaryString(aa+bb)+"";
    }
}
```

### Solution2

```java
public class Solution {
    public String addBinary(String a, String b) {
//        int aa = Integer.parseInt(a, 2);
//        int bb = Integer.parseInt(b, 2);
//        return Integer.toBinaryString(aa+bb)+"";
        if (a==null||a.length()==0)return b;
        if (b==null||b.length()==0)return a;
        int i = a.length()-1, j = b.length()-1;
        StringBuilder sb = new StringBuilder();
        int flag = 0;
        while (i>=0&&j>=0){
            if(a.charAt(i)=='1'&&b.charAt(j)=='1'){
                sb.append(flag);
                flag = 1;
            }else if (a.charAt(i)=='0'&&b.charAt(j)=='0'){
                sb.append(flag);
                flag = 0;
            }else {
                if (flag == 0) {
                    sb.append(1);
                    flag = 0;
                }
                else {
                    sb.append(0);
                    flag = 1;
                }
            }
            i--;j--;
        }
        while (i>=0){
            if (a.charAt(i)=='1'){
                if (flag == 0) {
                    sb.append(1);
                    flag = 0;
                }
                else {
                    sb.append(0);
                    flag = 1;
                } 
            }else {
                sb.append(flag);
                flag = 0;
            }
            i--;
        }
        while (j>=0){
            if (b.charAt(j)=='1'){
                if (flag == 0) {
                    sb.append(1);
                    flag = 0;
                }
                else {
                    sb.append(0);
                    flag = 1;
                }
            }else {
                sb.append(flag);
                flag = 0;
            }
            j--;
        }
        if(flag == 1)sb.append(1);
        return sb.reverse().toString();
    }

}
```
### Solution3

```java
public class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();
        int len1 = a.length() - 1;
        int len2 = b.length() - 1;
        int sum = 0;
        while(len1 >= 0 || len2 >= 0){
            
            if(len1 >= 0){
                sum += a.charAt(len1)-'0';
                len1--;
            }
            if(len2 >= 0){
                sum += b.charAt(len2)-'0';
                len2--;
            }
            sb.append(sum % 2);
            sum /= 2;
        }
        if(sum > 0){
            sb.append(sum);
        }
        return sb.reverse().toString();
    }
}
```