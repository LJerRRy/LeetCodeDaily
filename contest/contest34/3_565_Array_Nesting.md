## 565. Array Nesting
A zero-indexed array A consisting of N different integers is given. The array contains all integers in the range [0, N - 1].

Sets S[K] for 0 <= K < N are defined as follows:

S[K] = { A[K], A[A[K]], A[A[A[K]]], ... }.

Sets S[K] are finite for each K and should NOT contain duplicates.

Write a function that given an array A consisting of N integers, return the size of the largest set S[K] for this array.

```
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```
## Summary
典型的DFS问题。
## Solution

### Approach#1
暴力搜索，将会超时，不能通过测试
- 时间复杂度：O(n^2) 
- 空间复杂度：O(n)

```java
public class Solution {
    public int arrayNesting(int[] nums) {
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            int start = nums[i], count = 0;
            do {
                start = nums[start];
                count++;
            }
            while (start != nums[i]);
            res = Math.max(res, count);

        }
        return res;
    }
}
```

### Approach#2

- 时间复杂度：O(n) 因为访问过的点将不会再被访问，所以时间复杂度为n
- 空间复杂度：O(n)

```java
public class Solution {
    public int arrayNesting(int[] nums) {
        int n = nums.length;
        boolean[] visited = new boolean[n];
        int answer = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                int cur = i;
                int count = 0;
                do {
                    visited[cur] = true;
                    cur = nums[cur];
                    count++;
                } while (cur != i);
                answer = Math.max(answer, count);
            }
        }
        return answer;
    }
}
```
### Approach#3

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```java
public class Solution {
    public int arrayNesting(int[] nums) {
        int max = Integer.MIN_VALUE;
        boolean[] visited = new boolean[nums.length];
        for (int i = 0; i < nums.length; i++) {
        	if (visited[i]) 
        		continue;
        	max = Math.max(max, calcLength(nums, i, visited));
        }
        return max;
    }
	
	private int calcLength(int[] nums, int start, boolean[] visited) {
		int i = start, count = 0;
		while (count == 0 || i != start) {
			visited[i] = true;
			i = nums[i];
			count++;
		}
		return count;
	}
}
```

### Approach#4
已经被访问过的数组只需要在原来的数组上做标记即可，这样空间复杂度为O(1)
- 时间复杂度：O(n)
- 空间复杂度：O(1)

```java
public class Solution {
    public int arrayNesting(int[] nums) {
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != Integer.MAX_VALUE) {
                int start = nums[i], count = 0;
                while (nums[start] != Integer.MAX_VALUE) {
                    int temp = start;
                    start = nums[start];
                    count++;
                    nums[temp] = Integer.MAX_VALUE;
                }
                res = Math.max(res, count);
            }
        }
        return res;
    }
}
```