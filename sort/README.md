- 基础知识：快速排序（Quick Sort）， 归并排序（Merge Sort）的原理与代码实现。需要能讲明白代码中每一行的目的。快速排序时间复杂度平均状态下O（NlogN），空间复杂度O（1），归并排序最坏情况下时间复杂度O（NlogN），空间复杂度O（N）
- 入门题目：
   - [Leetcode 148. Sort List（排序链表）](https://leetcode-cn.com/problems/sort-list/)
   - [Leetcode 56. Merge Intervals （合并区间）](https://leetcode-cn.com/problems/merge-intervals/)
- 进阶题目：
   - [Leetcode 179. Largest Number（最大数）](https://leetcode-cn.com/problems/largest-number/)
   - [Leetcode 75. Sort Colors（颜色分类）](https://leetcode-cn.com/problems/sort-colors/)
   - [Leetcode 215. Kth Largest Element（数组中第k个最大的元素）](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)
   - [Leetcode 4. Median of Two Sorted Arrays](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

注意：后两题是与快速排序非常相似的快速选择（Quick Select）算法，面试中很常考



### 总结
 10种排序算法做以下总结对比，如图所示：<br />![](https://cdn.nlark.com/yuque/0/2019/webp/126606/1561801452845-9acc463e-bf00-4d5c-b286-52733c0c9669.webp#height=588&id=dGhBT&originHeight=588&originWidth=966&originalType=binary&ratio=1&size=0&status=done&style=none&width=966)   从平均时间复杂度来看，7种比较排序效率由低到高依次是：<br />  冒泡排序 ≈ 选择排序 ≈ 插入排序< 希尔排序< 堆排序 < 归并排序< 快速排序<br />  **快速排序**是效率最高的，适用于数据量大且数值随机排列的情况。但如果数据已经基本有序的情况下，效率退化到O(n^2)。<br />  **冒泡排序**是最慢的排序算法，在实际应用是效率最低的算法，时间复杂度为O(n^2)。<br />  **选择排序**在实际应用中和冒泡排序基本差不多，使用较少。<br />  **插入排序**比冒泡排序快2倍。一般不适合数据量比较大的场合或数据重复比较多的场合。<br />  **希尔排序**比冒泡排序快5倍，比插入排序大致快2倍。Shell排序比起快速排序，归并排序，堆排序慢很多。但shell算法比较简单，特别适合数据量在5000以下且性能要求不是很高的场合。<br />  **堆排序**由于不需要大量的递归或者多维的暂存数组，只需要一个用来交换的暂存空间，因此这对于数据量非常巨大的序列是很合适的。<br />  **归并排序**比堆排序稍微快一点，由于它需要一个额外的数组，因此需要比堆排序多一些内存空间。