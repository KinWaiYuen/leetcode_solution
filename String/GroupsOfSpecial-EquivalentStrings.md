# Groups of Special-Equivalent Strings

@(算法)

你将得到一个字符串数组 `A`。

如果经过任意次数的移动，S == T，那么两个字符串 `S` 和 `T` 是特殊等价的。

一次移动包括选择两个索引 `i` 和 `j`，且 `i％2 == j％2`，并且交换 `S[j]` 和 `S [i]`。

现在规定，`A` 中的特殊等价字符串组是 `A` 的非空子集 `S`，这样不在 `S` 中的任何字符串与 `S` 中的任何字符串都不是特殊等价的。

返回 `A` 中特殊等价字符串组的数量。

**示例 1：**
```powershell
输入：["a","b","c","a","c","c"]
输出：3
解释：3 组 ["a","a"]，["b"]，["c","c","c"]
```

**示例 2：**
```powershell
输入：["aa","bb","ab","ba"]
输出：4
解释：4 组 ["aa"]，["bb"]，["ab"]，["ba"]
```

**示例 3：**
```powershell
输入：["abc","acb","bac","bca","cab","cba"]
输出：3
解释：3 组 ["abc","cba"]，["acb","bca"]，["bac","cab"]
```

**示例 4：**
```powershell
输入：["abcd","cdab","adcb","cbad"]
输出：1
解释：1 组 ["abcd","cdab","adcb","cbad"]
```

**提示：**

+ `1 <= A.length <= 1000`
+  `1 <= A[i].length <= 20`
+  所有 `A[i]` 都具有相同的长度。
+  所有 `A[i]` 都只由小写字母组成。


## 方法：

将奇数偶数位的字符分别拼成串，分别字典序排序，然后放到`set`去重即可。

```cpp
class Solution {
public:
    int numSpecialEquivGroups(vector<string>& A) {
        std::set<std::string> result;
        for (int i = 0; i < A.size(); i++)
        {
            std::string sEven;
            std::string sOdd;
            for (int j = 0; j < A[i].size(); j++)
            {
                if (j % 2)
                {
                    sOdd += A[i][j];
                }
                else
                {
                    sEven += A[i][j];
                }     
            }
            sort(sOdd.begin(), sOdd.end());
            sort(sEven.begin(), sEven.end());
            std::string sResult = sOdd + sEven;
            result.insert(sResult);
        }
        
        return result.size();
    }
};
```
