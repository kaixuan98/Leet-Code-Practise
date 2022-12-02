### 242. Valid Anagram

The property of anagram is that even jumble up, they are still the same word. 
- we can sort the jumble up word and compare with the original (method 1)
- we can count the occurance of both word. If both words has the same character occurances then it is an anagram (method 2)

Both method takes extra spaces. But there are difference in the time complexity
Method 1: depends on the sorting algorithm. The worst case of a good linear sorting algorithm is O(n log n). 
Method 2: Even with two for loop. The for loop are not nested and we check the same length. So the worst case is O(n). 


#### Method 1: Sorting

```
 var isAnagram = function(s, t) {
      var sArr = [];
      var tArr = [];
    
     if(s.length !== t.length) {
         return false;
     }else{
         sArr = s.split("");
         tArr = t.split("");

         sArr = sArr.sort();
         tArr = tArr.sort();

         for( let i = 0; i < sArr.length; i++) {
             if(sArr[i] !== tArr[i]){
                 return false;
             }
         }  
         return true;
     }
    
 };

```

#### Method 2: Hashing 

```
 var isAnagram = function(s, t) {
     var charFrequency = new Map();
     
     if (s.length !== t.length) return false; 
     
     // setting up the frequency hashmap
     for(let i=0; i< s.length; i++){
         if(charFrequency.has(s[i])){
             charFrequency.set(s[i], charFrequency.get(s[i]) + 1 );
         }else{
             charFrequency.set(s[i], 1 );
         }
     }
     
     for(let j = 0; j< t.length; j++){
         if(charFrequency.has(t[j])){
             charFrequency.set(t[j], charFrequency.get(t[j]) - 1 );
         }else{
             return false;
         }
     }
     
     // getting all the keys 
     var keys = charFrequency.keys();
     
     for (let key of keys){
         if(charFrequency.get(key) !== 0 ){
             return false;
         }
     }
     
     return true;
 }
```