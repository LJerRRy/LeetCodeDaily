## 605. Can Place Flowers
Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.
## Summary

## Solution
只需要求出最大能种的花数量，然后再比较即可。只需要判断连续零的个数，注意数组开始和结尾的时需要额外添加1.

### Approach#1

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```java
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        //n=0表示不种花，那么肯定符合条件
        if(n==0)return true;
        if(flowerbed==null||flowerbed.length==0)return false;
        if(flowerbed.length==1&&flowerbed[0]==0)return true;
        if(flowerbed.length==1&&flowerbed[0]==1)return false;
        int res = 0;
        if(flowerbed[0]==0&&flowerbed[1]==0){
            flowerbed[0]=1;
            ++res;
        }
        for (int i = 1; i < flowerbed.length - 1; i++) {
            if(flowerbed[i]==0&&flowerbed[i-1]==0&&flowerbed[i+1]==0){
                flowerbed[i] = 1;
                ++res;
            }
        }
        if(flowerbed[flowerbed.length-1]==0&&flowerbed[flowerbed.length-2]==0)res++;
        return res>=n;
    }

    public static void main(String[] args) {
        Solution t = new Solution();
        System.out.println(t.canPlaceFlowers(new int[]{1,0,0,0,0,0,0},3));
    }
}
```
简化版的代码如下：

```java
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int i = 0, count = 0;
        while (i < flowerbed.length) {
            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) && (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
            //优化一下
            if(count>=n)
                return true;
            i++;
        }
        return count >= n;
    }
}
```
### Approach#2
根据不同的零的个数进行判断即可。
- 时间复杂度：O(n)
- 空间复杂度：O(1)

```java
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int m = 0, c = 1;
        for (int i: flowerbed) {
            if (i == 0) {
                ++c;
            } else {
                m += (c - 1) / 2;
                c = 0;
            }
        }
        ++c;
        m += (c - 1) / 2;
        return m >= n;
    }
}
```