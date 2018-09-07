# String Compression
@(算法)

给定一组字符，使用原地算法将其压缩。

压缩后的长度必须始终小于或等于原数组长度。

数组的每个元素应该是长度为1 的字符（不是 int 整数类型）。

在完成原地修改输入数组后，返回数组的新长度。

**进阶:**
你能否仅使用O(1) 空间解决问题？

**示例 1：**
```powershell
输入：
["a","a","b","b","c","c","c"]

输出：
返回6，输入数组的前6个字符应该是：["a","2","b","2","c","3"]

说明：
"aa"被"a2"替代。"bb"被"b2"替代。"ccc"被"c3"替代。
```

**示例 2：**
```powershell
输入：
["a"]

输出：
返回1，输入数组的前1个字符应该是：["a"]

说明：
没有任何字符串被替代。
```

**示例 3：**
```powershell
输入：
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

输出：
返回4，输入数组的前4个字符应该是：["a","b","1","2"]。

说明：
由于字符"a"不重复，所以不会被压缩。"bbbbbbbbbbbb"被“b12”替代。
注意每个数字在数组中都有它自己的位置。
```

**注意：**
1. 所有字符都有一个ASCII值在`[35, 126]`区间内。
2. `1 <= len(chars) <= 1000。`


## 方法：

没啥好讲的，一边遍历，一边找到不同的元素然后同时修改前面的元素即可（利用另外一个追踪下标）

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        char index = 0;
        int result = 0;
        int num = 0;
        int modifyIndex = 0;
        int start = 0;
        int end = 0;
        int iTmpDigit = 0;
        for (int i = 0; i < chars.size(); i++)
        {
            if (!index)
            {
                index = chars[i];
            }
            
            if (chars[i] != index)
            {
                chars[modifyIndex++] = index;
                iTmpDigit = 0;
                start = modifyIndex;
                if (num > 1)
                {
                    while (num)
                    {
                        iTmpDigit++;
                        chars[modifyIndex++] = '0' + num % 10;
                        num /= 10;
                    }
                }
                end = modifyIndex;
                std::reverse(chars.begin() + start, chars.begin() + end);
                result += 1 + iTmpDigit;
                index = chars[i];
                num = 1;
            }
            else
            {
                num++;
            }
        }
        
        chars[modifyIndex++] = index;
        iTmpDigit = 0;
        start = modifyIndex;
        if (num > 1)
        {
            while (num)
            {
                iTmpDigit++;
                chars[modifyIndex++] = '0' + num % 10;
                num /= 10;
            }
        }
        end = modifyIndex;
        std::reverse(chars.begin() + start, chars.begin() + end);
        result += 1 + iTmpDigit;
        chars.erase(chars.begin() + modifyIndex, chars.end());
                
        return result;
    }

};
```
