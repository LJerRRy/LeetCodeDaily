## 609. Find Duplicate File in System
Given a list of directory info including directory path, and all the files with contents in this directory, you need to find out all the groups of duplicate files in the file system in terms of their paths.

A group of duplicate files consists of at least two files that have exactly the same content.

A single directory info string in the input list has the following format:

`"root/d1/d2/.../dm f1.txt(f1_content) f2.txt(f2_content) ... fn.txt(fn_content)"`

It means there are n files (f1.txt, f2.txt ... fn.txt with content f1_content, f2_content ... fn_content, respectively) in directory root/d1/d2/.../dm. Note that n >= 1 and m >= 0. If m = 0, it means the directory is just the root directory.

The output is a list of group of duplicate file paths. For each group, it contains all the file paths of the files that have the same content. A file path is a string that has the following format:

`"directory_path/file_name.txt"`

```
Input:
["root/a 1.txt(abcd) 2.txt(efgh)", "root/c 3.txt(abcd)", "root/c/d 4.txt(efgh)", "root 4.txt(efgh)"]
Output:  
[["root/a/2.txt","root/c/d/4.txt","root/4.txt"],["root/a/1.txt","root/c/3.txt"]]
```

**Follow up beyond contest:**
1. Imagine you are given a real file system, how will you search files? DFS or BFS ?
2. If the file content is very large (GB level), how will you modify your solution?
3. If you can only read the file by 1kb each time, how will you modify your solution?
4. What is the time complexity of your modified solution? What is the most time consuming part and memory consuming part of it? How to optimize?
5. How to make sure the duplicated files you find are not false positive?
## Summary

## Solution
给定文件夹路径，找出相同的文件。
### Approach#1

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```java
public class Solution {
    public List<List<String>> findDuplicate(String[] paths) {
        Map<String, List<String>> map = new HashMap<>();
        List<List<String>> res = new LinkedList<>();
        for(String s : paths){
            String[] t = s.split(" ");
            if (t.length <= 1)continue;
            for (int i = 1; i < t.length; i++) {
                //下面几行操作也可以替换为
                //int pi = t[i].indexOf('(');
                //String content = t[i].substring(pi);
                //String fn = split[i].substring(0, pi);
                String[] p = t[i].split("\\(");
                String fn = t[0] + "/" + p[0];
                String content = p[1].substring(0,p[1].length()-1);
                if(map.containsKey(content)){
                    map.get(content).add(fn);
                }else {
                    List<String> list = new LinkedList<>();
                    list.add(fn);
                    map.put(content, list);
                }
            }
        }
        for (String s:map.keySet()){
            if(map.get(s).size()>1){
                res.add(new LinkedList<>(map.get(s)));
            }
        }
        return res;
    }
}
```
### Approach#2
该解法在于充分利用了java8中map的特性
- 时间复杂度：O(n*m) m为文件路径中包含的文件个数，n为文件夹个数
- 空间复杂度：O(n)

```java
public class Solution {
    public static List<List<String>> findDuplicate(String[] paths) {
        Map<String, List<String>> map = new HashMap<>();
        for(String path : paths) {
            String[] tokens = path.split(" ");
            for(int i = 1; i < tokens.length; i++) {
                String file = tokens[i].substring(0, tokens[i].indexOf('('));
                String content = tokens[i].substring(tokens[i].indexOf('(') + 1, tokens[i].indexOf(')'));
                map.putIfAbsent(content, new ArrayList<>());
                map.get(content).add(tokens[0] + "/" + file);
            }
        }
        return map.entrySet().stream().filter(e -> e.getValue().size() > 1).map(e -> e.getValue()).collect(Collectors.toList());
    }
}
```