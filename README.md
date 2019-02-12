# Java Practice

## Problem 1

Given an unsorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2`, return `1->2`.
Given `1->1->2->3->3`, return `1->2->3`.

### Problem 1 - Solution

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

## Problem 2

Write a function that takes an unsigned integer and returns the number of `1` bits it has.

**Example:**

The 32-bit integer `11` has binary representation

```
00000000000000000000000000001011
```

so the function should return `3`.

### Problem 2 - Solution

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

## Problem 3

Given an integer n, return the number of trailing zeroes in n!.

*Note: Your solution should be in logarithmic time complexity.*

**Example :**

```
n = 5
n! = 120 
Number of trailing zeros = 1
So, return 1
```

### Problem 3 - Naïve Solution

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

### Problem 3 - Fancy Solution

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

## Problem 4

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

### Problem 4 - Solution

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

## Problem 5

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

### Problem 5 - Naïve Solution

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

### Problem 5 - Fancy Solution

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

## Problem 6

Given an array of integers, every element appears twice except for one. Find that single one.

*Note: Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?*

**Example :**

```
Input : [1 2 2 3 1]
Output : 3
```

### Problem 6 - SUPER FANCY Solution

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

## Problem 7

Given a string `s` consists of upper/lower-case alphabets and empty space characters `' '`, return the length of last word in the string.

If the last word does not exist, return `0`.

*Note: A word is defined as a character sequence consists of non-space characters only.*

**Example:**

Given `s = "Hello World"`,

return `5` as `length("World") = 5`.

*Please make sure you try to solve this problem without using library functions. Make sure you only traverse the string once.*

### Problem 7 - Solution

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

## Problem 8

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

**Example :**

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

The above binary tree is symmetric. 
But the following is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

### Problem 8 - Solution

```java
/**
 * Definition for binary tree
 * class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
	public int isSymmetric(TreeNode a) {
	    
	    if (a == null)
	        return 0;
	        
	    if (equal(a.left, a.right)) {
	        return 1;
	    } else {
	        return 0;
	    }
	}
	
	
	public boolean equal(TreeNode node1, TreeNode node2) {
	    
	    if (node1 == null && node2 == null)
	        return true;
	        
	    if (node1 == null || node2 == null)
	        return false;
	    
	    if (node1.val != node2.val)
	        return false;
	    
	    
	    return equal(node1.left, node2.right) && equal(node1.right, node2.left);
	}
	
}
```

## Problem 9

Reverse bits of an 32 bit unsigned integer

**Example 1:**

x = 0,

```
          00000000000000000000000000000000  
=>        00000000000000000000000000000000
```

return `0`

**Example 2:**

x = 3,

```
          00000000000000000000000000000011 
=>        11000000000000000000000000000000
```

return `3221225472`

### Problem 9 - Naïve String Manipulation Solution

```java
import java.math.BigInteger;

public class Solution {
	public static long reverse(long a) {
        String bs = Long.toBinaryString(a);
	    StringBuilder binaryString = new StringBuilder();
	    
	    while (binaryString.length() + bs.length() < 32){
	        binaryString.append("0");
	    }
       
	    binaryString.append(bs);
	    binaryString = binaryString.reverse();
	    
	    return parseLong(binaryString.toString(), 2);
	}
	
	private static long parseLong(String s, int base) {
        return new BigInteger(s, base).longValue();
    }
}
```

### Problem 9 - Solution

```java
public class Solution {
	public long reverse(long A) {
	    long reverse = 0;
	    
	    for (int i = 0; i < 32; i++) {
	        reverse = reverse << 1;
	        if ((A & (1 << i)) != 0)
	            reverse = reverse | 1;
	    }
	    
	    return reverse;
	    
	}
}
```

## Problem 10

**Remove Element**

Given an array and a value, remove all the instances of that value in the array. 
Also return the number of elements left in the array after the operation.

> **Example:**
> If array A is `[4, 1, 1, 2, 1, 3]`
> and value elem is `1`, 
> then new length is `3`, and A is now `[4, 2, 3]`

Try to do it in less than linear additional space complexity.

### Problem 10 - Solution

```java
public class Solution {
	public int removeElement(ArrayList<Integer> a, int b) {
	    for(int i = 0; i < a.size(); i++) {
	        if (a.get(i) == b) {
	            a.remove(i);
	            i--;
	        }
	    }
	    return a.size();
	}
}
```

## Problem 11

Remove duplicates from Sorted Array
Given a sorted array, remove the duplicates in place such that each element appears only once and return the new length.

**Note that even though we want you to return the new length, make sure to change the original array as well in place**

Do not allocate extra space for another array, you must do this in place with constant memory.

> **Example:** 
> Given input array A = `[1,1,2]`,
> Your function should return length = `2`, and A is now `[1,2]`.

### Problem 11 - Solution

```java
public class Solution {
	public int removeDuplicates(ArrayList<Integer> a) {
	    HashSet<Integer> hash = new HashSet<>();
	    
	    for (int i = 0; i < a.size(); i++ ) {
	        if (hash.contains(a.get(i))) {
	            a.remove(i);
	            i--;
	        } else {
	            hash.add(a.get(i));
	        }
	    }
	    
	    return a.size();
	}
}
```

## Problem 12

Reverse digits of an integer.

**Example1:**

x = 123,

return 321

**Example2:**

x = -123,

return -321

Return 0 if the result overflows and does not fit in a 32 bit signed integer

### Problem 12 - Solution

```java
public class Solution {
	public int reverse(int A) {
        int sign = (A > 0) ? 1 : -1;
        long ret = 0;
        
        A *= sign;
        
        while(A > 0) {
            ret *= 10;
            ret += A%10;
            A /= 10;
        }
        
        if (ret > 0x7fffffff) return 0;
        return ((int)ret) * sign;
    }
}
```

## Problem 13

Given a column title as appears in an Excel sheet, return its corresponding column number.

**Example:**

```
    A -> 1
    
    B -> 2
    
    C -> 3
    
    ...
    
    Z -> 26
    
    AA -> 27
    
    AB -> 
```

### Problem 13 - Solution

```java
public class Solution {
    public int titleToNumber(String a) {
        int result = 0;
        // Base 26 Conversion
        for (int i = 0; i < a.length(); i++) {
            result *= 26;
            result += (a.charAt(i) - 'A') + 1;
        }
        return result;
    }
}
```

## Problem 14

Given numRows, generate the first numRows of Pascal’s triangle.

Pascal’s triangle : To generate A[C] in row R, sum up A’[C] and A’[C-1] from previous row R - 1.

**Example:**

Given numRows = 5,

Return

```
[
     [1],
     [1,1],
     [1,2,1],
     [1,3,3,1],
     [1,4,6,4,1]
]
```

### Problem 14 - Solution

```java
public class Solution {
    public ArrayList<ArrayList<Integer>> generate(int a) {
        ArrayList<ArrayList<Integer>> pascal = new ArrayList<>();
        ArrayList<Integer> firstRow = new ArrayList<>();
        int prevRow = 1;
        int ind1 = 0;
        int ind2 = 1;
        
        if (a == 0) return pascal;
        
        firstRow.add(1);
        pascal.add(firstRow);
        
        if (a == 1) return pascal;
        
        ArrayList<Integer> secondRow = new ArrayList<>();
        secondRow.add(1);
        secondRow.add(1);
        pascal.add(secondRow);
        
        for (int i = 0; i < (a - 2); i++) {
            ArrayList<Integer> newRow = new ArrayList<>();
            newRow.add(1);
            
            for(int j = 0; j < prevRow; j++)
                newRow.add(pascal.get(prevRow).get(ind1++) + pascal.get(prevRow).get(ind2++));
        
            newRow.add(1);
            pascal.add(newRow);
            prevRow++;
            ind1 = 0;
            ind2 = 1;
        }   
        
        return pascal;
    }
}
```

## Problem 15

Given a non-negative number represented as an array of digits,

add 1 to the number ( increment the number represented by the digits ).

The digits are stored such that the most significant digit is at the head of the list.

**Example:**

If the vector has `[1, 2, 3]`

the returned vector should be `[1, 2, 4]`

as `123 + 1 = 124`.

> **NOTE:** Certain things are intentionally left unclear in this question which you should practice asking the interviewer.
> For example, for this problem, following are some good questions to ask :
>
> - **Q :** Can the input have 0’s before the most significant digit. Or in other words, is `0 1 2 3` a valid input?
> - **A :** For the purpose of this question, **YES**
> - **Q :** Can the output have 0’s before the most significant digit? Or in other words, is `0 1 2 4` a valid output?
> - **A :** For the purpose of this question, **NO**. Even if the input has zeroes before the most significant digit.

### Problem 15 - Solution

```java
public class Solution {
	public ArrayList<Integer> plusOne(ArrayList<Integer> a) {
        
        for(int i = a.size() - 1; i >= 0; i--) {
            // If the digit is not 9, just increment by 1
            if (a.get(i) != 9) {
                a.set(i, a.get(i) + 1);
                break;
            // Otherwise, set digit to 0 and move back one digit
            // to increment
            } else {
                // Edge case: [9, 9, ..., 9]
                if (i == 0){
                    a.set(0, 1);
                    a.add(0);
                } else {
                    a.set(i, 0);
                }
            }
        }
        
        // Remove leading zeros
        for(int i = 0; a.get(i) == 0; i++)
            a.remove(i--);
        
        return a;
	}
}
```

## Problem 16

Given a linked list, remove the nth node from the end of list and return its head.

For example,
Given linked list: `1->2->3->4->5`, and `n = 2`.
After removing the second node from the end, the linked list becomes `1->2->3->5`.

> **Note:**
> \* If n is greater than the size of the list, remove the first node of the list.

Try doing it using constant additional space.

### Problem 16 - Solution (With test driver)

```java
import java.io.*;
import java.util.*;

class ListNode {
   public int val;
   public ListNode next;
  
  ListNode (int a) {
    this.val = a;
    this.next = null;
  }
}

class Solution {
  
  public static void main(String[] args) {
      ListNode a = new ListNode(1);
      ListNode b = new ListNode(2);
      ListNode c = new ListNode(3);
      ListNode d = new ListNode(4);
      ListNode e = new ListNode(5);

      a.next = b;
      b.next = c;
      c.next = d;
      d.next = e;
    
      a = removeNthFromEnd(a, 5);
    
      while (a != null) {
        System.out.println(a.val);
        a = a.next;
      }
  }
  
  public static ListNode removeNthFromEnd(ListNode a, int b) {
    int listSize = 0;
    ListNode temp = a;

    if (b == 0) {
        return a;
    }

    while (temp != null) {
        listSize++;
        temp = temp.next;
    }

    temp = a;

    if (listSize <= b) {
        temp = a.next;
        a.next = null;
        return temp;
    } else {
        for(int i = 0; i < (listSize - (b + 1)); i++){
            temp = temp.next;
        }

        temp.next = temp.next.next;
    }

    return a;
  }
}
```

## Problem 17 - Asked During Interview

Given a String, determine if it is a palindrome or not.

For example,
`A man, a plan, a canal. Panama!`, and `race  ecar` should return true.

`chicken`, and `gravy` should return false.

### Problem 17 - Solution

```java
public class JavaTest
{
    public static boolean foo (String a) {

        int x = a.length() - 1; 
        int i = 0;

        a = a.toLowerCase();

        while (i != x) {
            while (!Character.isLetter(a.charAt(i)) && (i != x))
                i++;
            
            while (!Character.isLetter(a.charAt(x)) && (i != x))
                x--;

            if (i != x) {
                if ((a.charAt(i) == a.charAt(x))) {
                    x--;
                    i++;
                } else {
                    return false;
                }
            }
        }
        return true;
    }

    public static void main(String [] args)
    {
        String str = "A man, a plan, a canal. Panama!";
        System.out.println(foo(str));
    }
}
```

