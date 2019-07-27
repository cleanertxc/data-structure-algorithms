# Description
Given an array of elements, reorder it as follow:

- { N1, N2, N3, …, N2k } → { N1, Nk+1, N2, Nk+2, N3, Nk+3, … , Nk, N2k }

- { N1, N2, N3, …, N2k+1 } → { N1, Nk+1, N2, Nk+2, N3, Nk+3, … , Nk, N2k, N2k+1 }

Try to do it in place.

# Assumptions
- The given array is not null

# Examples
- { 1, 2, 3, 4, 5, 6} → { 1, 4, 2, 5, 3, 6 }

- { 1, 2, 3, 4, 5, 6, 7, 8 } → { 1, 5, 2, 6, 3, 7, 4, 8 }

- { 1, 2, 3, 4, 5, 6, 7 } → { 1, 4, 2, 5, 3, 6, 7 }

# Solution
```java
public class Solution {
  public int[] reorder(int[] array) {
    // Write your solution here
    if(array.length<=3){
      return array;
    }
    if(array.length%2==0){
      reorder(array,1,array.length-2);
    }
    if(array.length%2==1){
      reorder(array,1,array.length-3);
    }
    return array;
  }
  private void reorder(int[] array,int left,int right){
    while(left>=right){
      return;
    }
    int mid=left+(right-left)/2+1;
    for(int i=mid;i<=right;i++){
      swap(array,i,i-(right-left+1)/2);
    }
    reorder(array,left+1,right-1);
  }

  private void swap(int[] array, int i,int j){
    int temp=array[i];
    array[i]=array[j];
    array[j]=temp;
  }
}
//the idea is really hard to come up with!!
```
