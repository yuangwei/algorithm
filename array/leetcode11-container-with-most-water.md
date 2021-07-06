# Container With Most Water

## Question
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.
<br />
link: https://leetcode.com/problems/container-with-most-water/

## Solution

``` js
var maxArea = function(height) {
  var maxarea = 0, l = 0, r = height.length - 1;
  while (l < r) {
    maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
    if (height[l] < height[r])
      l++;
    else
      r--;
  }
  return maxarea;
};
```

使用双指针算法解决此问题为最佳，通过向内移动两边界线较短的一方(容器的容量取决于少的一方，超过该界限则水会溢出)来改变容器的容量，找出其中最大值。
