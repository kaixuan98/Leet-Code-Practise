### 1. Two Sum 

#### Method 1: Brute Force 
---
We can think of a two pointer solution, we have one pointer fixed at one of the element and the second pointer will go out and keep adding that pointing value untill we found our target. 

Time complexity = O(n^2)
Space = no extra space 

```
var twoSums = function(nums, target){

    let pair = [];

    for(let i = 0; i< nums.length; i++){
        for(let j = i + 1; j < nums ; j++){
            if(nums[i] + nums[j] === target){
                pair.push(i);
                pair.push(j);
            }
        }
    }
}
```

#### Method 2: Using Maps 
---
In method 1, the reason that causing the time complexity is we need to nest another for loop to find out which one will be add up to form our target. If we are able to overcome that with contant time access, then we can have a linear time solution. 

Since we know the target, and we will keep track of what we are seeing right now. We can use the target to subtract what we are seeing right now, so we know what we gonna look for the next half. 

We will use a hashmap with element as key and index as value. Then we can find it quick! 

Example: 
```nums = [2, 7, 9 , 11] 
target = 9 
9 - 2 = 7 
{
    2: 0, 
    7: 1,
    9: 2,
    11: 3
}
```

```
var twoSums = function(nums, target){

    let hashedMap = new Map();
    let pair = [];

    for ( let i = 0; i< nums.length; i++){
        hashedMap.set(nums[i], i);
    }

    for(let j = 0; j< nums.length; j++){
        let diff = target - nums[j];
        if(hashedMap.has(diff) && j !== hashedMap.get(diff)  ){
            pair.push(j);
            pair.push(hashedMap.get(diff));
            return pair;
        }
    }
}
```
