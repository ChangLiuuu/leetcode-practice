
# --------Tag: Array---------

## 7.17

### 561. Array Partition 
* 2n个整数，分割数组，两两一对，取每对较小的数使和最大，返回和。
* 用Greedy，最大化每对较小数之和，那么一对数字大小越近越好，因为舍掉大数字就浪费了。
所以，先sort一下，取奇数位求和。 

1. Arrays.sort(int[] nums) 用法
2. for 循环里是 i += 2; 不是 i + 2;


### 6. Remove Depulicates from Sorted Array
* 不分配额外空间，使老数组的前x项不重复作为新数组，不用管x项之后的长度，返回新数组长度。
* 用two pointers。end负责移动每次与front比较, front记录不重复的. 当nums[front]和nums[end]不相等时，front先向后移在该位置填上nums[end]（可优化）.

1. 边角情况，长度是0或1 判断条件直接 length < 2, 则 return length;
2. 优化: 如果front++之后，front != end  再填上nums[end]. 减少了一部分操作。
3. 最后返回长度 front + 1; front相当于新数组的末尾了。
4. 区分nums[i++] 和 arr = nums[++i]  (i = i + 1; arr = nums[i])


### 66. Plus One
* 数组代表一个整数A各位的digits，返回一个新数组，数组为整数A + 1后各位的digits.
* 从最高位开始遍历，判断是否小于九，若小于则digit+1返回数组，否则，该digit为零。遍历结束还没返回则说明都为9，需要创建新数组arr，长度为原长度加一。arr[0] = 1 return arr;

1. 记住整数加一的思想，同理比如加二呢。
2. 最后需要新建数组，新建数组方法别忘了‘new’。  int[] arr = new int[n + 1];
3. for循环的i 习惯写i++了 从大到小写时候，记住i--，杜绝弱智行为。

	


