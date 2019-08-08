# Description:
There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

# Example:
nums1 = [1, 3]
nums2 = [2]

The median is 2.0

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5

# Solution
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m=nums1.length;
        int n=nums2.length;
        
        double result=0.0;
       
        if(m<=n){
            result=helper(nums1,nums2);
        }else{
            result=helper(nums2,nums1);
        }
        return result;
    }
    
    private double helper(int[] nums1, int[] nums2){
        int lo=0;
        int high=nums1.length;
        while(lo<=high){
            int mid1=lo+(high-lo)/2;
            int mid2=(nums1.length+nums2.length+1)/2-mid1;
            
            int left1_max=mid1==0?Integer.MIN_VALUE:nums1[mid1-1];
            int right1_min= mid1==nums1.length?Integer.MAX_VALUE:nums1[mid1];
            
            int left2_max= mid2==0?Integer.MIN_VALUE:nums2[mid2-1];
            int right2_min= mid2==nums2.length? Integer.MAX_VALUE:nums2[mid2];
            
            if(left1_max<=right2_min&&left2_max<=right1_min){
                if((nums1.length+nums2.length)%2==1){
                    return Math.max(left1_max,left2_max);
                }else{
                    return (Math.max(left1_max,left2_max)+Math.min(right1_min,right2_min))/2.0;
                }
            }else if(left1_max>right2_min){
                high=mid1-1;
            }else{
                lo=mid1+1;
            }
        }
        return 0.0;
        
    }
}
//Always find the mid of the combined array, and remember to do binary search on the smaller one. Boundary condition is very hard to 
//figure out here.
```
