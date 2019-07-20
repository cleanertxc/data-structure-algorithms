# Description
Given a singly-linked list, where each node contains an integer value, sort it in ascending order. The insertion sort algorithm should be used to solve this problem.

# Examples
- null, is sorted to null
- 1 -> null, is sorted to 1 -> null
- 1 -> 2 -> 3 -> null, is sorted to 1 -> 2 -> 3 -> null
- 4 -> 2 -> 6 -> -3 -> 5 -> null, is sorted to -3 -> 2 -> 4 -> 5 -> 6

#Sulotion
```java
public class Solution {
  public ListNode insertionSort(ListNode head) {
    // Write your solution here
    if(head==null||head.next==null){
      return head;
    }
    ListNode dummy=new ListNode(0);
    dummy.next=head;
    ListNode cur=head;
    while(cur!=null){
      ListNode pre=dummy;
      cur=head;
      while(cur.next!=null&&pre.next.value<=cur.next.value){
        pre=pre.next;
        cur=cur.next;
      }
      if(cur.next==null){
        return dummy.next;
      }
      if(cur==head){
        head=cur.next;
      }
      ListNode mark=pre.next;
      pre.next=cur.next;
      cur.next=cur.next.next;
      pre.next.next=mark;
    }
    return dummy.next;
  }
}
//注意corner case的判断

```
