# 1 Description
Check if a given linked list has a cycle. Return the node where the cycle starts. Return null if there is no cycle.
# 2 Solution
```java
public class Solution {
  public ListNode cycleNode(ListNode head) {
    // write your solution here
    if(head==null||head.next==null){
      return null;
    }
    ListNode slow=head;
    ListNode fast=head;
    while(fast!=null&&fast.next!=null){
      slow=slow.next;
      fast=fast.next.next;
      if(fast==slow){
        fast=head;
        break;
      }
    }
    if(fast==null||fast.next==null){
      return null;
    }
    while(fast!=slow){
        fast=fast.next;
        slow=slow.next;
    }
    return fast;
  }
}
//需要注意的是：当有环时，将fast放回到链表起点，则fast与slow指针必然再circle的起始位置相遇。
```
