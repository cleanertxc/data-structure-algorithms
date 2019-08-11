# Description
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

# Example:
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

# Note:

- Only constant extra memory is allowed.
- You may not alter the values in the list's nodes, only nodes itself may be changed.

# Solution
```java
//This is an ugly(i think) iterative solution to traverse all the linkedlist, time complexity is supposed to be O(n)
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode cur=head;
        ListNode result=head;
        ListNode[] res=new ListNode[2];
        while(cur!=null){
            int count=1;
            ListNode rec=cur;
            while(cur!=null&&count<k){
                cur=cur.next;
                count++;
            }
            if(cur!=null){
                if(rec!=head){
                    res[1].next=cur;
                }
                cur=cur.next;
                res=reverse(rec,k);
                if(rec==head){
                    result=res[0];
                }
            }else{
                if(rec==head){
                    return rec;
                }else{
                    res[1].next=rec;
                    return result;
                }
            }
            
        }
        return result;
    }
    
    private ListNode[] reverse(ListNode head,int k){
        ListNode[] res=new ListNode[2];
        ListNode pre=null;
        ListNode cur=head;
        ListNode next;
        for(int i=0;i<k;i++){
            next=cur.next;
            cur.next=pre;
            pre=cur;
            cur=next;
            
        }
        res[0]=pre;
        res[1]=head;
        return res;
    }
}
```
