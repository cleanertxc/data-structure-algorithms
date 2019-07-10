# 1 Description
Given a singly-linked list, where each node contains an integer value, sort it in ascending order. The merge sort algorithm should be used to solve this problem.

# 2 Examples
- null, is sorted to null
- 1 -> null, is sorted to 1 -> null
- 1 -> 2 -> 3 -> null, is sorted to 1 -> 2 -> 3 -> null
- 4 -> 2 -> 6 -> -3 -> 5 -> null, is sorted to -3 -> 2 -> 4 -> 5 -> 6

# 3 Solution
```java
/**
 * class ListNode {
 *   public int value;
 *   public ListNode next;
 *   public ListNode(int value) {
 *     this.value = value;
 *     next = null;
 *   }
 * }
 */

public class Solution {
  public ListNode mergeSort(ListNode head) {
    // Write your solution here
    if(head ==null||head.next==null){
      return head;
    }
    ListNode mid =getMiddle(head);
    ListNode nexttomid=mid.next;
    mid.next=null;
    ListNode left=mergeSort(head);
    ListNode right=mergeSort(nexttomid);
    ListNode sortedHead = sortedMerge(left,right);
    return sortedHead;  
  }
  
  private ListNode sortedMerge(ListNode left, ListNode right){
    ListNode result=null;
    if(left==null){
      return right;
    }
    if(right==null){
      return left;
    }
    if(left.value<=right.value){
      result=left;
      result.next=sortedMerge(left.next,right);
    }else{
      result=right;
      result.next=sortedMerge(left,right.next);
    }
    return result;
  }
  
  private ListNode getMiddle(ListNode head){
    if(head==null){
      return head;
    }
    ListNode slow=head;
    ListNode fast=head.next;
    while(fast!=null){
      fast=fast.next;
      if(fast!=null){
        slow=slow.next;
        fast=fast.next;
      }
    }
    return slow;
  }
}

```
