# Compare Version Numbers

@(算法)

比较两个版本号 version1 和 version2。
如果 `version1 > version2` 返回 `1`，如果 `version1 < version2` 返回 `-1`， 除此之外返回 `0`。

你可以假设版本字符串非空，并且只包含数字和 . 字符。

` .` 字符不代表小数点，而是用于分隔数字序列。

例如，`2.5` 不是“两个半”，也不是“差一半到三”，而是第二版中的第五个小版本。

**示例 1:**
```powershell
输入: version1 = "0.1", version2 = "1.1"
输出: -1
```

**示例2:**
```powershell
输入: version1 = "1.0.1", version2 = "1"
输出: 1
```

**示例 3:**
```powershell
输入: version1 = "7.5.2.4", version2 = "7.5.3"
输出: -1
```

## 方法：

注意：`1.0`与`1`的特殊情况。

```python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        array1 = version1.split(".")
        array2 = version2.split(".")
        
        i, j = 0, 0
        
        while i < len(array1) or j < len(array2):
            if i == len(array1) and j != len(array2):
                """
                i 已到末尾
                """
                # 注意:1.0 与 1的特殊情况
                if int(array2[j]) != 0:
                    return -1
                else:
                    j = j + 1
            elif i != len(array1) and j == len(array2):
                """
                j 已到末尾
                """
                if int(array1[i]) != 0:
                    return 1
                else:
                    i = i + 1
            elif int(array1[i]) < int(array2[j]):
                return -1
            elif int(array1[i]) > int(array2[j]):
                return 1
            else:
                i = i + 1
                j = j + 1
        
        return 0
```
