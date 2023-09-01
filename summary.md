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
# array
```java
Arrays.sort();
```

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

937不会



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

# linked list
new a linked list
```java
 ListNode dummy=new ListNode(0);
 ```

```java
lass Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy=new ListNode(0);
        ListNode curr = dummy;
        int carry =0;

        while(l1!=null || l2!=null || carry ==1){
            int sum=0;
            if(l1 != null){
                sum+=l1.val;
                l1=l1.next;
            }
            if(l2 != null){ // adding l2 to our sum & moving l2
                sum += l2.val;
                l2 = l2.next;
            }
            sum+=carry;
            carry=sum/10;
            ListNode node= new ListNode(sum%10);
            curr.next = node;
            curr = curr.next;
        }
        return dummy.next;

        }
    }
```



## revered linked list
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


##stack
stake
特性：last in first out
适用于记录之前的状态，必要的时候可以回到之前的状态，或者利用之前的值；
不像array，不能用Index访问，只能每次拿stack 顶的元素；

dynamic programming
DP：记录之前所有的状态，随时可能访问任何一个子问题，所以通常用array或者HASH table，而且不会回到之前的状态，只会利用之前的值

stack 有两个操作：
peek
pop

queue 有两个操作：
enqueue
dequeue


739
找到下一个温度高的离了多少天

## queue

移动窗口
```java
class MovingAverage {
    int size,windowSum = 0, count =0;
    Deque queue = new ArrayDeque<Integer>();


    public MovingAverage(int size) {
        this.size = size;
        
    }
    
    public double next(int val) {
        ++count;
        queue.add(val);
        int tail = count > size ? (int)queue.poll():0;
        windowSum = windowSum - tail + val;
        return windowSum * 1.0 / Math.min(size, count);

        
    }
}
```

queue 变 Stack
```java
class MyStack 
{
    Queue<Integer> queue;
    
    public MyStack()
    {
        this.queue=new LinkedList<Integer>();
    }
    
    // Push element x onto stack.
    public void push(int x) 
    {
       queue.add(x);
       for(int i=0;i<queue.size()-1;i++)
       {
           queue.add(queue.poll());
       }
    }

    // Removes the element on top of the stack.
    public int pop() 
    {
        int x=queue.poll();
        return x;
    }

    // Get the top element.
    public int top() 
    {
        return queue.peek();
    }

    // Return whether the stack is empty.
    public boolean empty() 
    {
        return queue.isEmpty();
    }
}
```

```java
  int tail = count > size ? (int)queue.poll():0;
```
int tail = count > size ? (int)queue.poll() : 0;：检查窗口是否已经满了（count > size）。如果窗口已满，则从队列的头部移除一个元素，并将其赋值给tail。如果窗口未满，则tail保持为0

```java
public class MovingAverage {
    private int [] window;
    private int n, insert;
    private long sum;
    
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        window = new int[size];
        insert = 0;
        sum = 0;
    }
    
    public double next(int val) {
        if (n < window.length)  n++;
        sum -= window[insert];
        sum += val;
        window[insert] = val;
        insert = (insert + 1) % window.length;
        
        return (double)sum / n;
    }
}
```


## heap

heap 排序和 sort 的区别

heap : online algorithm, no fixed length,can scale acording to the new data.

sort array: a set of fixed length data , arrary acqires rescaling every time when new data added.


## Hashmap


two sum

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0;i < nums.length;i++){
            if(map.containsKey(target-nums[i])){
                return new int[] {map.get(target-nums[i]),i};
            }
            map.put(nums[i], i);
        }
        return null;
    }
}
```

这个例子中 index是 nums[i]，而里面的值是i 

example：

```java
import java.util.HashMap; // import the HashMap class

HashMap<String, String> capitalCities = new HashMap<String, String>();
```

```java
import java.util.HashMap;

public class Main {
  public static void main(String[] args) {
    // Create a HashMap object called capitalCities
    HashMap<String, String> capitalCities = new HashMap<String, String>();

    // Add keys and values (Country, City)
    capitalCities.put("England", "London");
    capitalCities.put("Germany", "Berlin");
    capitalCities.put("Norway", "Oslo");
    capitalCities.put("USA", "Washington DC");
    System.out.println(capitalCities);
  }
}
```

```java
capitalCities.get("England");
```
```java
capitalCities.remove("England");
```
```java
capitalCities.clear();
```
```java
// Print keys
for (String i : capitalCities.keySet()) {
  System.out.println(i);
}
```
```java
// Print values
for (String i : capitalCities.values()) {
  System.out.println(i);
}
```

```java
// Print keys and values
for (String i : capitalCities.keySet()) {
  System.out.println("key: " + i + " value: " + capitalCities.get(i));
}
```

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

 

Example 1:

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
Example 2:

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.


```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashSet<Integer> container = new HashSet<>();
        HashSet<Integer> output = new HashSet<>();

        for (int num:nums1){
            container.add(num);
        }
        for (int num:nums2){
            if(container.contains(num)){
                output.add(num);
            }
        }

        int[] outputArray = new int[output.size()];
        int index = 0;
        for (int x:output){
            outputArray[index] = x;
            index++;
        }

        return outputArray;
        
    }
}
```

359. Logger Rate Limiter
     
Design a logger system that receives a stream of messages along with their timestamps. Each unique message should only be printed at most every 10 seconds (i.e. a message printed at timestamp t will prevent other identical messages from being printed until timestamp t + 10).

All messages will come in chronological order. Several messages may arrive at the same timestamp.

Implement the Logger class:

Logger() Initializes the logger object.
bool shouldPrintMessage(int timestamp, string message) Returns true if the message should be printed in the given timestamp, otherwise returns false.
 

Example 1:

Input
["Logger", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage", "shouldPrintMessage"]
[[], [1, "foo"], [2, "bar"], [3, "foo"], [8, "bar"], [10, "foo"], [11, "foo"]]
Output
[null, true, true, false, false, false, true]

Explanation
Logger logger = new Logger();
logger.shouldPrintMessage(1, "foo");  // return true, next allowed timestamp for "foo" is 1 + 10 = 11
logger.shouldPrintMessage(2, "bar");  // return true, next allowed timestamp for "bar" is 2 + 10 = 12
logger.shouldPrintMessage(3, "foo");  // 3 < 11, return false
logger.shouldPrintMessage(8, "bar");  // 8 < 12, return false
logger.shouldPrintMessage(10, "foo"); // 10 < 11, return false
logger.shouldPrintMessage(11, "foo"); // 11 >= 11, return true, next allowed timestamp for "foo" is 11 + 10 = 21

```java
class Logger {
    private HashMap<String, Integer> msgDict;

    public Logger() {
        msgDict = new HashMap<String, Integer>();

    }
    
    public boolean shouldPrintMessage(int timestamp, String message) {

        if(!this.msgDict.containsKey(message)){
            this.msgDict.put(message, timestamp);
            return true;

        }

        Integer oldTimestamp = this.msgDict.get(message);
        if ((timestamp - oldTimestamp)>= 10){
            this.msgDict.put(message, timestamp);
            return true;
        }
        else{
            return false;
        }
        
        
    }
}
```
注意在程序中的：
this.msgDict.put/containsKey 中的this建议加上不会出错。

```java
Hash_Map.containsValue(Object Value)
```
also can find the Value in HashMap

```java
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        HashMap < Integer, Integer > map = new HashMap < > ();
        map.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

HashMap:

HashMap 是一个基于哈希表的数据结构，用于存储键值对。
允许使用 null 作为键，但只能有一个。
允许使用 null 作为值。
不保证元素的顺序，即不保证键值对的插入和迭代顺序一致。
允许键值对的键是不可变对象（通常使用不可变对象作为键）。
HashMap 是非线程安全的，需要在多线程环境下使用适当的同步措施。
HashSet:

HashSet 是基于哈希表的集合实现，用于存储唯一的元素（不重复）。
允许使用 null 元素，只能有一个。
不保证元素的顺序，即不保证元素的插入和迭代顺序一致。
HashSet 使用哈希函数来确定元素的存储位置，从而提高了查找和插入操作的效率。

##tree
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null){
            return res;
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);

        while(!q.isEmpty()){
            int size = q.size();
            List<Integer> level = new ArrayList<>();
            for(int i =0;i < size;i++){
            TreeNode cur = q.poll();
            level.add(cur.val);
            if(cur.left != null){
                q.offer(cur.left);
            }
            if(cur.right != null){
                q.offer(cur.right);
            }
            }
            res.add(level);


        }
        return res;
    }
}
```

深度搜索递归

```java
class Solution {
    int max= Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        path(root);
        return max;
        
    }

    private int path(TreeNode node){
        if(node == null){
            return 0;
        }

        int left = path(node.left);
        int right = path(node.right);
        left = left < 0? 0:left;
        right = right < 0? 0:right;
        max= Math.max(max,left+right+node.val);
        return Math.max(left+node.val,right+node.val);
}
}
```


