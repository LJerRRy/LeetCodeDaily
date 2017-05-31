## 599. Minimum Index Sum of Two Lists
Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.
## Summary
题意： 求出给定两个字符串数组中相同字符串的数组下标和最小的字符串，返回的是个链表（可能有多个字符串他们下标之和相等）
## Solution

### Approach#1
只需要将其中一个数组其字符串和其下标映射到map中，然后遍历另一个数组，如果map中存在，则保存该字符串，并改变map中value值。
- 时间复杂度：O(n) n为list2和list1中数组长度大的值
- 空间复杂度：O(n) n为map中的长度值

```java
public class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        Map<String,Integer> map = new HashMap<>();
        for (int i = 0; i < list1.length; i++) {
            map.put(list1[i], i);
        }
        String[] t = new String[list1.length];
        int j = 0;
        for (int i = 0; i < list2.length; i++) {
            if(map.containsKey(list2[i])){
                map.put(list2[i],map.get(list2[i])+i);
                t[j++] = list2[i];
            }
        }
        System.out.println(j-1);
        int min = Integer.MAX_VALUE;
        List<Integer> list = new LinkedList<>();
        for(int k = j-1;k>=0;k--){
            int c = map.get(t[k]);
            System.out.print(c+" ");
            if(c<min){
                list.clear();
                System.out.println(t[k]);
                list.add(k);
                min = c;
            }else if(c==min) {
                list.add(k);
            }
        }
        String[] res = new String[list.size()];
        System.out.println(list.size());
        int k = 0;
        for(int c : list){
            res[k++] = t[c];
        }
        return res;
    }
}
```
### Approach#2
Copy from the board. 时间复杂度更高，空间复杂度相对比较低。但更容易理解吧
- 时间复杂度：O(n*m) n和m分别为list1和list2的长度 
- 空间复杂度：O(1) 只用到3000个字符串的额外空间

```java
public class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        String[] ret = new String[3000];
        int p = 0;
        int min = 99999999;
        for(int i = 0;i < list1.length;i++){
            for(int j = 0;j < list2.length;j++){
                if(list1[i].equals(list2[j])){
                    if(i+j < min){
                        min = i+j;
                        p = 0;
                        ret[p++] = list1[i];
                    }else if(i+j == min){
                        ret[p++] = list1[i];
                    }
                }
            }
        }
        //需要注意的是，不能直接返回ret，因为ret数组长度3000，明显返回的数组长度不可能这么长，只需要复制前p个即可。
        return Arrays.copyOf(ret, p);
    }
}
```