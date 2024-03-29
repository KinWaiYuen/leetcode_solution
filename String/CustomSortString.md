# Custom Sort String

@(算法)

字符串`S`和 `T` 只包含小写字符。在`S`中，所有字符只会出现一次。

`S` 已经根据某种规则进行了排序。我们要根据`S`中的字符顺序对`T`进行排序。更具体地说，如果`S`中`x`在`y`之前出现，那么返回的字符串中`x`也应出现在`y`之前。

返回任意一种符合条件的字符串`T`。

```powershell
示例:
输入:
S = "cba"
T = "abcd"
输出: "cbad"
解释: 
S中出现了字符 "a", "b", "c", 所以 "a", "b", "c" 的顺序应该是 "c", "b", "a". 
由于 "d" 没有在S中出现, 它可以放在T的任意位置. "dcba", "cdba", "cbda" 都是合法的输出。
```

**注意：**
+ `S`的最大长度为`26`，其中没有重复的字符。
+ `T`的最大长度为`200`。
+ `S`和`T`只包含小写字符。

## 方法：哈希表法

```cpp
class Solution {
public:
    string customSortString(string S, string T) {
        std::map<char, int> mapSource;
        
        for (int i = 0; i < S.length(); i++)
        {
            mapSource[S[i]] = i;
        }
        
        // 根据mapSource的顺序进行排序
        for (int i = 0; i < T.length() - 1; i++)
        {
            for (int j = i + 1; j < T.length(); j++)
            {
                int tmpBefore = -1;
                if (mapSource.find(T[i]) != mapSource.end())
                {
                    tmpBefore = mapSource[T[i]];
                }
                int tmpAfter = -1;
                if (mapSource.find(T[j]) != mapSource.end())
                {
                    tmpAfter = mapSource[T[j]];
                }
                
                if (tmpAfter < tmpBefore)
                {
                    char chTmp = T[i];
                    T[i] = T[j];
                    T[j] = chTmp;
                }
            }
        }
        return T;
    }
};
```
