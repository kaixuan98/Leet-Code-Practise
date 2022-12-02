### 125. Valid Palindrome

#### Phase 1: Cleaning the string 
A string can have non-alphanumeric characters like punctuation. We need to clean that by replacing those letter to blank. Using regax to do that

#### Phase 2: Check Palindrome 
Always check for palindrome after cleaning not before. If there is a case with `","` then this will still be true but not in the way its defined palindrome definition. 

##### Method 1: 2 pointer at front and back 
PS. remember to move the pointers

```
    var isPalindrome = function(s) {
    
    let cleanStr = "";
    
    cleanStr = s.replace(/[\W_\s\n]+/g, "").toLowerCase();
    
    if(cleanStr.length === 0){
        return true; 
    }
    
    let left = 0; 
    let right = cleanStr.length-1; 
    
    while(left < right){
        if(cleanStr[left] !== cleanStr[right]){
            return false;
        }
        left ++; 
        right --;
    }
    return true;

};

```

##### Method 2: Reverse and check 


```
var isPalindrome = function(s) {
    
    var str = "";
    var reverseStr = "";
    
    str = s.replace(/[\W_\s\n]+/g, "");
    str = str.toLowerCase();
    
    if (str.length < 0 ) return false;
    
    for(let i=(str.length) -1 ; i >= 0 ; i--){
        reverseStr += str[i];
    }
    if(reverseStr === str) return true;
    
    return false;
    
    
};
```