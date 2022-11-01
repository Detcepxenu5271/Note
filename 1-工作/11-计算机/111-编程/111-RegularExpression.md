# Regular Expression


## 一些自己的实践
### 去除数字的前导零
```shell
^(0*)([\d^0]+|0)(|\.\d+)\t
$2$3
```
