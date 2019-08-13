# Description
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

# Solution
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int rec=-1;
        if(nums.length==1){
            return;
        }
        for(int i=nums.length-1;i>=1;i--){
            if(nums[i]>nums[i-1]){
                rec=i-1;
                break;
            }
        }
        if(rec==-1){
            reverse(nums,0,nums.length-1);
            return;
        }
        int j=rec+1;
        int mark=j;
        int secondLarge=nums[j];
        j++;
        while(j<nums.length){
            if(secondLarge>=nums[j]&&nums[j]>nums[rec]){
                secondLarge=nums[j];
                mark=j;
            }
            j++;
        }
        swap(nums,rec,mark);
        reverse(nums,rec+1,nums.length-1);
    }
    
    private void reverse(int[] nums,int start,int end){
        int i=start;
        int j=end;
        while(i<j){
            swap(nums,i,j);
            i++;
            j--;
        }
    }
    
    private void swap(int[] nums,int i,int j){
        int tmp=nums[i];
        nums[i]=nums[j];
        nums[j]=tmp;
    }
}
//find the first descending pair from right, and replace the smaller one with the secondLarge number in the right, then reverse the right
```java
