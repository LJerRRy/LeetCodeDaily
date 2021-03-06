## 648. Replace Words
In English, we have a concept called root, which can be followed by some other words to form another longer word - let's call this word successor. For example, the root an, followed by other, which can form another word another.

Now, given a dictionary consisting of many roots and a sentence. You need to replace all the successor in the sentence with the root forming it. If a successor has many roots can form it, replace it with the root with the shortest length.

You need to output the sentence after the replacement.

Example 1:
Input: dict = ["cat", "bat", "rat"]
sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
Note:
1. The input will only have lower-case letters.
2. 1 <= dict words number <= 1000
3. 1 <= sentence words number <= 1000
4. 1 <= root length <= 100
5. 1 <= sentence words length <= 1000
## Summary

## Solution

### Approach#1
遍历字典

```java
public class Solution {
    public String replaceWords(List<String> dict, String s) {
        String[] t = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for (String i:t){
            boolean flag = false;
            for(String j:dict){
                if(i.startsWith(j)){
                    sb.append(" ");
                    sb.append(j);
                    flag = true;
                    break;
                }
            }
            if(!flag){
                sb.append(" ");
                sb.append(i);
            }
        }
        return sb.toString().trim();
    }
}
```
### Approach#2
遍历字符串，利用Hash Table

```java
public class Solution {
    public String replaceWords(List<String> dict, String sentence) {
        if (dict == null || dict.size() == 0) return sentence;
        
        Set<String> set = new HashSet<>();
        for (String s : dict) set.add(s);
        
        StringBuilder sb = new StringBuilder();
        String[] words = sentence.split("\\s+");
        
        for (String word : words) {
            String prefix = "";
            for (int i = 1; i <= word.length(); i++) {
                prefix = word.substring(0, i);
                if (set.contains(prefix)) break;
            }
            sb.append(" " + prefix);
        }
        
        return sb.deleteCharAt(0).toString();
    }
}
```