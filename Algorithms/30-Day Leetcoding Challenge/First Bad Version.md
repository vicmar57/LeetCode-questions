## First Bad Version
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example:**
```
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
```

##Java Solution
```Java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int right = n;
        int left = 1;
        int mid = 1;
        
        while(left < right)
        {
            mid = left + (right-left)/2;
            if(isBadVersion(mid)) // bad version
                right = mid;
            else // good version
                left = mid + 1;
            //System.out.println("r: " + right + ", m: " + mid + ", l: " + left);
        }
        
        return right;
    }
}
```

**Complexity Analysis::**
* Time: O(logn) - binary search
* Space: O(1) - three int variables