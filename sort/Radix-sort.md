## 基数排序（Radix Sort）
  **基数排序**，是按照低位先排序，然后收集；再按照高位排序，然后再收集；依次类推，直到最高位。<br />![](https://cdn.nlark.com/yuque/0/2019/webp/126606/1561801453226-963c9c24-330f-4370-b341-9427bba9f0de.webp#height=567&id=IM76r&originHeight=567&originWidth=1000&originalType=binary&ratio=1&size=0&status=done&style=none&width=1000)

### 算法描述

- 取得数组中的最大数，并取得位数；
- arr为原始数组，从最低位开始取每个位组成radix数组；
- 对radix进行计数排序（利用计数排序适用于小范围数的特点）。

### 代码实现
```javascript
var counter = [];
function radixSort(arr, maxDigit) {
    var mod = 10;
    var dev = 1;
    for (var i = 0; i < maxDigit; i++, dev *= 10, mod *= 10) {
        for(var j = 0; j < arr.length; j++) {
            var bucket = parseInt((arr[j] % mod) / dev);
            if(counter[bucket]==null) {
                counter[bucket] = [];
            }
            counter[bucket].push(arr[j]);
        }
        var pos = 0;
        for(var j = 0; j < counter.length; j++) {
            var value = null;
            if(counter[j]!=null) {
                while ((value = counter[j].shift()) != null) {
                      arr[pos++] = value;
                }
          }
        }
    }
    return arr;
}
```