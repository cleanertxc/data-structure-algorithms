# Description
Given two integer arrays A1 and A2, sort A1 in such a way that the relative order among the elements will be same as those are in A2.

For the elements that are not in A2, append them in the right end of the A1 in an ascending order.

# Assumptions
A1 and A2 are both not null.
There are no duplicate elements in A2.

# Examples
A1 = {2, 1, 2, 5, 7, 1, 9, 3}, A2 = {2, 1, 3}, A1 is sorted to {2, 2, 1, 1, 3, 5, 7, 9}

# Solution
```java
public class Solution {

  public int[] quickSort(int[] array) {
    // Write your solution here
    if(array==null&&array.length==0){
      return array;
    }
    quickSort(array,0,array.length-1);
    return array;
  }
  private void quickSort(int[] array, int left, int right){
    if(left>=right){
      return;
    }
    int pivot=partition(array,left,right);
    quickSort(array,left,pivot-1);
    quickSort(array,pivot+1,right);
  }
  
  private int partition(int[] array, int left,int right){
    int pivot=right;
    int i=left;
    int j=right-1;
    while(i<=j){
    if(array[i]<array[pivot]){
      i++;
    }else if(array[j]>=array[pivot]){
      j--;
    }else{
      swap(array,i,j);
      i++;
      j--;
    }
    }
    swap(array,i,pivot);
    return i;
  }
  
  private void swap(int[] array, int a,int b){
    int temp=array[a];
    array[a]=array[b];
    array[b]=temp;
  }

  public int[] sortSpecial(int[] A1, int[] A2) {
    // Write your solution here

    int[] temp=new int[A1.length];
    //不要直接int[] temp=quickSort(A1),否则temp和A1指向同一个地址；
    for(int i=0;i<A1.length;i++){
      temp[i]=A1[i];
    }
    temp=quickSort(temp);
    int[] mark=new int[A1.length];
    int count=0;
    for(int i=0;i<A1.length;i++){
      mark[i]=0;
    }
    if(A2.length==0){
      return temp;
    }
    for(int i=0;i<A2.length;i++){
      int j;
      for(j=0;j<temp.length;j++){
        if(temp[j]==A2[i]){
          break;
        }
      }
      for(int k=j;k<temp.length;k++){
        if(temp[k]==A2[i]){
          A1[count++]=temp[k];
          mark[k]=1;
        }
      }
    }

    for(int m=0;m<temp.length;m++){
      if(mark[m]==0){
        A1[count++]=temp[m];
      }
    }
    return A1;
  }
}
```
