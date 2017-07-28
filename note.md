
# --------Tag: Array---------

## 7.17

### 561. Array Partition 
* 2n个整数，分割数组，两两一对，取每对较小的数使和最大，返回和。
* 用Greedy，最大化每对较小数之和，那么一对数字大小越近越好，因为舍掉大数字就浪费了。
所以，先sort一下，取奇数位求和。 

1. Arrays.sort(int[] nums) 用法
2. for 循环里是 i += 2; 不是 i + 2;


### 26. Remove Depulicates from Sorted Array
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
* 利用3个pointer记录3个index，在已知长度的情况下，从m+n-1向前比较，避免覆盖元素。 

1. 写法上trick  while(i > -1) 不是  i > 0
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

1. 掌握 add(index, ele) 和 set(index, ele) 用法(replace的作用)
2. 杜绝错误：改变当前元素index错了使循环变量发生了变化比如 1 2 1 -> 1 3 1-> 1 3 4 1
3. 所以，一般循环迭代时候考虑从后想前迭代。
4. res.add(new ArrayList<Integer>(row))    (row)的格式就是new的格式

### 119. Pascal's Triangle II
* 给一个rowIndex k return 第k行的数组 例如3 return [1,3,3,1]

1. 陷阱就是k的取值，是从0开始的！不是从1. 与118不同！

## 7.19

### 605. Can place flowers
* 给一个0，1数组nums 和 想种花的数量n。是否能保证花1不相邻，返回boolean。 
* Greedy解法。难点在于开头和结尾的判断，本身0 看pre和next是否为0.

1. 难点在于开头和结尾的判断，但一个巧妙的方法避开了edge case，避免数组越界： 假设两个整数 pre 和 next。若为开头则直接设pre=0,否则 pre=nums[i-1] 同理 next.
2. 三目运算符运用
3. count++ 完之后 记得种上花，既 flowerbed[i] = 1； 别犯第二次-，-


### 121. Best Time to Buy and Sell Stock
* 一个无序数组，选择两个数，使后减前差最大，返回差值。
* 动态规划。 每走一步，找出这一步及之前的最低价，然后用此时的价格减去最低价，比较出最大利。目的为了每走一步都要得出这一步的最高利益。 方法二：Kadane算法，记录每次基于之前价格的变化浮动，求出最大子序列和。

1. edge case: length < 2 return 0; 因为 i 从1开始的。
2. Kadane算法有点不好理解的地方就是 为什么求出最大子序列和就求出最大利益了。因为记录每次的浮动是基于每次之前的价格。浮动的大小就是赚了多少，所以求和即可。
3. 有个trick 就是DP方程里的值 curMax = max(nums[i], curMax + nums[i]) 这里可以直接max(0, curMax + nums[i]) 这里的nums[i]就是 pirces[i] - prices[i - 1] 价格相对浮动值。最差就是不赚不赔，所以浮动为负数不用考虑。


### 122 Best Time to Buy and Sell Stock II
* 多次买卖，但是手里能持一支股票，既想买时，必须卖掉手里那支。
* 用Greedy思想，局部最高减局部最低。这道题有点逗，因为相邻两支股票有差价时要么前>后 要么 前<后，肯定是在前<后进行买卖。即每次买卖肯定是存在于相邻两天的价格。 diff为正时累加求得。

1. 同121一样 考虑edge case。
2. Greedy思想理解。


### 53. Maximum Subarray
* 给一串数组，求连续的一个子序列和最大是多少
* DP的思路。 时间复杂度O(n). 一个参数控制舍弃前面的数，一个参数负责记录全局最大和。 到i时考虑前面是否为累赘，若为累赘则和清零重新从这位开始。

1. 思路一看前面的和是不是负数，既 curMax = n[i] + (curMax > 0 ? curMax : 0);
2. 思路二看curMax = Math.max(n[i], n[i] + curMax); 两种思路都是判断前面是累赘还是大腿，要不要舍掉的问题。。
3. 注意edge case: length == 0 的情况

## 7.20

### 1. two sum
* 给一个数target，在数组里找到两个数和等于target，返回这两个数index组成的数组。只有一组解，并且同一元素本身不能使用两次。
* hashmap.

1. 二逼错误，数组声明 .... = new int[2]; 不是  new int(2)
2. 考虑到不能同一元素使用两次即4 + 4 = 8 第一个4和第二个4的index应该是不一样的。所以先check hashmap里是否有target - nums[i] 有话res[0] = i res[0] = map.get(target - nums[i]); 没有的话 再put(nums[i],i) 

### 442. Find All Duplicates
* 一个数组 1 <= a[i] <= n, 有些元素出现了两次，找出重复元素，返回一个ArrayList。保证哦恩复杂度无额外空间。
* 负号标记大法 或 元素复位法。 方法一好用。找到元素和下标关系，index = abs(ele) - 1 对应变负. 如果发现对应已经是负说明重复。

1. 重点在于操作数组符号后，还要用到已经变负数的元素，为了找到对应下标嘛，但这时候存在的问题就在这个元素是负的，ele - 1 负数作为下标肯定不行。用Math.abs()方法也存在问题 问题在于原有元素用abs()方法了，符号就被人为改变了，而不是元素碰到对应下标改变的了。
2. 用临时变量取元素绝对值减一得到对应下标，这样既得到了下标，又没改变原有数组的正负。

### 448. Find All Numbers Disappeared in an Array
* 同442，不过找的找出的是消失的元素，返回ArrayList。 保证哦恩复杂度无额外空间。
* 负号标记大法。 遍历两次，第二次找出元素还大于零的数，对应下标加一就是原数组消失的元素了。 

## 7.21

### 581. Shortest Unsorted Continuous Subarray
* 递增序列找最短乱序M 使M排好后整个序列就递增了 返回M长度
* 乾坤挪移奇迹大法。 max开头，min最后，两个指针start end。end说起： 如果 开头后面的数比max还大，max更新没毛病，因为本来就是递增的；如果max不更新了，就出问题了，说明变小趋势，end该向后移动了
同理 start.

1. 这个方法真的无解。直观方法就是先排好序，然后two pointer 首位比较。但排序时间复杂度nlogn 没这个 O(n)的牛逼。
2. 技巧点在于 找max从开头找，找min从尾巴向前找。
3. 还有一点厉害之处，设置 start = -1 end = -2 这样, end - start + 1  避免edge case 检验

### 566. Reshape the Maxtrix
* 二维数组变型，比如4 * 1 变成 2 * 2形式。给出r c 和 nums[][] 如果能变 返回新的res[r][c]，如果不能返回原数组。
* 遍历原矩阵，设置新矩阵的row 和 col 自加。如果col == c row++ col = 0 方法二 遍历原矩阵index, index / c 为行 index % c 为列 nums行 index / nums[0].length 列： %

1. 记住数组常用方法，取col的商得行数，取col得余数得列数。

## 7.22

### 628. Maximum Product of Three Numbers
* 给一个数组范围[-1000, 1000] 个数[3, 10^4] 找出三个数乘积最大，返回这个乘积。
* 三个数乘积最大，要保证乘积最大，乘积尽可能是正数且绝对值最大，+++ --+ -++（挑--+）如果三个负数，则保证绝对值最小 ---。  三个最大数相乘。Math.max(max1 * max2 * max3, min1 * min2 * max3)

1.掌握在一个数组里得到前k个最值O(n)方法。

### 643. Maximum Average Subarray I
* 数组里有n个整数，找到连续长度k的子序列使和最大 返回和平均数,带小数的。
* sliding window方法. 先找到前k项和sum 然后设max=sum, 从后开始相当于进一个出一个，吃一个n[i]拉一个n[i-k]的赶脚。

1. 重点在于最后类型的强制转换，一个int数乘以1.0得到double型
2. 注意下标是0到k-1 之后是从k开始进一个出一个

### 532. K-diff Pairs in an Array
* 整型数组range[-1e7, 1e7]，给一个差值k，找出数组中元素差值为k的对儿数，返回pairs数。
* hashmap。key记录ele value记录ele的频率 若k==0 找频率大于1的,count++, else if map.countsKey(entry.getKey() + k), count++.

1. edge case: 这题需要考虑k<0和nums.length<2
2. 学会了map的遍历：for(Map.Entry<Integer,Integer> entry : map.entrySet()){}
3. hashmap JAVA8新方法： map.getOrDefault() :  map.put(m, map.getOrDefault(m, 0) + 1)  如果对应k没有value 设默认值。

## 7.23
复习，修改笔记。


## 7.24

### 167. Two Sum II - Input array is sorted
* sorted数组，给一个target，返回数组[]{index1, index2} 其中index1 < index2
* two pointers 首尾向中间移动

1. edge case： 长度小于2
2. 空数组 new int[2]；
3. 初始化数组 new int[]{left + 1, right + 1} 或 int[2]   这道题index从1开始的所以left right 要加一

### 27 Remove Element
* 给nums[] 和 val , 去掉nums里ele=val的 返回长度
* two pointers 前面check 后面cur记录

1. 最后长度是cur 不是cur + 1 因为是先改变ele再cur++ 最后cur的位置总是数组的位置多一
2. 优化： 改变ele时候 check一下 nums[cur] != nums[i]


## 7.25

### 217. Contains Duplicate
* 整形数组，有重复元素返回true，没有返回false
* Hashset time: n, space: n;    先sort再比较相邻  time: nlogn, space 1

1. set先check 再 add. 
2. 比较相邻注意边界

### 219 Contains Duplicate II
* 整形数组，在k距离内找到两个元素相等。如果能找到返回true。
* HashSet思路： 在长度diff为k的hashset里，如果add不进去了，说明找到了。 保证k长度的hashset需要提前remove掉第i - k - 1个，再add第i个.

1. 领会i - k到哪个index了 0_____k    然后领会 i - k - 1： x 0_____k


### 169. Majority Element
* 一个数组，其中有一个数出现次数大于 n/2 ，返回这个数。（比存在这样的数）
* 动态规划的思想。count计数，当count为0时，说明有数抵消掉res了，这时从新开始count = 1 res = n[i]. 总会有一个数的count比其他数大，然后res不变了 或者是刚变 比如1 2 1，最后一个1就是刚变的res。

复习之前的题，做到bugfree.


## 7.26

### 35. Search Insert Position
* 一个sorted数组 和 一个target 如果ele有 返回index; 如果没有 返回target排序后应该在的index。
* 二分搜索。 sorted的 有target。重点在于边界的判定。 

1. low + (high - low) / 2 防止变量溢出
2. while (low <= high) ;   low = mid + 1   high = mid - 1
3. return low; 

### 414. Third Maximum Number
* 返回数组第三大的数，没有的话返回最大的数。[1,2,2] 返回2（如果元素相同，算并列大）
* max3 max2 max1 

1. 初始时 Integer max3 = null, 避免max不知道是自己初始化赋值还是比出来的。
2. for (Integer i : nums)
3. for循环里面要先判断if(nums[i].equals(max).......) continue;


## 7.27

### 283. Move Zeroes
* 一个数组把零都移到后面，没有额外空间。
* for (n : nums) n != 0  nums[cur++] = n;  while (cur < nums.length) nums[cur++] = 0;

1. for-each的用法, 前面逐个覆盖后面数的时候常用


### 485. Max Consecutive Ones
* 一个Binary数组（只有0,1) 返回最大几个1连续。
* counter计数。遇到0 counter=0, 遇到1 counter++  用max记录max（max, counter）

1. for-each 立马用上


### 268. Missing Number
* 有一个0到n的数组，这时候拿走一个数组成新数组nums。返回拿走的那个数。
* 方法1：O(n) 异或   0 1 2 3 5 6   设 res = 6， res异或i,然后异或nums[i]，相同的两个数异或为0，所以最后得到的数就是4
* ---------------   0 1 2 3 4 5
* 最好的方法是Binary search.  O(logn).


### 189 Rotate Array
* 给一个n和k  n代表从1到n的数组， k代表把最后一个元素放最前面 执行k次 比如n=4 k=2 [1 2 3 4] -> [3 4 1 2]
* 很巧妙。整体reverse一下，然后前k个再reverse，后 n - k个 reverse








