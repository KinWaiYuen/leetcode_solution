# *Buddy Strings*

@(算法)

给定两个由小写字母构成的字符串 `A` 和 `B` ，只要我们可以通过交换 `A` 中的两个字母得到与 `B` 相等的结果，就返回 `true` ；否则返回 `false` 。

**示例 1：**
```powershell
输入： A = "ab", B = "ba"
输出： true
```

**示例 2：**
```powershell
输入： A = "ab", B = "ab"
输出： false
```

**示例 3:**
```powershell
输入： A = "aa", B = "aa"
输出： true
```

**示例 4：**
```powershell
输入： A = "aaaaaaabc", B = "aaaaaaacb"
输出： true
```

**示例 5：**
```powershell
输入： A = "", B = "aa"
输出： false
```

**提示：**
1. `0 <= A.length <= 20000`
2. `0 <= B.length <= 20000`
3. `A` 和 `B` 仅由小写字母构成。  


## 方法：

思路并不复杂，但是我对`aa`和`aa`这种情况的考虑并不简洁，后面看了别人的答案才发现别人通过引入`set`数据结构，然后比较`setDiff`和`vecDiff`的个数大小来看是否具有重复字符，因为有重复字符的话，也是可以通过交换等价的。这里值得记住。

### 我的方法：
```cpp
class Solution {
public:
    bool buddyStrings(string A, string B) {
        std::size_t lenA = A.length();
        std::size_t lenB = B.length();
        
        if (lenA != lenB) return false;
        
        int iDiff = 0;
        
        char diffA = 0;
        char diffB = 0;
        
        for (int i = 0; i < lenA; i++)
        {
            if (A[i] != B[i])
            {
                iDiff++;
                
                if (iDiff > 2)
                {
                    return false;
                }
                else if ((iDiff == 2) && (diffA != B[i] || diffB != A[i]))
                {
                    return false;
                }
                else if (iDiff == 1)
                {
                    diffA = A[i];
                    diffB = B[i];
                }
            }
        }
        
        if (iDiff == 0)
        {
            for (int i = 0; i < lenA; i++)
            {
                if (std::count(A.begin(), A.end(), A[i]) % 2 == 0)
                {
                    return true;
                }
            }
        }
        
        return iDiff == 2 ? true : false;
    }
};
```


### 引入set方法：

```cpp
class Solution {
public:
    bool buddyStrings(string A, string B) {
        if (A.length() != B.length()) return false;
        if (A.length() == 0) return false;
        
        std::vector<int> vecDiff;
        for (int i = 0; i < A.length(); i++)
        {
            if (A[i] != B[i])
            {
                vecDiff.push_back(i);  // 记住下标
            }
        }
        
        if (vecDiff.size() == 2)
        {
            if (A[vecDiff[0]] == B[vecDiff[1]] && A[vecDiff[1]] == B[vecDiff[0]])
            {
                return true;
            }
        }
        
        if (vecDiff.size() == 0)
        {
            std::set<char> setA;
            for (int i = 0; i < A.length(); i++)
            {
                setA.insert(A[i]);
            }
            if (setA.size() != A.length()) return true;
        }
        
        return false;
    }
};
```
