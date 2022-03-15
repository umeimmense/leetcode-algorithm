## 快速排序（Quick Sort）
  **快速排序**，是对冒泡排序的一种改进。在快速排序中，记录的比较和移动的是从两端向中间进行，数值大的记录一次就能从前面移动到后面，数值小的记录一次就能从后面移动到前面，从而减少了总的比较次数和移动次数。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452709-1d5ce1dc-08e8-49dd-83ce-9ba2b1ecd6d5.gif#height=252&id=GcywX&originHeight=252&originWidth=811&originalType=binary&ratio=1&size=0&status=done&style=none&width=811)

### 算法描述
快速排序使用分治法把一个数列（list）分为2个数列（sub-lists），具体算法如下：
- 从数列中挑出一个元素，称为 “基准”（pivot）；
- 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；
- 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

### 代码实现
```javascript
function quickSort(arr, left, right) {
    var len = arr.length,
        partitionIndex,
        left = typeof left != 'number'? 0 : left,
        right = typeof right != 'number'? len -1 : right;
    if(left < right) {
        partitionIndex = partition(arr, left, right);
        quickSort(arr, left, partitionIndex-1);
        quickSort(arr, partitionIndex+1, right);
    }
}
// 分区操作
function partition(arr, left, right) { 
    // 设定基准值pivot
    var pivot = left,
        index = pivot+1;
    for(var i = index;i<= right;i++){
        if(arr[i] < arr[pivot]){
            swap(arr, i, index);
            index++;
        }
    }
    swap(arr, pivot, index-1);
    return index-1;
}
// 交换数据
function swap(arr, i, j) {
    var temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```