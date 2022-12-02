### 20. Valid Parentheses

#### Example cases that allowed 
1. Nested brackets that has proper closing : {()} , [[]]
2. Seperated Brackets that has proper closing : []{}()
3. Single Brackets that has proper closing: {}, (), []

#### Example cases that not allowed
1. Start with a closing : )( , }{}, ][()]
2. The length less or equals to 1: (, )
3. Only open no close: (( , {{{ . [[[[
4. The closing does not match: (] 

#### Method: use a stack
```
var isValid = function(s){

    let stack = [];

    if(s.length <= 1){
        return false; 
    }

    for(let i = 0 ; i < s.length; i++){
        if(s[i] === "(" || s[i] === "[" || s[i] === "{"){
            stack.push(s[i]);
        }else{
            if(stack.length === 0) return false;
            let top = stack.pop(); 
            if( top === "(" && s[i] !== ")" ||top === "{" && s[i] !== "}" || top === "[" && s[i] !== "]" ){
                return false; 
            }
        }
    }

    return (stack.length <= 0 ); 



}
```

##### Time Complexity 
O(n)

##### Space Complexity 
O(n)
