## Find All Anagrams in a String

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.
Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.
The order of output does not matter.

**Example 1:**
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## My Java solution
```Java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new LinkedList <>();
        if(s == null || p == null || s.length() == 0 || p.length() == 0 || p.length() > s.length())
            return res;
        HashMap <Character, Integer> hist = new HashMap <>();
        for(Character c: p.toCharArray()) {
            hist.put(c, hist.getOrDefault(c,0) +1);
        }
        
        //System.out.print("hist:");
        //hist.entrySet().forEach(entry->{
        //    System.out.print(entry.getKey() + " -> " + entry.getValue() + ", ");  
        // });
        
        int i;
        for(i = 0; i < p.length(); i++) {
            Character c = s.charAt(i);
            hist.put(c, hist.getOrDefault(c,0) -1);
            
            if(hist.getOrDefault(c,0) == 0)
                hist.remove(c);
        }
        
        //System.out.println();
        //System.out.print("hist:");
        //hist.entrySet().forEach(entry->{
        //    System.out.print(entry.getKey() + " -> " + entry.getValue() + ", ");  
        // });
        //System.out.println();
        
        if(hist.isEmpty())
            res.add(0);
        
        int pLen = p.length();
        for( ; i < s.length(); i++) {
            Character toRem = s.charAt(i-pLen);
            Character toAdd = s.charAt(i);
            
            hist.put(toAdd, hist.getOrDefault(toAdd,0) -1);
            hist.put(toRem, hist.getOrDefault(toRem,0) +1);
            
            if(hist.getOrDefault(toRem, -1) == 0)
                hist.remove(toRem);
            if(hist.getOrDefault(toAdd, -1) == 0)
                hist.remove(toAdd);
            
            //System.out.print("hist:");
            //hist.entrySet().forEach(entry->{
            //    System.out.print(entry.getKey() + " -> " + entry.getValue() + ", ");  
            // });
            //System.out.println();

            if(hist.isEmpty())
                res.add(i-pLen+1);
        }
        
        return res;
    }
}
```

**Complexity Analysis::**
* Time: O(s) - for iterating over all of s and p
* Space: O(s) - for the hashmap


## Better solution
```Java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        int[] map = new int[26];
        List<Integer> result = new ArrayList<>();
        
        for(int i=0;i<p.length();i++){
            map[p.charAt(i) - 'a']++;
        }
    
        int windowStart = 0;
        int windowEnd = 0;
        while(windowEnd<s.length()){
		// valid anagram
            if(map[s.charAt(windowEnd) - 'a'] > 0){
                map[s.charAt(windowEnd++) - 'a']--;
			// window size equal to size of P
                if(windowEnd-windowStart ==  p.length()){                    
                    result.add(windowStart);
                }
            }
			// window is of size 0
            else if(windowStart == windowEnd){
                windowStart ++;
                windowEnd ++;
            }
			// decrease window size
            else{
                map[s.charAt(windowStart++) - 'a']++;
            }      
        }
        return result;
    }
}
```

**Credit to Shradha1994's solution on https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/636988/Sliding-Window-or-HashTable-or-Java-Explained-with-Diagram-Beats-99**

**Complexity Analysis::**
* Time: O(s) - for iterating over all of s and p
* Space: O(1) - few int variables, and constant-size array (map)