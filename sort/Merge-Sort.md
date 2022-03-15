## 归并排序（Merge Sort）
  **归并排序**，是一种借助“归并”进行排序的方法，归并的含义是将两个或两个以上的有序序列归并成一个有序序列的过程。归并排序的主要思想：将若干有序序列逐步归并，最终归并为一个有序序列。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452790-b6656778-38b0-49a8-93bb-93b2f8260cb6.gif#height=505&id=CnxPu&originHeight=505&originWidth=811&originalType=binary&ratio=1&size=0&status=done&style=none&width=811)
<a name="tDHHN"></a>
### 算法描述

- 把长度为n的输入序列分成两个长度为n/2的子序列；
- 对这两个子序列分别采用归并排序；
- 将两个排序好的子序列合并成一个最终的排序序列。
<a name="PFukR"></a>
### 代码实现
```javascript
function mergeSort(arr) {  //采用自上而下的递归方法
    var len = arr.length;
    if(len < 2) {
        return arr;
    }
    var middle = Math.floor(len / 2),
        left = arr.slice(0, middle),
        right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}
function merge(left, right) {
    var result = [];
 
    while (left.length && right.length) {
        if (left[0] <= right[0]) {
            result.push(left.shift());
        } else {
            result.push(right.shift());
        }
    }
 
    while (left.length)
        result.push(left.shift());
 
    while (right.length)
        result.push(right.shift());
 
    return result;
}
```