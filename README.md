# Crack-the-Interview
Starting my preparation for coding interview : So let's first dig into data structure algorithm.
Goal : One algorithm per day at minimum, starting the seventh of november 2021 !
Always aim for O(log(n)) complexity algorithm.

---
### Binary Search : 
Given an ordenated array and a target number, give back the index of the target value inside the array, if it doesn't exist return -1. 
```javascript
const search = (nums, target) => {
    let left = 0, right = nums.length - 1;
    
    while (left <= right) {
        let mid = (left + (right-left) / 2) | 0; 
        /* Can use Math.round((left + right) / 2) instead of | 0, same thing
           Better to use left + (right-left)/2 than (right+left)/2
           Because integer limite size, can block sometimes */
        if (nums[mid] === target) { return mid; }
        if (nums[mid] > target) { right = mid - 1; }
        else { left = mid + 1; }
    }
    
    return -1;
};
``` 
**Conclusion** : Instanciate two pointers, left and right, and at each iteration check the midle of the array by adjusting right or left. 
Don't forget to use round number with JS;

---
### First Bad Version : 

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which returns whether version is bad
```javascript
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        
        let left = 1;
        let right = n;

        while (left<=right) {
            let middle = Math.round(left + (right-left) / 2);
            if (isBadVersion(middle) && (!isBadVersion(middle-1))) {
               return midle; 
            }
            if (isBadVersion(middle)) {
                right = midle - 1;
            }
            else { 
                left = middle + 1;
            }
        }
    };
};
``` 
**Conclusion** : Same logic as above 

---
### Search Insert Position :

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

```javascript
var searchInsert = function(nums, target) {
    let left = 0;
    let right = nums.length - 1;
    
    if (target > nums[right]) {
        return right +1;
    }
    
    if (target<nums[left]) {
        return left;
    }
    
    while (left <= right) {
        let middle = Math.round(left + (right - left) / 2);
        if (nums[middle] == target) {
            return middle;
        }
        if (nums[middle] > target && nums[middle-1] < target) {
            return middle;
        }
        if (nums[middle] < target && nums[middle+1] > target) {
            return middle + 1;
        }
        if (nums[middle] > target) {
            right = middle - 1;
        }
        else {
            left = middle + 1; 
        }
    }
};
``` 
**Conclusion** : Same logic as above
---



