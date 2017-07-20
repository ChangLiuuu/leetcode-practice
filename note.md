
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
2. 最后需要新建数组，新建数组方法别忘了‘new’: int[] arr = new int[n + 1];
3. for循环的i 习惯写i++了 从大到小写时候，记住i--，杜绝弱智行为。



## 7.18

### 88. Merge Sorted Array
* 两个数组，要求将nums2并到nums1中，两个数组中的数初始长度m和n，nums1的长度足够（大于等于m + n）无返回值。
* 利用3个pointer记录3个index，在已知长度的情况下，从后向前比较，如果从前向后会覆盖掉还未比较的nums1元素。 

1. 写法上trick  i > -1 代替 i >= 0 操作少一个等号 速度相对快点
2. 熟练三目运算符与i--配合  nums1[k--] = (nums1[i] > nums2[j] ? nums1[i--] : nums2[j--])
3. nums1的指针若先结束，则会出现一个问题，就是开头是重复的，所以要将未用完的nums2复制到num1开头


### 118. Pascal's Triangle I
* 给一个数例如5 ，输入 
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

* 将数组对齐进行推理。首先要看出来有两层循环，外层add（row）,内层构建row。构建内层row时，长度首先是和上一个数组长度是一样的，通过变化后，head增加元素1既row(0, 1) 然后 add(row)即可.

1. 掌握 add(index, ele) 和 set(index, ele) 用法
2. 杜绝错误：改变当前元素index错了使循环变量发生了变化比如 1 2 1 -> 1 3 1-> 1 3 4 1
3. 所以，一般循环迭代时候考虑从后想前迭代。

### 119. Pascal's Triangle II
* 给一个rowIndex k return 第k行的数组 例如3 return [1,3,3,1]

1. 陷阱就是k的取值，是从0开始的！不是从1. 与118不同！

## 7.19

### 605. Can place flowers
* 给一个0，1数组nums 和 想种花的数量n。是否能保证花1不相邻，返回boolean。 
* Greedy解法。难点在于开头和结尾的判断，本身0 看pre和next是否为0.

1. 难点在于开头和结尾的判断，但一个巧妙的方法避开了edge case，避免数组越界： 假设两个整数 pre 和 next。若为开头则直接设pre=0,否则 pre=nums[i-1] 同理 next.
2. 三目运算符运用

### 121. Best Time to Buy and Sell Stock
* 一个无序数组，选择两个数，使后减前差最大，返回差值。
* 动态规划。 每走一步，找出这一步及之前的最低价，然后用此时的价格减去最低价，比较出最大利。目的为了每走一步都要得出这一步的最高利益。 方法二：Kadane算法，记录每次基于之前价格的变化浮动，求出最大子序列和。

1. edge case: length < 2 return 0; 因为 i 从1开始的。
2. Kadane算法有点不好理解的地方就是 为什么求出最大子序列和就求出最大利益了。因为记录每次的浮动是基于每次之前的价格。浮动的大小就是赚了多少，所以求和即可。

