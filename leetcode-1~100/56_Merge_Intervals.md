## 56. Merge Intervals
Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].
## Solution

### Solution1
第一次做的时候，没通过用例[[1,4],[2,3]]，没有判断是否前一个包括第二范围。

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals==null||intervals.size()<=0){
            return new LinkedList<>();
        }
        List<Interval> res = new ArrayList<>();
        intervals.sort((o1, o2) -> {
            if (o1.start - o2.start == 0) {
                return o1.end - o2.end;
            } else
                return o1.start - o2.start;
        });
        for (int i = 0; i < intervals.size()-1; i++) {
            Interval cur =intervals.get(i), next = intervals.get(i+1);
            if (cur.end>=next.start){
                //注意这里需要判断是否前一个包含后一个
                if (cur.end>=next.end){
                    next.start = cur.start;
                    next.end = cur.end;
                }
                else {
                    next.start = cur.start;
                }
            }else {
                res.add(cur);
            }
        }
        res.add(intervals.get(intervals.size()-1));
        return res;
    }

}
```


### Solution2
和第一种方法略有不同。但效率高很多，不需要从list多次遍历节点

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> res = new ArrayList<>();
        if (intervals == null || intervals.size() <= 1) {
            return intervals;
        }
        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval a, Interval b) {
                if (a.start != b.start) {
                    return a.start - b.start;
                } else {
                    return a.end - b.end;
                }
            }
        }); 
        
        int start = intervals.get(0).start, end = intervals.get(0).end;
        for (int i = 1; i < intervals.size(); i++) {
            if (intervals.get(i).start > end) {
                res.add(new Interval(start, end));
                start = intervals.get(i).start;
                end = intervals.get(i).end;
            } else {
                end = Math.max(intervals.get(i).end, end);
            }
        }
        res.add(new Interval(start, end));
        return res;
    }
}
```

### Solution3
Excellent Solution!!!效率很高。以空间换取时间

```java
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        int n = intervals.size();
	int[] starts = new int[n];
	int[] ends = new int[n];
	for (int i = 0; i < n; i++) {
		starts[i] = intervals.get(i).start;
		ends[i] = intervals.get(i).end;
	}
	Arrays.sort(starts);
	Arrays.sort(ends);
	// loop through
	List<Interval> res = new ArrayList<Interval>();
	for (int i = 0, j = 0; i < n; i++) { // j is start of interval.
		if (i == n - 1 || starts[i + 1] > ends[i]) {
			res.add(new Interval(starts[j], ends[i]));
			j = i + 1;
		}
	}
	return res;
    }
}
```