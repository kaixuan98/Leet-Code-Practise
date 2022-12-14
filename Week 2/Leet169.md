### 169. Majority Element

#### Method 1: Hashing
---
Intuition 
1. find the maj boundary 
2. hash the element in nums with key = value and value = occurance 
3. loop the key and find the occurance that is higher than maj bound and current max 

```
var majorityElement = function(nums) {
    // first to find the boudary for majority
    let majBound = Math.floor(nums.length / 2) 
    let hashTable = new Map();
    let currMaxValue = 0; 

    for(let i = 0 ; i < nums.length; i++){
        if(hashTable.has(nums[i])){
            hashTable.set(nums[i], hashTable.get(nums[i]) + 1 )
        }else{
            hashTable.set(nums[i], 1 )
        }
    } 

    for(key of hashTable.keys()){
        if(hashTable.get(key) > majBound){
            if(hashTable.get(key) > currMaxValue){
                currMaxValue = key;
            }
        }
    }

    return currMaxValue; 

};
```
#### Method 2 
---