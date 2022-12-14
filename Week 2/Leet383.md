### 383. Ransom Note

#### Method 1: Brute Force
---
We can use a double for loop to check the validity of the randsom note. The outer for loop is to keep track of which character we are in the ransom note. The second for loop is to find the matching character in the magazine. This method take O(n^2) time. We can reduce the time by having a constant access of the letter in magazine. This lead to method 2. 

#### Method 2: Hashing 
---
In order to have a constant time access of letter in magazine. We need to hash the magazine characters with key = letter and value = no of occurances. 

Intuition: 
1. hash the magazine with key = letter seen and value = no of occurance
2. loop the ransom notes
   a. if the hashing has the character && the value is > 0 : then reduce the value of that key 
   b. if not then return false

Additional corner case that we can handle without map
1. if the ransom notes is longer than the magazine, just return false

Solution 
```
var canConstruct = function(ransomNote, magazine) {
    
    var hashedMagazine = new Map();
    
    if(ransomNote.length > magazine.length) return false;
    
    // create the hashmap 
    for (let i=0; i<magazine.length; i++){
        if(!hashedMagazine.has(magazine[i])) { // no key
            hashedMagazine.set(magazine[i], 1); // add key and add value
        }else{
            hashedMagazine.set(magazine[i], hashedMagazine.get(magazine[i])+1); // add 1 to that key
        }
    }
    
    // iterate the ransomNote 
    for (let j=0; j< ransomNote.length; j++ ){
        if(hashedMagazine.has(ransomNote[j])) {
            if(hashedMagazine.get(ransomNote[j]) !== 0){
                hashedMagazine.set(ransomNote[j], hashedMagazine.get(ransomNote[j])-1)
            }else {
                return false;
            }
        }else{
            return false;   
        }
    }
    
    return true;
    
};
```