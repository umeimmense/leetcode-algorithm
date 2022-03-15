## 冒泡排序（Bubble Sort）
  **冒泡排序**，是交换排序中最简单的排序方法，其主要思想是：在待排序序列中选两相邻记录的数字，如果反序则交换，直到没有反序的数列为止。<br />![](https://cdn.nlark.com/yuque/0/2019/gif/126606/1561801452701-0a5d5c4b-caa8-4f1d-a99a-2b141fe47edf.gif#height=257&id=curWg&originHeight=257&originWidth=826&originalType=binary&ratio=1&size=0&status=done&style=none&width=826)

### 算法描述
- 比较相邻的元素。如果第一个比第二个大，就交换它们两个；
- 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；
- 针对所有的元素重复以上的步骤，除了最后一个；
- 重复步骤1~3，直到排序完成。

### 代码实现
```javascript
function bubbleSort(arr) {
    var len = arr.length;
    for(var i = 0;i < len;i++) {
        for(var j = 0;j < len-1-i;j++) {
            if(arr[j] > arr[j+1]) {// 相邻元素两两比较
                var temp = arr[j+1];// 元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}
```