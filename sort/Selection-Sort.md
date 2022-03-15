## 选择排序（Selection Sort）
  **选择排序**，是一种简单直观的排序算法，其基本思想是：首先在待排序序列中选出最小值，存放在排序序列起始位置，然后再从剩余未排序元素中继续寻找最小元素，放到已排序序列末尾。以此类推，直到所有元素均排序完毕。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452734-2e5ff326-4dce-4ae2-8d7c-e6b532ebbaf0.gif#height=248&id=iOyLH&originHeight=248&originWidth=811&originalType=binary&ratio=1&size=0&status=done&style=none&width=811)

### 1、算法描述
n个记录的直接选择排序可经过n-1趟直接选择排序得到有序结果。具体算法描述如下：

- 初始状态：无序区为R[1..n]，有序区为空；
- 第i趟排序(i=1,2,3…n-1)开始时，当前有序区和无序区分别为R[1..i-1]和R(i..n）。该趟排序从当前无序区中-选出关键字最小的记录 R[k]，将它与无序区的第1个记录R交换，使R[1..i]和R[i+1..n)分别变为记录个数增加1个的新有序区和记录个数减少1个的新无序区；
- n-1趟结束，数组有序化了。

### 2、代码实现
```javascript
function selectionSort(arr) {
    var len = arr.length;
    var minIndex, temp;
    for(var i = 0; i< len-1;i++){
        minIndex = i;
        for(var j = i+1;j<len;j++) {
            if(arr[j] < arr[minIndex]) {// 寻找最小的数
                minIndex = j;
            }
        }
        temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
    return arr;
}
```