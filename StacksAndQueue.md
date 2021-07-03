# Stack and Queue

<details>
<summary><b> Reverse a stack </b>
</summary>
  
  ### Naive way
  Use two stacks, s1 and s2, initially all the elements are part of stack s1

  ```
  for i in size of s1:
    int x = top of s1;
    move n-1-i elements from s1 to s2
    push back x to s1
    move n-1-1 elements from s2 to s1 

  ```

  ```java
	public static void transfer(Stack<Integer> src, Stack<Integer> dest, int num) {
		for (int i=0; i<num; ++i) {
			dest.push(src.peek());
			src.pop();
		}
	}

	public static void reverseStack(Stack<Integer> s1) {
		Stack<Integer> s2 = new Stack<>();
		int n = s1.size();
		for (int i=0; i<n; ++i) {
			// in java top is obtained using peek()
			Integer x = s1.peek();
			s1.pop();
			transfer(s1,s2,n-1-i);
			s1.push(x);
			transfer(s2,s1,n-1-i);
		}
	}
                                     
```
                                     
### Using recursion
While using recusion we do same steps as above but this time call stack will be used as second stack.

```java
	public static void insertAtBottom(Stack<Integer> stk, Integer x) {
		if (stk.isEmpty()) {
			stk.push(x);
			return;
		}
		Integer data = stk.peek();
		stk.pop();
		insertAtBottom(stk, x);
		stk.push(data);
	}

	public static void reverseStack2(Stack<Integer> stk) {
		if (stk.isEmpty()) {
			return;
		}
		Integer x = stk.peek();
		stk.pop();
		reverseStack(stk);
		insertAtBottom(stk, x);
	}
```

</details>
<details>
<summary> <b>Finding next greater element using stack</b></summary>
	let's say we have an array of size n
	we need to find the next greater element for every element a[i]
	where 0 <= i < n
	
	- when no next greater element exist then assume -1 

```
We start traversing the array from end to start
	for every element:
		// this step will make sure that no element less than current element
		// is left in the stack,
		// say you have 2,1,3,5,7,5
		// after we get 7 stack has (5)
		// pop 5 as 5 cannot be nge for any element left to 7 
		// why? see the image below for better understanding 
		while stack top is less than or equal to element 
			pop the stack top
		next greater element is stack top or -1 in case stack is empty
		// most important step which I tend to forget
		push the current element to stack 
```
	
![test](https://gblobscdn.gitbook.com/assets%2F-M1hB-LnPpOmZGsmxY7T%2F-M1hBADdxsYKAvjevalu%2F-M1hBB0V6J6oCdssH5iq%2F1.png?alt=media)
Image source - https://labuladong.gitbook.io/algo-en/ii.-data-structure/monotonicstack
	
```java
public static int[] nextGreaterElement(int[] arr) {
	//let's make a stack first
	Stack<Integer> stk = new Stack<>();
	int n = arr.length;
	int[] nge = new int[n];
	// traverse the array from end -> start
	for (int i=n-1; i>=0; --i) {
		while (!stk.isEmpty() && stk.peek()<= arr[i]) {
			stk.pop();
		}
		nge[i] = stk.isEmpty() ? -1 : stk.peek();
		stk.push(arr[i]);
	}
	return nge;
} 
					       
```

- If circular array is provided then what changes??
</details>

<details>
<summary><b> Celebrity problem </b>
</summary>
	Suppose you are at a party with n people (labeled from 0 to n - 1) and among them, there may exist one celebrity. The definition of a celebrity is that all the other n - 1 people know him/her but he/she does not know any of them.

Read problem statement here -> https://www.lintcode.com/problem/645/

```
let's say n = 5
we have 0,1,2,3,4
we are provided a function knows(a,b) that tells us weather a knows b (order matters) 

If I say, 2 is our celebrity then everyone knows 2, but 2 doesn't know anyone

    0 	1   2 	3   4 
0 | - |   | y |   | y
1 | y | - | y |   |
2 |   |   | - |   | 
3 |   |   | y | - | y
4 | y |   | y |   | -

	    ^ note that 3 is known by everyone
also note a person may/may not know himself depending on problem statement but it will never matter
```

## Naive way 

check for every person 0 to n-1 and find out know doesn't know anyone
This will be O(n<sup>2</sup>)

## Better way

Since we have to optimize number of calls to knows we can use a stack here

```
let's push every element to the stack from 0 to n-1, in the same order
	while stack is not empty
		pop two elements 
			if e1 knows e2 // this means e2 can be celebrity but e1 cannot
				push back e2
			else // e2 is not known so pop e2
				push back e1

	in the end we are left with only single element who is possible answer
	since we did not compared celebrity person with everyone
		-> we will validate if p is celebrity else return -1

```

```java

	public int findCelebrity(int n) {
	        Stack<Integer> stk = new Stack<>();
	        for (int i=0; i<n; ++i) {
	            stk.push(i);
	        }
	        while (stk.size() > 1) {
	            int p1 = stk.pop();
	            int p2 = stk.pop();
	            // p1 knows p2
	            if (knows(p1, p2)) {
	                //p1 can never be celebrity
	                stk.push(p2);
	            } else {
	                // p1 does not know p2, can be celebrity
	                // p2 is not celebrity
	                stk.push(p1);
	            }
	        }
	        int celeb = stk.pop();
	        for (int i = 0; i<n; ++i) {
	            if(i != celeb && !knows(i,celeb)) {
	                // no celebrity exist
	                return -1;
	            }
	        }
	        return celeb;
	    }

```
</details>
