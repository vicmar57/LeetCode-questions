## Last Stone Weight

We have a collection of stones, each stone has a positive integer weight.

Each turn, we choose the two heaviest stones and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:

If x == y, both stones are totally destroyed;
If x != y, the stone of weight x is totally destroyed, and the stone of weight y has new weight y-x.
At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)

**Example 1:**
```
Input: [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of last stone.
```

### Note:
```
1 <= stones.length <= 30
1 <= stones[i] <= 1000
```

## Java Solution
```
class Solution {
    public int lastStoneWeight(int[] stones) {
        if (stones == null || stones.length == 0) return -1;
        if (stones.length ==  1) return stones[0];
        
        Queue <Integer> maxHeap = new PriorityQueue <>((n1, n2) -> n2 - n1);
        for (int num : stones) {
            maxHeap.add(num);
        }
        
        while(maxHeap.size() > 1) { //x <= y
            int y = maxHeap.poll();
            int x = maxHeap.poll();
            
            if(x < y)
                maxHeap.add(y-x);
        }
        
        if(maxHeap.size() == 0) return 0;
        return maxHeap.poll();
        
    }
}
```

** Complexity analysis: **
* Time : total O(nlogn) - O(n) for maxHeap construction and O(nlogn) for removing and adding to heap.
* Space : O(n) for maxHeap

