# 3sum

## Question
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]

Example 2:
Input: nums = []
Output: []

Example 3:
Input: nums = [0]
Output: []

## Solution
``` js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
const threeSum = function(nums) {
  let result = [];
  nums = nums.sort((a, b) => a - b);
  for(let i = 0; i < nums.length; i++) {
    if (nums[i] > 0) {
      break;
    }
    if (i > 0 && nums[i] === nums[i - 1]) {
      continue;
    }
    let l = i + 1, r = nums.length - 1, target = -nums[i];
    while (l < r) {
      let sum = nums[i] + nums[l] + nums[r];
      if (sum === 0) {
        result.push([nums[i], nums[l], nums[r]]);
        // 防止左指针重复解
        while (nums[l] === nums[l + 1]) { l++ }
        // 防止右指针出现重复解
        while (nums[r] === nums[r - 1]) { r-- }
        l++;
        r--;
        // 小于 0 说明左边界的数小了，往右移动，因为整个数是排序好的
      } else if (sum < 0) { 
        l ++;
      } else {
        r --;
      }
    }
  }
  return result;
};
```
本题采用一个循环加一个双指针来解决，关键点在于去重的逻辑：如果前后重复，则自动移到下一位。另外双指针90%以上的题目都是需要排序的，去重后才能更有效的判断指针左右移动的条件，这点要注意。