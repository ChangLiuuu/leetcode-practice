
# --------Tag: DP---------

## 7.28

### 303. Range Sum Query - Immutable
* nums 和 sumRange（index1, index2）求和
* sums[0] = nums[0] ; for 1->n-1 sums[i] = nums[i] + sums[i-1]

## 7.31

### 70. Climbing Stairs
* n层台阶，一次走一层或两层，求走到顶的方法有多少种
* 斐波那契数列递归思想。动态规划思想。 solve(n) --> solve(n-1) + solve(n-2)  

1. 优化空间复杂度：用数组保存走到该层的方法总数。
2. 再优化 就用3个数来保存，这一步 = 一步前 + 两步前， 两步前 = 一步前， 一步前 = 这一步。 一个传递的感觉。  