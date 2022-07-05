## 题目描述（[link](https://leetcode.cn/problems/largest-number/)）
给定一组非负整数 nums，重新排列每个数的顺序（每个数不可拆分）使之组成一个最大的整数。
注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。
示例 1：
> 输入：nums = [10,2]
> 输出："210"

示例 2：
> 输入：nums = [3,30,34,5,9]
> 输出："9534330"

提示：
> 1 <= nums.length <= 100
> 0 <= nums[i] <= 109



## 思路分析及代码实现
这一题很容易想到把数字都转化为字符串，利用字符串比较，来排序，这样 9 开头的一定排在最前面。不过这样做有一个地方是错误的，比如：“3” 和 “30” 比较，“30” 比 “3” 的字符序要大，这样排序以后就出错了。实际上就这道题而言， “3” 应该排在 “30” 前面。
在比较 2 个字符串大小的时候，不单纯的只用字符串顺序进行比较，还加入一个顺序。
```go
aStr := a + b
bStr := b + a
```
通过比较 aStr 和 bStr 的大小来得出是 a 大还是 b 大。
举个例子，还是 “3” 和 “30” 的例子，比较这 2 个字符串的大小。

```go
aStr := "3" + "30" = "330"
bStr := "30" + "3" = "303"
```
#### JS版本
```javascript
/**
 * @param {number[]} nums
 * @return {string}
 */
var largestNumber = function(nums) {
    quickSort(nums,0,nums.length-1)
    return nums[0] == '0'?'0':nums.join('')
};
function quickSort(nums,start,end) {
    if(start >= end) return
    var index = start
    var pivot = nums[start]
    for(let i = start + 1;i <= end;i++){
        if(nums[i] + ''+ pivot > pivot + ''+ nums[i]){
            index++
            swap(nums,index,i)
        }
    }
    swap(nums,index,start)
    quickSort(nums,start,index-1)
    quickSort(nums,index+1,end)
}
function swap(nums,l,r) {
    var temp = nums[l]
    nums[l] = nums[r]
    nums[r] = temp
}
```
#### Golang版本
```go
import (
	"strconv"
)

func largestNumber(nums []int) string {
	if len(nums) == 0 {
		return ""
	}
	numStrs := toStringArray(nums)
	quickSortString(numStrs, 0, len(numStrs)-1)
	res := ""
	for _, str := range numStrs {
		if res == "0" && str == "0" {
			continue
		}
		res = res + str
	}
	return res
}

func toStringArray(nums []int) []string {
	strs := make([]string, 0)
	for _, num := range nums {
		strs = append(strs, strconv.Itoa(num))
	}
	return strs
}
func partitionString(a []string, lo, hi int) int {
	pivot := a[hi]
	i := lo - 1
	for j := lo; j < hi; j++ {
		ajStr := a[j] + pivot
		pivotStr := pivot + a[j]
		if ajStr > pivotStr { // 这里的判断条件是关键
			i++
			a[j], a[i] = a[i], a[j]
		}
	}
	a[i+1], a[hi] = a[hi], a[i+1]
	return i + 1
}
func quickSortString(a []string, lo, hi int) {
	if lo >= hi {
		return
	}
	p := partitionString(a, lo, hi)
	quickSortString(a, lo, p-1)
	quickSortString(a, p+1, hi)
}
```

