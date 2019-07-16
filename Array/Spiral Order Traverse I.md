# Description
Traverse an N * N 2D array in spiral order clock-wise starting from the top left corner. Return the list of traversal sequence.

# Assumptions
The 2D array is not null and has size of N * N where N >= 0

# Examples

{ {1,  2,  3},

  {4,  5,  6},

  {7,  8,  9} }

the traversal sequence is [1, 2, 3, 6, 9, 8, 7, 4, 5]

# Solution
```java
public class Solution {
  public List<Integer> spiral(int[][] matrix) {
    // Write your solution here
    List<Integer> result=new ArrayList<Integer>();
    if(matrix.length==0){
      return result;
    }
    spiralTraverse(matrix,0,matrix[0].length-1,0,matrix.length-1,result);
    return result;
  }

  private void spiralTraverse(int[][] matrix,int left,int right,int top,int bottom,List<Integer>result){
    //i is row and j is column.
    if(left==right){
      for(int i=top;i<=bottom;i++){
        result.add(matrix[i][left]);
      }
      return;
    }
    if(top==bottom){
      for(int j=left;j<=right;j++){
        result.add(matrix[top][j]);
      }
      return;
    }

    for(int j=left;j<right;j++){
      result.add(matrix[top][j]);
    }
    for(int i=top;i<bottom;i++){
      result.add(matrix[i][right]);
    }
    for(int j=right;j>left;j--){
      result.add(matrix[bottom][j]);
    }
    for(int i=bottom;i>top;i--){
      result.add(matrix[i][left]);
    }
    if(left+1<right&&top+1<bottom){
      spiralTraverse(matrix,left+1,right-1,top+1,bottom-1,result);
    }
  }
}
//注意分析只有一行或者一列的情况下的base case！
```
