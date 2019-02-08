<h1>Technical Interview Practice</h1>

<h2>Problem 1</h2>

Given an unsorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2`, return `1->2`.
Given `1->1->2->3->3`, return `1->2->3`.

<h3>Problem 1 - Solution</h3>

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     public int val;
 *     public ListNode next;
 *     ListNode(int x) { val = x; next = null; }
 * }
 */
public class Solution {
	public ListNode deleteDuplicates(ListNode a) {
	    ListNode head = a;
	    ListNode hold = a;
	    HashSet<Integer> used = new HashSet<>();
	    
	    while (a.next != null) {
	        if (used.contains(a.val)){
	            hold.next = a.next;
	            a = hold.next;
	        } else {
	            used.add(a.val);
	            a = a.next;
	            
	            if (hold.next != a) {
	                hold = hold.next;
	            }
	        }
	    } 
	    if (used.contains(a.val)) {
	        hold.next = a.next;
	        a = hold.next;
	    }
	    return head;
	}
}
```

<h2>Problem 2</h2>

Write a function that takes an unsigned integer and returns the number of `1` bits it has.

**Example:**

The 32-bit integer `11` has binary representation

```
00000000000000000000000000001011
```

so the function should return `3`.

<h3>Problem 2 - Solution</h3>

```Javascript
public class Solution {
	public int numSetBits(long A) {
	    int count = 0;
	    while (A > 0) {
	        if ( (A & 1) != 0)
	            count++;
	        A >>= 1;
	    } 
	    return count;  
	}
}
```


<h2>Problem 3</h2>

Given an integer n, return the number of trailing zeroes in n!.

*Note: Your solution should be in logarithmic time complexity.*

**Example :**

```
n = 5
n! = 120 
Number of trailing zeros = 1
So, return 1
```

<h3>Problem 3 - Naïve Solution</h3>

```java
public class Solution {
	public int trailingZeroes(int a) {
		int factorial = 1;
		int counter = 0;
	    
		for (int factor = 2; factor <= a; factor++)
			factorial *= factor;
        
		while (factorial % 10 == 0) {
			counter++;
			factorial /= 10;
		}
	    
		return counter;
	}
}
```

<h3>Problem 3 - Fancy Solution</h3>

```java
public class Solution {
	public int trailingZeroes(int a) {
		int sum=0;
	    
		for(int i=5; i <= a; i*=5) 
			sum += a/i;
            
		return sum;
	}
}
```



