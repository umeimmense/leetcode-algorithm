## 插入排序（Insertion Sort）
  **插入排序**，是一类借助“插入”进行排序的方法，其主要思想是：每次将一个待排序的数字按其关键码的大小插入到一个已排好的有序序列中，直到全部数字排好序。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452699-f47a2f46-0005-4a0b-b98b-9b25d04670f3.gif#height=505&id=Sh3pt&originHeight=505&originWidth=811&originalType=binary&ratio=1&size=0&status=done&style=none&width=811)

### 算法描述
插入排序采用in-place在数组上实现，具体算法描述如下：

- 从第一个元素开始，该元素可以认为已经被排序；
- 取出下一个元素，在已经排序的元素序列中从后向前扫描；
- 如果该元素（已排序）大于新元素，将该元素移到下一位置；
- 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置；
- 将新元素插入到该位置后；
- 重复步骤2~5。

### 代码实现
```javascript
function insertionSort(arr) {
    var len = arr.length;
    var preIndex, current;// 从后向前扫描索引，当前元素数值
    for(var i = 1;i<len;i++) {
        preIndex = i-1;
        current = arr[i];
        while(preIndex >= 0 && arr[preIndex] > current) {
            arr[preIndex+1] = arr[preIndex];
            preIndex--;
        }
        arr[preIndex+1] = current;
    }
    return arr;
}
```