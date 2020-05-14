## Single Element in a Sorted Array
You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once. Find this single element that appears only once.

**Example 1:**
```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```
**Example 2:**
```
Input: [3,3,7,7,10,11,11]
Output: 10
```

**Note: Your solution should run in O(log n) time and O(1) space.**

## Java Solution
```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        if(nums == null || nums.length == 0)
            throw new IllegalArgumentException("Can't handle zero-length arrays.");
        
        for(int i=0, j=1; i < nums.length-1; i+=2) {
            if(nums[i] != nums[j]) {
                return nums[i];
            }
            j+=2;
        }
        return nums[nums.length-1];
    }
}
```

**Complexity Analysis::**
* Time: O(log(n)) - checking pairs only
* Space: O(1)