# Linked List

<details>
<summary><b> Reverse a linked list </b>
</summary>

Reversing a linked list is a popular problem
there are multiple ways to do it.

### Simple Iterative Approach

This is easy to understand but for some reason I am unable to come up with this on my own even after I have read it 3-4 times 
```
Here I am just trying to reverse the link one by one
head-> 1 -> 2-> 3-> 4-> 5 -> null
we do somthing similar to swapping
where, swap(a,b) is
{
    temp = b
    b = a
    a = temp
}

I will keep prev, curr and fwd  to swap links while moving forward 
initially: 
prev = null,
curr = head,
fwd = null

// I always have to look this up, maybe I m dumb!
while curr is not null:
    fwd = curr.next
    curr.next = prev
    prev = curr
    curr = fwd
```
Image to visualize it better
![text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/RGIF2.gif)
Image via: geeksforgeeks

Code for the same is as below

```java
    // I always keep my class definition as leetcode ones
    public static void reverse (ListNode head) {
        ListNode curr = head;
        ListNode fwd, prev;
        while (curr != null) {
            fwd = curr.next;
            curr.next = prev;
            prev = curr;
            curr = fwd;
        }
        // important to change header of linked list
        head = prev;
    }

```

### Recursive approach
This is more intuitive once I understand
```java
    public ListNode reverse (ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }
            // this will return a reversed linked list 
            // after head.next
            ListNode rev = reverseList(head.next);
            // eh! head still points it's previous next 
            // which is now end/last node
            // our new last node will be head! (yes take a min to think)
            head.next.next = head; // looks magical but head points to last node and last node should point to head now
            // now head is last node so it must point to null
            head.next = null;
            return rev;
    }
```
</details>

<details>
<summary> <b>
Add first method (can be used as helper in many questions)
</b>
</summary>
I saw this in a pepcoding tutorial and found it really useful 

</details>
