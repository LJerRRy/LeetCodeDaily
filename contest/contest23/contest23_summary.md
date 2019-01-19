> 这次完成了前两道~~，还行吧，一道easy 的和一道medium的，还有两道未完成~

## 字符串与字符数组转换

```java
//string to char[]
char[] c = s.toCharAray();
// char[] to string
String s = String.valueOf(c);
//or
String s = new String(c);
```

## StringBuilder内置函数
`StringBuilder sb = new StringBuilder();`
1. `sb.append()` 能添加很多类型的上去

```java
StringBuilder append(char[] str) 
Appends the string representation of the char array argument to this sequence. 
StringBuilder append(char[] str, int offset, int len)
StringBuilder append(double d) 
Appends the string representation of the double argument to this sequence. 
StringBuilder append(float f) 
Appends the string representation of the float argument to this sequence. 
StringBuilder append(int i) 
Appends the string representation of the int argument to this sequence. 
StringBuilder append(long lng) 
Appends the string representation of the long argument to this sequence. 
StringBuilder append(Object obj)  
```
2. `sb.reverse()`逆转字符
3. `sb.indexOf()`

```java
int indexOf(String str) 
Returns the index within this string of the first occurrence of the specified substring. 
int indexOf(String str, int fromIndex) 
Returns the index within this string of the first occurrence of the specified substring, starting at the specified index. 
```
4. `sb.toString() sb.substring()`

## String内置函数

1. `s.charAt(index) s.substring() toCharArray() toLowerCase() toUpperCase() trim()`
2. `String.valueOf()`静态方法，参数可以为字符数组，字符，浮点数，整数，或者Object。
3. `s.split(String regex)`返回String[]
4. `s.match(String regex)`返回boolean类型

## List类型排序
Collections在java.util包下
1. `List<String> List<Integer>`可以直接调用`Collection.sort(list)`对list进行排序。
2. `Collectionssort(List<T> list, Comparator<? super T> c)`
Sorts the specified list according to the order induced by the specified comparator.

```java
List<Stu> s = new LinkedList<Stu>();
Collections.sort(s, new Comparator<Stu>() {
    public int compare(Stu o1, Stu o2) {
        return o1.id - o2.id;
    }
});

class Stu{
    int id = 0;
    public Stu(int s){
        this.id = s;
    }

    @Override
    public String toString() {
        return "Stu{" +
                "id=" + id +
                '}';
    }
}
```

## 递归构造二叉树




