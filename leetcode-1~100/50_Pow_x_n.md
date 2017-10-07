## 50. Pow(x, n)

Implement pow(x, n).

## Solution

### Solution1 (Iteration)

```java
public class Solution {
    public double myPow(double x, int n) {
        if (n==0)return 1.0;
        double t = 1.0;
        if (n<0){
            x = 1.0/x;
            // 当n = -2147483648时，n=-n就会造成n还是 -2147483648因为int最大值为2147483647;先进行一次乘法
            n = -(n+1);
            t *= x;
        }
        while (n>=1){
            if ((n&1)==1)
                t *= x;
            x *= x;
            n = n>>1;
        }
        return t;
    }
}
```


### Solution2 (Recusion)
nest mypow

```java
double myPow(double x, int n) {
    if(n<0) return 1/x * myPow(1/x, -(n+1));
    if(n==0) return 1;
    if(n==2) return x*x;
    if(n%2==0) return myPow( myPow(x, n/2), 2);
    else return x*myPow( myPow(x, n/2), 2);
}
```


### Solution3 
double mypow

```java
double myPow(double x, int n) { 
    if(n==0) return 1;
    double t = myPow(x,n/2);
    if(n%2) return n<0 ? 1/x*t*t : x*t*t;
    else return t*t;
}
```