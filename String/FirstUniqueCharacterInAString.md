# First Unique Character in a String
@(算法)

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**
```powershell
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```


**注意事项：** 您可以假定该字符串只包含小写字母。

## 方法：

没啥好讲的，直接find两次即可。哈希表也可以做，但是没那么简洁。

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        int index = -1;
        
        for (int i = 0; i < s.size(); i++)
        {
            size_t found = s.find(s[i]);
            
            if (s.find(s[i], found + 1) != std::string::npos)
            {
                continue;
            }
            else
            {
                return i;
            }
        }
        
        return index;
    }
};
```

