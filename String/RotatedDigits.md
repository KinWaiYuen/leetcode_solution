# Rotated Digits

@(算法)

我们称一个数 X 为好数, 如果它的每位数字逐个地被旋转 180 度后，我们仍可以得到一个有效的，且和 X 不同的数。要求每位数字都要被旋转。

如果一个数的每位数字被旋转以后仍然还是一个数字， 则这个数是有效的。0, 1, 和 8 被旋转后仍然是它们自己；2 和 5 可以互相旋转成对方；6 和 9 同理，除了这些以外其他的数字旋转以后都不再是有效的数字。

现在我们有一个正整数 `N`, 计算从 `1` 到 `N` 中有多少个数 X 是好数？

```powershell
示例:
输入: 10
输出: 4
解释: 
在[1, 10]中有四个好数： 2, 5, 6, 9。
注意 1 和 10 不是好数, 因为他们在旋转之后不变。
```

**注意：**
+ N 的取值范围是 `[1, 10000]`。

## 方法一：非字符串解法

不使用字符串方法解题。

```cpp
class Solution {
public:
    int rotatedDigits(int N) {
        int num = 0;
        for (int i = 1; i <= N; i++)
        {
            if (isRotateDigit(i))
            {
                num++;
            }
        }
        return num;
    }
    
    bool isRotateDigit(int N)
    {
        bool bFlag = false;
        while (N)
        {
            int digit = N % 10;
            if (digit == 2 || digit == 5 || digit == 6 || digit == 9)
            {
                bFlag = true;
            }
            else if (digit == 3 || digit == 4 || digit == 7)
            {
                return false;
            }
            N /= 10;
        }
        
        return bFlag;
    }
};
```

## 方法二：字符串解法

通过将`[1, N]`中的每一位转化为字符串，然后判断满足下面两个条件的数均为“好数”。

+ 含有2, 5, 6, 9的其中一位；
+ 不含有3, 4, 7的每一位。

```cpp
class Solution {
public:
    int rotatedDigits(int N) {
        int num = 0;
        
        for (int i = 1; i <= N; i++)
        {
            // 使用C++11的to_string方法，将数字转成字符串
            std::string sDigit = std::to_string(i);
            
            // 含有2,5,6,9且不能含有3,4,7的数则视为好数
            if (
                (
                    sDigit.find("2") != std::string::npos ||
                    sDigit.find("5") != std::string::npos ||
                    sDigit.find("6") != std::string::npos ||
                    sDigit.find("9") != std::string::npos
                ) 
                &&
                (
                    sDigit.find("3") == std::string::npos &&
                    sDigit.find("4") == std::string::npos &&
                    sDigit.find("7") == std::string::npos
                )
            )
            {
                num++;
            }
        }
        
        return num;
        
    }
};
```


## 方法三：动态规划法

这题可以用动态规划来做：

对于 `0~9`，做以下判断：
+ `0,1,8，dp[i] = 1`;
+ `2,5,6,9，dp[i] = 2`;
+ `3,4,7, dp[i] = 0`；

对于 `i >= 10`，`dp[i]`的值取决于`dp[i % 10]`，`dp[i / 10]`。
+ `dp[i % 10]`或者`dp[i / 10]`为`0`的时候，`dp[i]`也为`0`；
+ `dp[i % 10]`为`1`且`dp[i / 10]`为`1`的时候，`dp[i]`为`1`；
+ `dp[i % 10]`和`dp[i / 10]`为1，2组合或者2，2组合的时候，`dp[i]`也为`2`。

```cpp
class Solution {
public:
    int rotatedDigits(int N) {
        int num = 0;
        std::vector<int> dp(N+1);
        
        for (int i = 0; i <= N; i++)
        {
            // 0,1,8——一类数，旋转后相等
            // 2,5,6,9——二类数，旋转后是好数
            // 3,4,7——三类数，旋转后无效数
            if (i < 10)
            {
                if (i == 0 || i == 1 || i == 8)
                {
                    dp[i] = 1;
                }
                else if (i == 2 || i == 5 || i == 6 || i == 9)
                {
                    dp[i] = 2;
                    num++;
                }
                // 剩余默认为0
            }
            else
            {
                if (dp[i / 10] == 1 && dp[i % 10] == 1)
                {
                    dp[i] = 1;
                }
                else if (dp[i / 10] >= 1 && dp[i % 10] >= 1)
                {
                    dp[i] = 2;
                    num++;
                }
            }   
        }
        
        return num;
        
    }
};
```
