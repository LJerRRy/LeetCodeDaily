## 600. Non-negative Integers without Consecutive Ones
Given a positive integer n, find the number of non-negative integers less than or equal to n, whose binary representations do NOT contain consecutive ones.

```
Input: 5
Output: 5
Explanation: 
Here are the non-negative integers <= 5 with their corresponding binary representations:
0 : 0
1 : 1
2 : 10
3 : 11
4 : 100
5 : 101
Among them, only integer 3 disobeys the rule (two consecutive ones) and the other 5 satisfy the rule. 
```

## Summary

## Solution

### Approach#1 Brute Force [Time Limit Exceeded]
超时。
- 时间复杂度：O(32*n)
- 空间复杂度：O(1)

```java
public class Solution {
    public int findIntegers(int num) {
        int count = 0;
        for (int i = 0; i <= num; i++)
            if (check(i))
                count++;
        return count;
    }
    public boolean check(int n) {
        int i = 31;
        while (i > 0) {
            if ((n & (1 << i)) != 0 && (n & (1 << (i - 1))) != 0)
                return false;
            i--;
        }
        return true;
    }
}
```
### Approach#2 Better Brute Force [Time Limit Exceeded]

- 时间复杂度：O(x) x为最后返回解的值
- 空间复杂度：O(log(max_int)=32) 递归深度能达到32

```java
public class Solution {
    public int findIntegers(int num) {
        return find(0, 0, num, false);
    }
    //从后往前添加位数，i表示当前位数。
    public int find(int i, int sum, int num, boolean prev) {
        if (sum > num)
            return 0;
        if (1<<i > num)
            return 1;
        //如果之前的前缀为1，那么添加一位后只能加0，比如当前为1，添加一位则01
        if (prev)
            return find(i + 1, sum, num, false);
        // 否则可以添加0也可以添加1
        return find(i + 1, sum, num, false) + find(i + 1, sum + (1 << i), num, true);
    }
}
```
### Approach#3 Using Bit Manipulation [Accepted]
递推公式f(n) = f(n-1) + f(n-2)
具体思路如下：

```
输入的值为100110110，那么我们可以转化为f(100000000)+f(100000)+f(10000)-1
用公式求出1~100000000后，只需要100000001~100110110的个数，转化为110110的个数，同理，只需要求100000的个数加上10110的个数，由于前面一个是1，所以当前的位数不能为1，那么就是f(10000)-1的个数
```
- 时间复杂度：O(32)
- 空间复杂度：O(32)

```java
public class Solution {
    public int findIntegers(int num) {
        int[] f = new int[32];
        f[0] = 1;
        f[1] = 2;
        for (int i = 2; i < f.length; i++)
            f[i] = f[i - 1] + f[i - 2];
        int i = 30, sum = 0, prev_bit = 0;
        while (i >= 0) {
            if ((num & (1 << i)) != 0) {
                sum += f[i];
                if (prev_bit == 1) {
                    sum--;
                    break;
                }
                prev_bit = 1;
            } else
                prev_bit = 0;
            i--;
        }
        return sum + 1;
    }
}
```

## 参考资料
1.[https://leetcode.com/articles/non-negative-integers-without-consecutive-ones/](https://leetcode.com/articles/non-negative-integers-without-consecutive-ones/)