### 121. Best Time to Buy and Sell Stock


#### Method 1: Brute Forces
---
We can use a double for loop which we have one pointer point at one value and that will be our current buy price. A second pointer will go out there and find a value that can give a max profit. This case is not idea if we have a huge array to check because the time complexity will be `O(n^2)`.

```
    var maxProfit = function(prices) {
        let maxProfit = 0 ; 
        for(let i = 0 ; i < prices.length; i++){
            for(let j = i + 1; j < prices.length; j++){
                if(prices[j] - prices[i] > maxProfit){
                    maxProfit = prices[j] - prices[i]; 
                }
            }
        }
        
        return maxProfit;
    };

```


#### Method 2: Go through only once! 
---
In method 1, we always compare again when we have a new i (new buy value). If we have a method to always keep the buy price low then we dont need to always go out and find one value that can give a max profit. 

```
    Example: 

    Iterate i = 0 ; [7] itertate j : [1,5,3,6,4]
    Iterate i = 1 : [1] iterate  j : [5,3,6,4]
    Iterate 1 = 2 : [5] iterate  j : [3,6,4]
    Iterate 1 = 3 : [3] iterate  j : [6,4]
    ...
```
To lower down the time complexity, we can only loop through the prices once. As we are looping the prices, we are allow to do two action 
1. buy when low 
   - we only buy when we see a price that is lower than what we currently have
2. sell when max profit 
   - if we are not buying then we need to check the sell price, so we alwasys got the high profit. 

This will keep the time complexity to `O(n)`

```
var maxProfit = function(prices) {
    
    var buy = prices[0]; 
    var max_profit = 0 ; 

    for (let i = 1; i< prices.length; i++){
        if (prices[i] < buy){
            buy = prices[i];
        }else if (prices[i] - buy > max_profit){
            max_profit = prices[i] - buy;
        }
    }

    return max_profit;
};
```


