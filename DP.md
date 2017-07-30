
# --------Tag: DP---------

## 7.28

### 303. Range Sum Query - Immutable
* nums 和 sumRange（index1, index2）求和
* sums[0] = nums[0] ; for 1->n-1 sums[i] = nums[i] + sums[i-1]