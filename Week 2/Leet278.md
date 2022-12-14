### 278. First Bad Version

#### Method 1: Brute Force
---
We can use the version to find the first bad version. This will give us `n` calls but we are trying to optimise the number of API calls to check for bad versions. The reason it takes `n` calls is because the possible bad version can at the end of the list. 

#### Method 2: Binary Search 
---
One of the method to reduce the search time is using Binary search which is divide and conquer method approach. Each time we reduce the array size by half. 

The intuition: 
1. start at the middle of the version. 
2. check the middle version 
    a. middle is bad: move to the left because the middle might not be the first case
    b. middle is good: move to the right because the bad one can only be bigger than the middle
3. So we need a way to stop it!! 
    a. If the `start > end` then we left with no element, we just gonna return the start element. 

The time complexity at worst case is O(lg n). 

Solution: 
```
// assume that isBadVersion(element) is a given function 

function helper(start ,end){

    if(start > end ){
        return start;
    }else{
        let mid = Math.floor((start + end) / 2);

        if(isBadVersion(mid)){
            return helper(start, mid - 1);
        }else{
            return helper(mid + 1, end);
        }
    }
}

function findBad(n){
    return helper(1,n);
}

```