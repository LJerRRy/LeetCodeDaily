## 604. Design Compressed String Iterator
Design and implement a data structure for a compressed string iterator. It should support the following operations: next and hasNext.

The given compressed string will be in the form of each letter followed by a positive integer representing the number of this letter existing in the original uncompressed string.

next() - if the original string still has uncompressed characters, return the next letter; Otherwise return a white space.
hasNext() - Judge whether there is any letter needs to be uncompressed.
## Summary

## Solution

### Approach#1

```java
public class StringIterator {
    String s;
    int cnt;
    int i;
    char ch;
    public StringIterator(String c) {
        s = c;
        cnt = 0;
        i = 0;
    }
    
    public char next() {
        if(i>=s.length()&&cnt==0)return ' ';
        if(cnt>0){
            cnt--;
            return ch;
        }
        ch = s.charAt(i++);
        int tmp = i;
        while(i<s.length()&&s.charAt(i)>='0'&&s.charAt(i)<='9')i++;
        cnt = Integer.parseInt(s.substring(tmp,i));
        cnt--;
        return ch;
    }
    
    public boolean hasNext() {
        if(i>=s.length()&&cnt==0)return false;
        return true;
    }
}

/**
 * Your StringIterator object will be instantiated and called as such:
 * StringIterator obj = new StringIterator(compressedString);
 * char param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```
### Approach#2
利用队列

```java
public class StringIterator {
    
    Queue<int[]> queue = new LinkedList<>();
    
    public StringIterator(String s) {
        int i = 0, n = s.length();
        while (i < n) {
            int j = i+1;
            while (j < n && s.charAt(j) - 'A' < 0) j++;
            queue.add(new int[]{s.charAt(i) - 'A',  Integer.parseInt(s.substring(i+1, j))});
            i = j;
        }
    }
    
    public char next() {
        if (queue.isEmpty()) return ' ';
        int[] top = queue.peek();
        if (--top[1] == 0) queue.poll();
        return (char) ('A' + top[0]);
    }
    
    public boolean hasNext() {
        return !queue.isEmpty();
    }

}
```