# Complex Number Multiplication

@(算法)

给定两个表示复数的字符串。

返回表示它们乘积的字符串。注意，根据定义 i2 = -1 。

**示例 1:**
```powershell
输入: "1+1i", "1+1i"
输出: "0+2i"
解释: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i ，你需要将它转换为 0+2i 的形式。
```

**示例2：**
```powershell
输入: "1+-1i", "1+-1i"
输出: "0+-2i"
解释: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i ，你需要将它转换为 0+-2i 的形式。
```

**注意:**
1. 输入字符串不包含额外的空格。
2. 输入字符串将以 **a+bi** 的形式给出，其中整数 **a** 和 **b** 的范围均在 [-100, 100] 之间。**输出也应当符合这种形式**。


## 方法：

根据`(a + bi)(c + di)=(ac - bd) + (bc + ad)i`,即可。

```cpp
class Solution {
public:
    string complexNumberMultiply(string a, string b) {
        int a1 = 0;
        int b1 = 0;
        int a2 = 0;
        int b2 = 0;
        
        GetNumberFromComplex(a, a1, b1);
        GetNumberFromComplex(b, a2, b2);
        
        int result1 = a1 * a2 - b1 * b2;
        int result2 = b1 * a2 + a1 * b2;
        
        return std::to_string(result1) + "+" + std::to_string(result2) + "i";
    }
    
    void GetNumberFromComplex(string word, int & a1, int & b1)
    {
        a1 = 0;
        b1 = 0;
        bool bAfter = false;
        int iNegativeBefore = 1;
        int iNegativeAfter = 1;
        
        for (int i = 0; i < word.length(); i++)
        {
            if (word[i] == '+')
            {
                bAfter = true;
            }
            
            if (word[i] == '-' && bAfter)
            {
                iNegativeAfter = -1;
            }
            else if (word[i] == '-' && !bAfter)
            {
                iNegativeBefore = -1;
            }
            
            if (word[i] >= '0' && word[i] <= '9' && bAfter)
            {
                b1 = b1 * 10 + (word[i] - '0');
            }
            else if (word[i] >= '0' && word[i] <= '9' && !bAfter)
            {
                a1 = a1 * 10 + (word[i] - '0');
            }
        }
        
        a1 *= iNegativeBefore;
        b1 *= iNegativeAfter;
    }
};
```
