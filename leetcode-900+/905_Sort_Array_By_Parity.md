# 905. Sort Array By Parity

Given an array `A` of non-negative integers, return an array consisting of all the even elements of `A`, followed by all the odd elements of `A`.

You may return any answer array that satisfies this condition.

Example 1:

```json
Input: [3,1,2,4]
Output: [2,4,3,1]
The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```

## Solution 1

** 双指针法 **
两端分别去找奇数和偶数，左端找奇数，右端找偶数，交换，然后继续找，直到指针相遇

```java
class Solution {
    public int[] sortArrayByParity(int[] A) {
        int a = 0, b = A.length - 1;
        for (;;) {
            while ((A[a] & 1) == 0 && a<b) a++;
            while ((A[b] & 1) == 1 && a < b) b--;
            if (a == b) break;
            int temp = A[a];
            A[a] = A[b];
            A[b] = temp;
        }
        return A;
    }
}
```