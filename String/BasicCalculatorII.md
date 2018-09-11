# Basic Calculator II

@(算法)

实现一个基本的计算器来计算一个简单的字符串表达式的值。

字符串表达式仅包含非负整数，+， - ，*，/ 四种运算符和空格  。 整数除法仅保留整数部分。

**示例 1:**
```powershell
输入: "3+2*2"
输出: 7
```

**示例 2:**
```powershell
输入: " 3/2 "
输出: 1
```

**示例 3:**
```powershell
输入: " 3+5 / 2 "
输出: 5
```

**说明：**
+ 你可以假设所给定的表达式都是有效的。
+ 请**不要**使用内置的库函数 `eval`。


## 方法：

从头遍历一次即可，注意`*`和`/`的处理，具备优先级，需要先计算。这里没有`(`，`)`，处理起来相对简单。

```cpp
class Solution {
public:
    int calculate(string s) {
        char cOperator = '+';
        int num = 0;
        int result = 0;
        std::stack<int> sValue;
        
        for (int i = 0; i < s.length(); i++)
        {
            if (s[i] >= '0')
            {
                num = num * 10 + (s[i] - '0');
            }
            
            if ((s[i] < '0' && s[i] != ' ') || i == s.length() - 1)
            {
                switch(cOperator)
                {
                    case '+':
                        sValue.push(num);
                        break;
                    case '-':
                        sValue.push(-num);
                        break;
                    case '*':
                        {
                            int iTop = sValue.top();
                            sValue.pop();
                            sValue.push(iTop * num);
                        }
                        break;
                    case '/':
                        {
                            int iTop = sValue.top();
                            sValue.pop();
                            sValue.push(iTop / num);
                        }
                        break;  
                }
                cOperator = s[i];
                num = 0;
            }
        }
        
        while (!sValue.empty())
        {
            cout << sValue.top() << endl;
            result += sValue.top();
            sValue.pop();
        }
        
        return result;
    }
};
```
