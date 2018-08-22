# Count and Say

@(算法)

报数序列是指一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

```powershell
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` 被读作  `"one 1"`  (`"一个一"`) , 即 `11`。
`11` 被读作 `"two 1s"` (`"两个一"`）, 即 `21`。
`21` 被读作 `"one 2"`,  `"one 1"` （`"一个二"` ,  `"一个一"`) , 即 `1211`。

给定一个正整数 n ，输出报数序列的第 n 项。

注意：整数顺序将表示为一个字符串。

**示例 1:**
```powershell
输入: 1
输出: "1"
```

**示例 2:**
```powershell
输入: 4
输出: "1211"
```

## 方法：

没啥好讲的，转换方法就是判断不同的数字有多少个，然后以个数+数字的方式连接起来。

```cpp
class Solution {
public:
    string countAndSay(int n) {
        std::string start = "1";
        std::string tmp;
        int num = 0;
        for (int i = 0; i < n - 1; i++)
        {
            tmp.clear();
            num = 0;
            for (int j = 0; j < start.length(); j++)
            {
                num++;
                if (j != start.length() -1 && start[j] != start[j+1])
                {
                    tmp += std::to_string(num) + start[j];
                    num = 0;
                }
            }
            tmp += std::to_string(num) + start[start.length() -1];
            start = tmp;
            
        }
        return start;
    }
};
```
