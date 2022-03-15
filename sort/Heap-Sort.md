## 堆排序（Heap Sort）
  **堆排序**，是利用堆数据结构设计的一种排序算法。堆是具有下列性质的完全二叉树：每个结点的值都小于或等于其左右孩子结点的值（称为小根堆）；或者每个结点的值都大于或等于其左右孩子结点的值（称为大根堆）。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452693-cebd608c-ea2f-448f-a238-fbf34cbf65d5.gif#height=364&id=d4ZYS&originHeight=364&originWidth=547&originalType=binary&ratio=1&size=0&status=done&style=none&width=547)

### 算法描述

- 将初始待排序关键字序列(R1,R2….Rn)构建成大顶堆，此堆为初始的无序区；
- 将堆顶元素R[1]与最后一个元素R[n]交换，此时得到新的无序区(R1,R2,……Rn-1)和新的有序区(Rn),且满足R[1,2…n-1]<=R[n]；
- 由于交换后新的堆顶R[1]可能违反堆的性质，因此需要对当前无序区(R1,R2,……Rn-1)调整为新堆，然后再次将R[1]与无序区最后一个元素交换，得到新的无序区(R1,R2….Rn-2)和新的有序区(Rn-1,Rn)。不断重复此过程直到有序区的元素个数为n-1，则整个排序过程完成。

### 代码实现
```javascript
// 多个函数需要用到数据长度，把len设为全局变量
var len; 
// 建立大顶堆
function buildMaxHeap(arr) {
    len = arr.length;
    for(var i = Math.floor(len/2); i >= 0;i--) {
        heapify(arr, i);
    }
}
// 堆调整
function heapify(arr, i) {
     var left = 2 * i + 1,
        right = 2 * i + 2,
        largest = i;
    if (left < len && arr[left] > arr[largest]) {
        largest = left;
    }
    if (right < len && arr[right] > arr[largest]) {
        largest = right;
    }
    if (largest != i) {
        swap(arr, i, largest);
        heapify(arr, largest);
    }
}
function swap(arr, i, j) {
    var temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
function HeapSort(arr) {
    buildMaxHeap(arr);
}
```
<a name="gdzbX"></a>