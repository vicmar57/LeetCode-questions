##Ransom Note

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

Note:
You may assume that both strings contain only lowercase letters.
```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

##Java Solution
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap <Character, Integer> charCntMap = new HashMap <>();
        for (Character c : magazine.toCharArray()) {
            charCntMap.put(c, charCntMap.getOrDefault(c,0) + 1);
        }
        
        for (Character c : ransomNote.toCharArray()) {
            if (charCntMap.containsKey(c)) {
                int charCnt = charCntMap.get(c);
                if(charCnt > 0) {
                    charCntMap.put(c, charCnt - 1);
                } else {
                    return false;
                }
            } else {
                return false;
            }
        }
        return true;
    }
}
```

**Complexity Analysis::**
* Time: O(n) - where n is the length of the longest string
* Space: O(n) - for the hashmap