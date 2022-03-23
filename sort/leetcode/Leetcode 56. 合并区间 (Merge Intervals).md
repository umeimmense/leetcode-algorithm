题目描述（link）
以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。请你合并所有重叠的区间，并返回一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间。

示例 1：
输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
示例 2：
输入：intervals = [[1,4],[4,5]]
输出：[[1,5]]
解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。
提示：
1 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 104
思路分析及代码实现
如果我们按照区间的左端点排序，那么在排完序的列表中，可以合并的区间一定是连续的。如下图所示，标记为蓝色、黄色和绿色的区间分别可以合并成一个大区间，它们在排完序的列表中是连续的：


算法
我们用数组 merged 存储最终的答案。
首先，我们将列表中的区间按照左端点升序排序。然后我们将第一个区间加入 merged 数组中，并按顺序依次考虑之后的每个区间：
● 如果当前区间的左端点在数组 merged 中最后一个区间的右端点之后，那么它们不会重合，我们可以直接将这个区间加入数组 merged 的末尾；
● 否则，它们重合，我们需要用当前区间的右端点更新数组 merged 中最后一个区间的右端点，将其置为二者的较大值。


正确性验证
上述算法的正确性可以用反证法来证明：在排完序后的数组中，两个本应合并的区间没能被合并，那么说明存在这样的三元组 (i, j, k) 以及数组中的三个区间 a[i], a[j], a[k] 满足 i <j<k 并且 (a[i], a[k]) 可以合并，但 (a[i], a[j]) 和 (a[j], a[k]) 不能合并。这说明它们满足下面的不等式：
a[i].end<a[j].start(a[i] 和 a[j] 不能合并)
a[j].end<a[k].start(a[j] 和 a[k] 不能合并)
a[i].end≥a[k].start(a[i] 和 a[k] 可以合并)

我们联立这些不等式（注意还有一个显然的不等式 a[j].start≤a[j].end），可以得到：
a[i].end<a[j].start≤a[j].end<a[k].start
产生了矛盾！这说明假设是不成立的。因此，所有能够合并的区间都必然是连续的。
JS版本
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */

var merge = function (intervals) {
    intervals.sort((a, b) => a[0] - b[0]);
    let prev = intervals[0]
    let result = []
    for(let i =0; i<intervals.length; i++){
        let cur = intervals[i]
        if(cur[0] > prev[1]){
            result.push(prev)
            prev = cur
        }else{
            prev[1] = Math.max(cur[1],prev[1])
        }
    }
    result.push(prev)
    return result
};

golang版本
func merge(intervals [][]int) [][]int {
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][0]<intervals[j][0]
	})

	res:=[][]int{}
	prev:=intervals[0]

	for i:=1;i<len(intervals);i++{
		cur :=intervals[i]
		if prev[1]<cur[0]{
			res=append(res,prev)
			prev=cur
		}else {
			prev[1]=max(prev[1],cur[1])
		}
	}
	res=append(res,prev)
	return res
}
func max(a, b int) int {
	if a > b { return a }
	return b

复杂度分析

时间复杂度：O(nlogn)，其中 n 为区间的数量。除去排序的开销，我们只需要一次线性扫描，所以主要的时间开销是排序的 O(nlogn)。

空间复杂度：O(logn)，其中 n 为区间的数量。这里计算的是存储答案之外，使用的额外空间。O(logn) 即为排序所需要的空间复杂度。
