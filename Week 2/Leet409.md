###  409. Longest Palindrome

#### Method: HashTable + Greedy Algo
---
A palindrome is a string that read the same after reversing it. The goal of the question is to find the maximum length of palindrome from a given string. 

###### Greedy Algo
Since we are finding the maximum length , it is an optimizing problem. We can use greedy algo. As we move forward in the string, we need to decided whether we are able to build a palindrome from what I see and get the maximum length. 

```
For example: "aabbaa"
1. a -> yes I can make palindrome -> max Length = 1
2. aa -> yes I can make palindrome -> max length = 2 
3. aab -> yes I can make palindrome but need arrangement (aba) -> max length = 3
4. aabb -> yes I can but need arrangement (baab) -> maxLength = 4 
5. ...
   
Keep going until we reach the end of the string 


```
###### Hashing 
We can use hashing to group the character that we see. This help us to know are we able to get the next coming character to build our palindrome

The following show some of the palindrom patterns. There are odd and even. 

Example: odd length palindrome 
   - **valid** : "cac"(3), "aabaa" (5), "aabcbaa" (7) , "ccc"(3)
   - **not valid**: "abc"(3), "abcde" (5)

Example: even length palindrome
   - **valid** : "aa" (2) , "baab" (4)
   - **not valid** : "ab" (2), "aabb" (4)

If it is even, we can be greedy and take whatever that comes next. 

If it is odd, we cannot be greedy and be precises on what we are grabbing.
   - next is even : be greedy and add to my max values
   - next is odd: we can take portion of it (even portion)

#### Solution
```
var longestPalindrome = function(s) {
    // hash the string 
    let hashTable = new Map(); 
    let maxLength = 0; 

    for(let i= 0; i < s.length; i++){
        if(hashTable.has(s[i])){
            hashTable.set(s[i], hashTable.get(s[i]) + 1 );
        }else{
            hashTable.set(s[i], 1);
        }
    }
    
    // if we are odd, can only take event number 
    for(let val of hashTable.values()){
        if(maxLength % 2 != 0){  // odd
            if(val % 2 === 0){
                maxLength += val;
            }else{ // next value is odd : I can take val -1 of it
                maxLength += val - 1; 
            }
        }else{
            maxLength += val; // take anything
        }
    }

    return maxLength;
};
```