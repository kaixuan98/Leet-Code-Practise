### 21. Merge Two Sorted Lists

#### Method :Intitive Method 
We can have one pointer each for `list1` and `list2`. Then we can keep looping both list until one of them reach null, while moving, check which pointer have a smaller value. The smaller value will be appended to a brand new mergedList. 

#### Things to take care 
1. One of the empty list. Remember to first check if anyone of the list is empty then we can just return the other list 
2. Having two pointers for the result. If we keep moving the head, we will never be able to return the result


```
var mergeTwoLists = function(list1, list2) {
    
    let pointerL1 = list1; 
    let pointerL2 = list2; 
    let resultHead = null; // keep maintaing the start of the result
    
    
    if(!pointerL1){
        return list2; 
    }else if(!pointerL2){
        return list1;
    }
    
    // first item in the result list
    if(pointerL1.val <= pointerL2.val){
        resultHead = pointerL1;
        pointerL1 = pointerL1.next;
    }else{
        resultHead = pointerL2;
        pointerL2 = pointerL2.next; 
    }
    
    let resultCurr = resultHead; 
  
    // after the first item 
    while(pointerL1 && pointerL2){
      if(pointerL1.val <= pointerL2.val){
            resultCurr.next = pointerL1;
            pointerL1 = pointerL1.next; 
        }else{
            resultCurr.next = pointerL2;
            pointerL2 = pointerL2.next; 
        }
        resultCurr = resultCurr.next;
    }
    
     // the remainder of the longer linked list
    
    if(pointerL1 !== null){
        resultCurr.next = pointerL1;
    }
    
    if(pointerL2 !== null){
        resultCurr.next = pointerL2;
    }
    
    
    
    return resultHead;
};
```

#### Time Complexity 
O(n)

#### Space Complexity 
O(n+m) 
n = length of list 1 
m = length of list 2