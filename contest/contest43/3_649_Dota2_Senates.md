## 649. Dota2 Senates
In the world of Dota2, there are two parties: the Radiant and the Dire.

The Dota2 senate consists of senators coming from two parties. Now the senate wants to make a decision about a change in the Dota2 game. The voting for this change is a round-based procedure. In each round, each senator can exercise one of the two rights:

1. Ban one senator's right: A senator can make another senator lose all his rights in this and all the following rounds.
2. Announce the victory:  If this senator found the senators who still have rights to vote are all from the same party, he can announce the victory and make the decision about the change in the game.
Given a string representing each senator's party belonging. The character 'R' and 'D' represent the Radiant party and the Dire party respectively. Then if there are n senators, the size of the given string will be n.

The round-based procedure starts from the first senator to the last senator in the given order. This procedure will last until the end of voting. All the senators who have lost their rights will be skipped during the procedure.

Suppose every senator is smart enough and will play the best strategy for his own party, you need to predict which party will finally announce the victory and make the change in the Dota2 game. The output should be Radiant or Dire.

Example 1:

```
Input: "RD"
Output: "Radiant"
Explanation: The first senator comes from Radiant and he can just ban the next senator's right in the round 1. 
And the second senator can't exercise any rights any more since his right has been banned. 
And in the round 2, the first senator can just announce the victory since he is the only guy in the senate who can vote.
```
Example 2:

```
Input: "RDD"
Output: "Dire"
Explanation: 
The first senator comes from Radiant and he can just ban the next senator's right in the round 1. 
And the second senator can't exercise any rights anymore since his right has been banned. 
And the third senator comes from Dire and he can ban the first senator's right in the round 1. 
And in the round 2, the third senator can just announce the victory since he is the only guy in the senate who can vote.
```
Note:
The length of the given string will in the range [1, 10,000].
Discuss


## Summary

## Solution

### Approach#1

- 时间复杂度：O(nlogn) 时间复杂度最高的就是R和D各一半，
- 空间复杂度：O(1)

```java
public class Solution {
    public String predictPartyVictory(String s) {
        if(s.length()==1)return s.charAt(0)=='R'?"Radiant":"Dire";
        char[] c = s.toCharArray();
        int sum = c.length, j = 0;
        String res = "";
        while(sum>1){
            int i = j % c.length;
            if(c[i]!='R'&&c[i]!='D'){
                j++;
                continue;
            }
            if(!fun(c[i], c, i)){
                res = c[i]=='R'?"Radiant":"Dire";
                break;
            }else{
                j++;
                sum--;
                if(sum == 1){
                    res = c[i]=='R'?"Radiant":"Dire";
                }
            }
        }
        return res;
    }
    private boolean fun(char c1, char[] c, int i){
        if(c1=='R')c1='D';
        else if(c1=='D')c1='R';
        boolean f = false;
        for(int j = i+1; j%c.length!=i;j++){
            if(c[j%c.length] == c1){
                c[j%c.length] = '0';
                f = true;
                break;
            }
        }
        return f;
    }

}
```
### Approach#2
构建一个循环链表，当R或者D的数量为0的时候终止循环。
- 时间复杂度：O(n)
- 空间复杂度：O(n)

```java
public class Solution {
    private static class Node {
        char val;
        Node next;
        boolean active = true;
        
        public Node(char val) {
            this.val = val;
        }
    }
    public String predictPartyVictory(String senate) {
        int rcnt = 0, dcnt = 0;
        for (int i=0; i<senate.length(); i++) {
            if (senate.charAt(i) == 'R') {
                rcnt++;
            } else {
                dcnt++;
            }
        }
        Node head = new Node('R');
        Node tail = head;
        for (int i=0; i<senate.length(); i++) {
            tail = tail.next = new Node(senate.charAt(i));
        }
        tail.next = head.next;
        Node ptr = head.next;
        while (rcnt > 0 && dcnt > 0) {
            if (ptr.val == 'R') {
                dcnt--;
                for (Node q=ptr; ;q=q.next) {
                    if (q.next.val == 'D') {
                        q.next = q.next.next;
                        break;
                    }
                }
            } else {
                rcnt--;
                for (Node q=ptr; ;q=q.next) {
                    if (q.next.val == 'R') {
                        q.next = q.next.next;
                        break;
                    }
                }
            }
            ptr = ptr.next;
        }
        return rcnt > 0 ? "Radiant" : "Dire";
    }
}
```