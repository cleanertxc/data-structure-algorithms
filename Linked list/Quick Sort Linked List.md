# Description
Given a singly-linked list, where each node contains an integer value, sort it in ascending order. The quick sort algorithm should be used to solve this problem.

# Examples
null, is sorted to null
1 -> null, is sorted to 1 -> null
1 -> 2 -> 3 -> null, is sorted to 1 -> 2 -> 3 -> null
4 -> 2 -> 6 -> -3 -> 5 -> null, is sorted to -3 -> 2 -> 4 -> 5 -> 6

# Solution
```java
public class Solution {
  public ListNode quickSort(ListNode head) {
        // Write your solution here
        if(head==null||head.next==null){
            return head;
        }
        ListNode tail=findTail(head);
        ListNode result=quickSort(head,tail);
        return result;
    }
    private ListNode quickSort(ListNode head, ListNode tail){
        if(head==null||head==tail){
            return head;
        }
        ListNode[] result=partition(head,tail);

        ListNode left  = quickSort(result[0],result[1]);
        
        if(result[1]!=result[2]){
            ListNode leftTail=findTail(left);
            leftTail.next=result[2];
        }
        ListNode right  = quickSort(result[3],result[4]);
        if(result[2]!=result[3]) {
            result[2].next = right;
        }

        return left;
    }

    private ListNode[] partition(ListNode head, ListNode tail){
        ListNode[] result=new ListNode[5];

        int pivot=tail.value;
        ListNode dummy1=new ListNode(0);
        ListNode dummy2=new ListNode(0);
        ListNode cur=head;
        ListNode m=dummy1;
        ListNode n=dummy2;
        while(cur.next!=null){
            if(cur.value<=pivot){
                m.next=cur;
                m=m.next;
                cur=cur.next;
            }else{
                n.next=cur;
                n=n.next;
                cur=cur.next;
            }
        }
        m.next=null;
        n.next=null;
        if(m==dummy1){
            result[0]=tail;//leftHead
            result[1]=tail;//leftTail
            result[2]=tail;//pivot
            result[3]=dummy2.next;//rightHead
            result[4]=n;//rightTail
            return result;
        }
        if(n==dummy2){
            result[0]=dummy1.next;//leftHead
            result[1]=m;//leftTail
            result[2]=tail;//pivot
            result[3]=tail;//rightHead
            result[4]=tail;//rightTail
            return result;
        }
        result[0]=dummy1.next;//leftHead
        result[1]=m;//leftTail
        result[2]=tail;//pivot
        result[3]=dummy2.next;//rightHead
        result[4]=n;//rightTail

        return result;
    }

    private ListNode findTail(ListNode head){
        ListNode cur=head;
        while(cur.next!=null){
            cur=cur.next;
        }
        return cur;
    }
}
//写了一下午终于pass了。。撒花！个人对于直接一个ListNode数组不是太满意，然后特别要注意左边尾节点或者右边头节点和pivot节点重合的情况，这种情况下
//是不需要link的，感觉终于对recursion有了一点点体会。。

```
