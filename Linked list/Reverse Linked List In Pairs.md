# 1 Description
Reverse pairs of elements in a singly-linked list.
# 2 Examples
L = null, after reverse is null
L = 1 -> null, after reverse is 1 -> null
L = 1 -> 2 -> null, after reverse is 2 -> 1 -> null
L = 1 -> 2 -> 3 -> null, after reverse is 2 -> 1 -> 3 -> null
# 3 Solution
public class Solution {
  public ListNode reverseInPairs(ListNode head) {
    // Write your solution here
    if(head==null||head.next==null){
      return head;
    }
    ListNode cur=head;
    ListNode next;
    ListNode pre=null;
    while(cur!=null&&cur.next!=null){
      next=cur.next;
      cur.next=next.next;
      next.next=cur;
      if(pre==null){
        head=next;
      }else{
        pre.next=next;
      }
      pre=cur;
      cur=cur.next;
    }
    return head;
  }
}
