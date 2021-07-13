# Combination Sum

## Question

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

 

Example 1:
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.


Example 2:
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]


Example 3:
Input: candidates = [2], target = 1
Output: []


Example 4:
Input: candidates = [1], target = 1
Output: [[1]]


Example 5:
Input: candidates = [1], target = 2
Output: [[1,1]]
 

## Solution
``` jsx
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
  const res=[]
  candidates.sort((a,b)=>a-b)
  const dfs=(arr,target,index)=>{
      if(target===0){
          res.push(arr.slice())
          return
      }
      for(let i=index;i<candidates.length&&target-candidates[i]>=0;i++){
          arr.push(candidates[i])
          dfs(arr,target-candidates[i],i)
          arr.pop()
      }
  }
  dfs([],target,0)
  return res
};
```
本题使用回朔算法解题
参数就是放将来可能符合结果的数组、目标数、层级（如果没有会出现内部顺序不同但数字都一样的结果）
跳出条件target等于0；循环中额外加入target-candidates[i]>=0避免了递归的浪费调用，也就不会出现跳出递归判断条件中target小于0的情况
