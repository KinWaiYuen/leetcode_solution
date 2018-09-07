# Valid Parentheses
@(算法)

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：
1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**示例 1:**
```powershell
输入: "()"
输出: true
```

**示例 2:**
```powershell
输入: "()[]{}"
输出: true
```

**示例 3:**
```powershell
输入: "(]"
输出: false
```

**示例 4:**
```powershell
输入: "([)]"
输出: false
```

**示例 5:**
```powershell
输入: "{[]}"
输出: true
```

## 方法：

没啥好讲的，大学数据结构习题

```cpp
class Solution {
public:
    bool isValid(string s) {
        std::stack<char> sStack;
        
        for (int i = 0; i < s.size(); i++)
        {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[')
            {
                sStack.push(s[i]);
            }
            else if (
                (s[i] == ')' && !sStack.empty() && sStack.top() == '(') ||
                (s[i] == ']' && !sStack.empty() && sStack.top() == '[') ||
                (s[i] == '}' && !sStack.empty() && sStack.top() == '{') )
            {
                sStack.pop();
            }
            else
            {
                return false;
            }
        }
        
        return sStack.empty() ? true : false;
    }
};
```


