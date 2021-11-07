# Crack-the-Interview
Starting my preparation for coding interview : So let's dig in data structure algorithm.
Goal : 1 algorithm per day at minimum !


Binary Search : Given an ordenated array and a target number, give back the index of the target value inside the array, if it doesn't exist return -1. 
```javascript
const search = (nums, target) => {
    let left = 0, right = nums.length - 1;
    
    while (left <= right) {
        let mid = (left + right) / 2 | 0;
        
        if (nums[mid] === target) { return mid; }
        if (nums[mid] > target) { right = mid - 1; }
        else { left = mid + 1; }
    }
    
    return -1;
};
```

Instanciate two pointers, left and right, and at each iteration check the midle of the array by adjusting right or left. 
