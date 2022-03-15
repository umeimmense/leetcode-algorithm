希尔排序（Shell Sort）
  **希尔排序**，是对插入排序的一种改进，其排序的基本思想：先将整个待排序序列分割成若干个子序列，在子序列分别进行直接插入排序，待整个序列基本有序时，再对整体序列进行一次插入排序。<br />![](https://cdn.nlark.com/yuque/0/2019/webp/126606/1561801452944-ed0d9194-0720-4129-bf82-e318ff987644.webp#height=448&id=h8cji&originHeight=448&originWidth=853&originalType=binary&ratio=1&size=0&status=done&style=none&width=853)

### 算法描述

- 选择一个增量序列t1，t2，…，tk，其中ti>tj，tk=1；
- 按增量序列个数k，对序列进行k 趟排序；
- 每趟排序，根据对应的增量ti，将待排序列分割成若干长度为m 的子序列，分别对各子表进行直接插入排序。仅增量因子为1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。

### 代码实现
```javascript
function SellSort(arr) {
    var len = arr.length;
    for(var gap = Math.floor(len / 2); gap > 0; gap = Math.floor(gap / 2)) {
        // 多个分组交替执行
        for(var i = gap; i < len;i++) {
            var j = i;
            var current = arr[i];
            while (j - gap >= 0 && current < arr[j - gap]) {
                 arr[j] = arr[j - gap];
                 j = j - gap;
            }
            arr[j] = current;
        }
    }
    return arr;
}
```