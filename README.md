<h1>Java Practice</h1>

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

<h2>Problem 4</h2>

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

Try solving it using constant additional space.

**Example :**

```
Input : 

                  ______
                 |     |
                 \/    |
        1 -> 2 -> 3 -> 4

Return the node corresponding to node 3. 
```

<h3>Problem 4 - Solution</h3>

```javascript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     public int val;
 *     public ListNode next;
 *     ListNode(int x) { val = x; next = null; }
 * }
 */
public class Solution {
	public ListNode detectCycle(ListNode a) {
	    
	    if (a == null) {
	        return null;
	    } 
	    
	    HashSet<ListNode> nodes = new HashSet<>();
	    
	    while (a.next != null) {
    	    if (nodes.contains(a)) {
    	        return a;
    	    } else {
    	        nodes.add(a);
    	        a = a.next;
    	    }
	    }
	    
	    return null;
	}
}
```

<h2>Problem 5</h2>

Given an array `A` of integers and another non negative integer `k`, find if there exists 2 indices `i` and `j` such that `A[i] - A[j] = k, i != j`.

**Example :**

Input :

```
A : [1 5 3]
k : 2
```

Output :

```
1
```

as `3 - 1 = 2`

- Return `0 / 1` for this problem.

<h3>Problem 5 - Naïve Solution</h3>

```java
public class Solution {
	public int diffPossible(final List<Integer> a, int b) {
	    for (int i = 0; i < a.size(); i++) {
	        for (int j = 0; j < a.size(); j++) {
	            if (i != j) {
	                if (a.get(i) - a.get(j) == b)
	                    return 1;
	            }
	        }
	    }
	    return 0;
	}
}
```

<h3>Problem 5 - Fancy Solution</h3>

```java
public class Solution {
	public int diffPossible(final List<Integer> A, int B) {
	    
	    HashMap<Integer, Integer> hashMap = new HashMap<>();
	    
	    for (int num : A) {
	        if (hashMap.containsKey(num)) {
	            int value = hashMap.get(num);
	            value++;
	            hashMap.put(num, value);
	        } else {
	            hashMap.put(num, 1);
	        }
	    }
	    
	    for (int num : A) {
	        
	        int n = B + num;
	        
	        if (hashMap.containsKey(n)) {
	            if (num == n && hashMap.get(n) > 1)
	                return 1;
	            else if (num != n)
	                return 1;
	        }
	        
	        n = num - B;
	        
	        if (hashMap.containsKey(n)) {
	            if (num == n && hashMap.get(n) > 1)
	                return 1;
	            else if (num != n)
	                return 1;
	        }
	    }
	    
	    return 0;
	    
	    
	}
}
```

<h2>Problem 6</h2>

Given an array of integers, every element appears twice except for one. Find that single one.

*Note: Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?*

**Example :**

```
Input : [1 2 2 3 1]
Output : 3
```

<h3>Problem 6 - SUPER FANCY Solution</h3>

```java
public class Solution {
	// DO NOT MODIFY THE LIST
	public int singleNumber(final List<Integer> A) {
	    int num = 0;
	    
	    for (int val : A) {
	        num ^= val;
	    }
	    
	    return num;
	    
	}
}
```

<h2>Problem 7</h2>

Given a string `s` consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return `0`.

*Note: A word is defined as a character sequence consists of non-space characters only.*

**Example:**

Given `s = "Hello World"`,

return `5` as `length("World") = 5`.

*Please make sure you try to solve this problem without using library functions. Make sure you only traverse the string once.*

<h3>Problem 7 - Solution</h3>

```java
public class Solution {
	public int lengthOfLastWord(final String a) {
	    int count = 0;
	    boolean firstWord = true;
	    
	    for(int i = a.length(); i > 0; i--) {
	        if (a.charAt(i-1) == ' ' && firstWord) {
	            ;
	        } else {
	            firstWord = false;
    	        if (a.charAt(i-1) == ' ') break;
    	        count++;
	        }
	    }
	    
	    return count;
	}
}
```

