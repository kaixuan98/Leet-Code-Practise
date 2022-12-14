### 70. Climbing Stairs

#### Method 1: Brute Force - Recursion
---
We can use recursion to solve this problem. However, this solution takes O(2^N) time to solve which is exponential. We would need to look at the following example and try to write out the intuition.

Example: n = 3
There are 3 ways to get `n = 3`
1. 1+1+1
2. 2+1
3. 1+2

When we need to climb 3 steps. We can either goes 1 steps or 2 steps. We can imagine the relation as a tree. 
Go left -> one step
Go right -> two steps
```
        3               // we need to do 3 steps
       / \
      2   1             // the steps left after taking 1 or 2 steps
     / \ /              // path that ends with 0 is the possible ways
    1  0 0 
   /
  0                     
```

Intuition
1. When `n <= 1`, that means we reach till the end of where we can definitely say that "we only have 1 or 0 step left so we are done and I am a path"
   a. the base case is when `n = 1`, there is only one way to get 1
   b. when `n=0`, then we need to stop and return 1. We will reach this case when we take 2 steps.
2. then we can recurse both `n-1` steps and `n-2` steps


<br/>
Solution
```
var climbStairs = function(n){
    if(n < = 1 ){
        return 1;
    }

    return climbStairs(n-1) + climbStairs(n-2);
}
```

#### Method 2 : Dynamic Programming 
---
We can perform dynamic programming in the method 1 to optimize the solution. The time complexity will be O(n).

Dynamic Programming is having a data stuct to memorize the solution that we did. From method 1 example, we can see that there are overlapping solution when we have left 1 steps. Imagine if our N gets bigger (n=5), we would need to repeat (n=3) a few times in our recursion. Memoization comes in and solve the problem. If we see the problem before, we can just get it from our memo and then return that. 

```
var climbStairs = function(n){
    let memo = []; 

    var memoizeClimb = function(n){
        if(n <=1){
            return 1;
        }
        if(memo[n] != null){
            return memo[n];
        }
        return memo[n] = memoizeClimb(n-1) + memoizeClimb(n-2);
    }
    return memoizeClimb(n);
}
```