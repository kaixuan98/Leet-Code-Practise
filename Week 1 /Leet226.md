### 226. Invert Binary Tree

#### Method : Recursion!! 

```
    var invertTree = function(root) {
    
        if(root === null){
            return root;
        }
        
        // telling my left substree and right substree to invert
        invertTree(root.left);
        invertTree(root.right);
        
        // after the invert, its time for me to swap two of my children
        var temp = root.left;
        root.left = root.right; 
        root.right = temp; 
        
        // done swapping, will return myself
        return root; 
    
    };
```