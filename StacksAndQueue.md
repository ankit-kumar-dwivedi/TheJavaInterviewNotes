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
  details..
</details>

