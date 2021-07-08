# Search in Rotated Sorted Array

## Question
There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
Example 3:

Input: nums = [1], target = 0
Output: -1

## Solution
``` js
const search = function(nums, target) {
  let i = 0, j = nums.length - 1;
  if (nums.length === 0) return -1;
  if (nums.length === 1) {
    if (nums[0] === target) return 0;
    return -1;
  }
  while (i < j) {
    if (nums[i] === target) return i;
    if (nums[j] === target) return j;
    if (i <  target) {
      i ++;
    } else {
      j --;
    }

  }
  return -1;
};
```
题目中限定必须使用O(log n)的算法来做，所以不能直接使用顺序遍历。依然使用双指针来做。本题比较简单，重点在于对双指针移动时机的判断，以及边界值的判断。
切记一点：双指针算法中，一次循环中只有一个指针会移动，所以此类算法中判断到底是左指针还是右指针移动是解题重点。
一般判断的条件例如：左值和右值比大小；左值和中间值比大小或左值和一个特定标的比大小等。
