
# --------Tag: Hashtable---------

## 8.1

### 398.


### 594. Longest Harmonious Subsequence
* 一个整数数组， 找出相差为一的所有数来组成新数组。返回这样的数组的最大长度。
* HashMap记录出现的数和相应的频率。然后遍历key, 如果contains，那么相加频率。取最大。

1. 遍历key 用方法 map.keySet();   即 for (int i : map.keySet()) {}
2. 遍历value 用方法 map.values();





### 389. Find the Difference
* 两个字符串，只有小写字母，其中有一个字符串多了一个字母，返回多的字母. abc abcd 返回d
* 用NOR操作。 以后得出d





### 438.


## 8.2

### 500. Keyboard Row
* 输入一个字符串数组，都是单词。 如果里面的单词的字母都在键盘的同一行，加入res[]中，返回res.
* 用三个HashSet，一个空的HashSet作为指针，查找单词第一个然后指向相应的HashSet。或用一个HashMap存char和行数。

1. 首字母是大写的，所以存的时候记得存大写。
2. 什么时候add，当设一个长度如果大小等于单词长度则记录。
3. List -> Array : res.toArray(new String[res.size()])

### 447. Number of Boomerangs






