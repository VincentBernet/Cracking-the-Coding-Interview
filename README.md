# Crack-the-Interview
Starting my preparation for coding interview : So let's first dig into data structure algorithm.
Goal : One algorithm per day at minimum, starting the seventh of november 2021 !
Always aim for O(log(n)) complexity algorithm.

---

### Binary Search (Difficulty -> Easy) : Day One
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

### First Bad Version (Difficulty -> Easy) : Day Two

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

### Search Insert Position (Difficulty -> Easy) : Day Three

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

### Squares of a Sorted Array (Difficulty -> Easy) : Day Three

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

```javascript
var sortedSquares = function(nums) {
    let numsBySquare = [];
    let left = 0;
    let right = nums.length - 1;
    let i = nums.length-1;
    
    while (left <= right) {
        if (nums[left] * nums[left] >= nums[right] * nums[right]) {
            numsBySquare[i] = nums[left] * nums[left];
            left += 1;
        }
        else {
            numsBySquare[i] = nums[right] * nums[right];
            right -= 1;
        }
        i --;
    }
    return numsBySquare;
};
``` 
**Conclusion** : Same logic as above

---

---

### Rotate Array (Difficulty -> Medium) : Day Three

Given an array, rotate the array to the right by k steps, where k is non-negative.

```javascript
var rotate = function(nums, k) {
    
    // array.push(); créer une nouvelle value à la fin d'un array
    // array.unshift(); créer une nouvelle value au début d'un array
    // array.shift(); supprime la première value d'un array
    // array.pop(); supprime la dernière value d'un array
        
    /* Bonne idée, mais trop lents, complexity of O(n)
        let right = nums.length - 1;
        for (i=0;i<k;i++) {
            nums.unshift(nums[right]);
            nums.pop();
        } 
    */
    
    k %= nums.length;
    console.log(k);
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
};

const reverse = (nums, from, to) => {
    for (let i = from, j = to; i < j; i++, j--) {
        let leftAuxiliary = nums[i];
        nums[i] = nums[j];
        nums[j] = leftAuxiliary;
    }
}
``` 
**Conclusion** : Need to work on it, don't know how to think of that algorithm by myself
---

### Move Zeroes (Difficulty -> Easy) : Day Three

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

```javascript
var moveZeroes = function(nums) {
    for (let i = nums.length; i>=0 ; i--) {
        if (nums[i] === 0) {
            nums.splice(i,1);
            nums.push(0);
        }
    }
};
``` 
**Conclusion** : Splice very useful to delete specific value of an array, don't forget to start looping through the end of the array to avoid looping infinitly on the 0 you add. 

---




