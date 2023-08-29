#  Java 刷题整理
```java
if(A == B){
do something;
}

```
```java
while(A < B){
do something;
}

```
#array
## two pointers

异向双指针
```java
int i=0 ; j= arr.length -1;
while(i < j){
i++;
j++;
}
```

同向双指针
优势：不改变原来的顺序
```java
int i=0 ; j= 0;
while(j < arr.length - 1){
if ( i == 0 || arr[j] != arr[i-1]){
arr[i++] = arr[j++];
} else{
j++;
}
```

## 其他笔记
new a Array

```java
 int[] num1Copy= new int[m];
```
 
在java输出2D表格的时候，需要将 convert the output from a 2D Array to a 2D list。

```java
class Solution {
    public List<List<Integer>> shiftGrid(int[][] grid, int k) {

        // Repeat the transform k times.
        for (;k > 0; k--) {

            int previous = grid[grid.length - 1][grid[0].length - 1];
            for (int row = 0; row < grid.length; row++) {
                for (int col = 0; col < grid[0].length; col++) {
                    int temp = grid[row][col];
                    grid[row][col] = previous;
                    previous = temp;
                }
            }
        }

        // Copy the grid into a list for returning.
        List<List<Integer>> result = new ArrayList<>();
        for (int[] row : grid) {
            List<Integer> listRow = new ArrayList<>();
            result.add(listRow);
            for (int v : row) listRow.add(v);
        }

        return result;
    }
```

## string
```java
class Solution {
    public boolean checkRecord(String s) {
        int count=0;
        for(int i=0;i<s.length();i++){
            if (s.charAt(i)=='A')
             count++;
        }

    return count<2 && s.indexOf("LLL")<0;

        
    }
}
```
```java
String s = String.valueOf(new char[]{'c'}); //将一个char数组转换成String
```
```java
class Solution {
    public void reverseString(char[] s) {
        int i=0;
        int j=s.length-1;
        char temp;

        while(i<j){
            temp= s[i];
            s[i]=s[j];
            s[j]=temp;
            i++;
            j--;
        }
        
    }
}
```


##二分查找 binary search
有序区间

mid (l+r)/2 可能会因为（l+r)数据太大而超出范围；

```java
int i=0; r=arr.length -1 ;
while(1 <= r){
int mid= 1+ (r-l)/2；
if (arr[mid] == k ){
  return mid;
  } else if (arr[mid] > k){
  r = mid -1;
  //重新更改上下限
  }else {
  1 = mid +1;
  }
  }
  return -1;
  }
```
  万用型模糊查找
```java
int l=0 , r= arr.length-1;
while(l< r-1){
int mid = 1 + (r-1)/2;
if ( arr[mid] <k){
l=mid;}
else{
r=mid;
}
}

if (arr[r] < k ) {
return r;
}
else if (arr[l] >k){
return l;
}
else{
return k-arr[l] < arr[r] -k ? l:r
}
```

##revered linked list
high level idea:

1. Ak for next recursion
2. reverse current node
3. renturn reversed head

```java
public ListNode reverse(ListNode head){
if(head == null || head.next == null){
return head;
}
ListNode reversed_head = reverse(head.next);
head.next.next=head;
head.next=null;
return revered_head;
}
```


##heap

heap 排序和 sort 的区别

heap : online algorithm, no fixed length,can scale acording to the new data.

sort array: a set of fixed length data , arrary acqires rescaling every time when new data added.





