## 49. Group Anagrams

Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:

[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
Note: All inputs will be in lower-case.
## Solution
将同字母异顺序词分类

### Solution1

```java
public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        for(String s : strs){
            String tmp = sortString(s);
            if (map.containsKey(tmp)){
                //下面三行可以简化成一行
                //map.get(tmp).add(s);
                List<String> list = map.get(tmp);
                list.add(s);
                map.put(tmp, list);
            }else{
                List<String> list = new LinkedList<String>();
                list.add(s);
                map.put(tmp, list);
            }
        }
        List<List<String>> res = new LinkedList<>();
        res.addAll(map.values());
        return res;
    }
    private String sortString(String s){
        if (s == null||s.length()==0)return "";
        char[] a = s.toCharArray();
        Arrays.sort(a);
        return String.valueOf(a);
    }
}
```

### Solution2
这方法不错不错哦，将每个字母映射成一个质数，而后字符串将各个质数相乘，以乘积作为map的key

```java
public class Solution {
    
    /*
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<String, List<String>>();
        List<List<String>> result = new LinkedList<List<String>>();
        if(strs == null || strs.length == 0) return result;
        for(String str : strs) {
            char[] charArray = str.toCharArray();
            Arrays.sort(charArray);
            String sortedstr = String.valueOf(charArray);
            if(!map.containsKey(sortedstr)) {
                map.put(sortedstr, new LinkedList<String>());
            }
            map.get(sortedstr).add(str);
        }
        for(List<String> list : map.values()) {
            result.add(list);
        }
        
        //HOW TO GET ALL KEYS
        //for(String key : map.keySet()) {
        //    System.out.println(key);
        //}
        return result;
        //HOW TO GET ALL VALUES
        //you need to remember map.values();
        //return new LinkedList<List<String>>(map.values());
    }
    */
        
    public static List<List<String>> groupAnagrams(String[] strs) { 
        int[] prime = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103};
        List<List<String>> res = new ArrayList<>();
        HashMap<Integer, Integer> map = new HashMap<>();
        for (String s : strs) {
            int key = 1;
            for (char c : s.toCharArray()) {
                key *= prime[c - 'a'];
            }
            List<String> t;
            if (map.containsKey(key)) {
                t = res.get(map.get(key));
            } else {
                t = new ArrayList<>();
                res.add(t);
                map.put(key, res.size() - 1);
            }
            t.add(s);
        }
        return res;
    }
}
```