# Ransom Note
Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

#### Example
```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

### Python 3
```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        magazineCount = Counter(magazine)
        ransomNoteCount = Counter(ransomNote)
        
        for c in ransomNoteCount:
            if c not in ransomNoteCount or magazineCount[c] < ransomNoteCount[c]:
                return False
            
        return True
```
[code](Python%203/383.py)

#### Result
```
Runtime: 48 ms, faster than 75.50% of Python3 online submissions for Ransom Note.
Memory Usage: 14 MB, less than 25.00% of Python3 online submissions for Ransom Note.
```

### C
```C
int cmp(const void *a, const void *b)
{
    return *(const char*)a - *(const char*)b;
}

bool canConstruct(char * ransomNote, char * magazine){
    int ransomNoteSize = strlen(ransomNote);
    int magazineSize = strlen(magazine);
    int i = 0, j = 0;
    
    qsort(ransomNote, ransomNoteSize, sizeof(char), cmp);
    qsort(magazine, magazineSize, sizeof(char), cmp);
    
    while((i != ransomNoteSize)&&(j != magazineSize))
    {
        if(ransomNote[i] == magazine[j])
        {
            i++;
            j++;
        }
        else if(ransomNote[i] < magazine[j])
            return false;
        else
            j++;
    }
    
    return i == ransomNoteSize;
}
```
[code](C/383.c)

#### Result
```
Runtime: 40 ms, faster than 23.33% of C online submissions for Ransom Note.
Memory Usage: 6.7 MB, less than 100.00% of C online submissions for Ransom Note.
```
