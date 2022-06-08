# Cracking-the-Coding-Interview
Starting my preparation for coding interview : So let's first dig into data structure algorithm.
Goal : One algorithm per day at minimum, starting the seventh of november 2021 !
Always aim for O(log(n)) complexity algorithm.

---

### 1] Binary Search (Difficulty -> Easy) : Day One
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

### 2] First Bad Version (Difficulty -> Easy) : Day Two

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

### 3] Search Insert Position (Difficulty -> Easy) : Day Three

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

### 4] Squares of a Sorted Array (Difficulty -> Easy) : Day Three

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

### 5] Rotate Array (Difficulty -> Medium) : Day Three

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
**Conclusion** : ⚠️ TODO -> Need to work on it | Don't know how to think of that algorithm by myself

---
### 6] Move Zeroes (Difficulty -> Easy) : Day Three

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
### 8] Two Sum II - Input Array Is Sorted (Difficulty -> Easy) : Day Four

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

```javascript
// O(n) complexity 
var twoSum = function(numbers, target) {
    let left = 0;
    let right = numbers.length - 1;
    while (left <= right) {
        let sums = numbers[left] + numbers[right];
        
        if (sums === target) {
            return [left+1,right+1];
        }
        else if (sums > target) {
            right -= 1;
        }
        else { 
            left += 1; 
        }
    }
};
``` 
**Conclusion** : Two pointers, right and left, if the sums of both is greater than target then go lower with decrementing right, either go upper with incrementing left.

---

### 9] Reverse String (Difficulty -> Easy) : Day Four

Write a function that reverses a string. The input string is given as an array of characters s.

```javascript
// Goes throught the whole array simultanisly by the left and right, 
// And at each iteration reverse the values of the pointer index
var reverseString = function(s) {
    let left = 0;
    let right = s.length - 1;
    
    while (left <= right) {
        let leftAuxiliary = s[left];
        s[left] = s[right];
        s[right] = leftAuxiliary;
        left ++;
        right --;
    };
    return s;
};
``` 
**Conclusion** : Goes throught the whole array simultanisly by the left and right, and at each iteration reverse the values of the pointer index

---
### 10] Reverse Words in a String III (Difficulty -> Easy) : Day Five

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

```javascript
// First Solution : Not optimal, complexity of O(n)
var reverseWords = function(s) {
    let reversedArray = [];
    let currentWord = [];
    let reversedWord = [];
    s += " ";
    for (i=0;i<s.length;i++) {
        if (s.charAt(i) === " ") {
            reversedWord = reverse(currentWord);
            reversedArray = reversedArray.concat(reversedWord);
            reversedArray.push(" ");
            currentWord = [];
        }
        else {
            currentWord.push(s[i]);
        }
    }
    reversedArray.pop();
    let reversedString = reversedArray.join('');
    return reversedString;
};

function reverse(wordArray) {
    let left = 0;
    let right = wordArray.length - 1;
    
    while (left<=right) {
        let leftAuxialiary = wordArray[left];
        wordArray[left] = wordArray[right];
        wordArray[right] = leftAuxialiary;
        left ++;
        right --;
    }
    return wordArray;
}
``` 
**Conclusion** : ⚠️ TODO -> Need to work on it | 

---
### 📚 *New Concept* Linked List : 

    In computer science, a linked list is a linear collection of data elements whose order is not given by their physical placement in memory. Instead, each element points to the next. It is a data structure consisting of a collection of nodes which together represent a sequence. In its most basic form, each node contains: data, and a reference (in other words, a link) to the next node in the sequence. This structure allows for efficient insertion or removal of elements from any position in the sequence during iteration. More complex variants add additional links, allowing more efficient insertion or removal of nodes at arbitrary positions. A drawback of linked lists is that access time is linear (and difficult to pipeline). Faster access, such as random access, is not feasible. Arrays have better cache locality compared to linked lists.

---
### 11] Middle of the Linked List (Difficulty -> Easy) : Day Five

Given the head of a singly linked list, return the middle node of the linked list.

If there are two middle nodes, return the second middle node.
```javascript
var middleNode = function(head) {
    let slow = head, fast = head;
    while (fast !== null) {
        fast = fast.next;
        if (fast == null) break;
        else fast = fast.next;
        
        slow = slow.next;
    }
    return slow;
};
``` 
**Conclusion** : Instantiate another list and increment it two times faster in the following loop that go through the initial linked list with list.next.

---

### Reviewing previous algorithms : Day Seven

---

### 12] Reading Cracking The Coding Interview 6th Edition : Day Eight

Big O notation, it means the time complexity of an algorithm. The notation possible are : O(n), O(log(n)), O(n²), O(n\*log(n)) . Because we always git rid of constants, because we don't focus at all on the litle complexity. For example we won't have a complexity of O(2n) if we have go through two times of a n array size, we would just put O(n).

O(log(n)) << O(n\*log(n)) << O(n) << O(n²) << O(e²n)

---
### 13] Remove Nth Node From End of List (Difficulty -> Easy) : Day Nine

```javascript
const removeNthFromEnd = (head, n) => {
    let slow = head, fast = head;
    while (n>0) {
        fast = fast.next;
        n--;
    }
    while (fast && fast.next) {
            slow = slow.next;
            fast = fast.next;
    }
    if (!fast){
        return head.next;
    }
    slow.next = slow.next.next;
    return head;
}
```
---
### 14] Remove Nth Node From End of List (Difficulty -> Easy) : Day 10<sup>th</sup>

```javascript
function twoNumberSum(array, targetSum) {
	// Y = targetSum - X
	const dico = {};
	for (const currentValue of array) {
		const valueToFind = targetSum - currentValue;
		if (valueToFind in dico) {
			return[valueToFind, currentValue];
		}
		else {
			dico[currentValue] = true;
		}
	}
	return [];
}
```
----
### 15] Longuest Peak (Difficulty -> Easy) : Day 11<sup>th</sup>

```javascript
function longestPeak(array) {
  longestPeakLength = 0;
  let i = 1;
  while (i < array.length-1) {
    const isPeak = (array[i - 1] < array[i] && array[i+1] < array[i])
    if (!isPeak) {
      i += 1;
      continue;
    } 
    leftIdx = i - 2;
    while (leftIdx >= 0 && array[leftIdx] < array[leftIdx + 1] )
      {
        leftIdx --;
      }
    rightIdx = i + 2;
    while (rightIdx < array.length && array[rightIdx] < array[rightIdx - 1]) {
          rightIdx += 1;
    }

     const currentPeakLength = rightIdx - leftIdx - 1;
    longestPeakLength = Math.max(longestPeakLength, currentPeakLength);
    i = rightIdx;

  }
  return longestPeakLength;
}
```
----

