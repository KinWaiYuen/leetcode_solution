# Judge Route Circle

@(算法)

初始位置 (0, 0) 处有一个机器人。给出它的一系列动作，判断这个机器人的移动路线是否形成一个圆圈，换言之就是判断它是否会移回到**原来的位置**。

移动顺序由一个字符串表示。每一个动作都是由一个字符来表示的。机器人有效的动作有 `R`（右），`L`（左），`U`（上）和 `D`（下）。输出应为 true 或 false，表示机器人移动路线是否成圈。

**示例 1:**

```powshell
输入: "UD"
输出: true
```

**示例 2:**

```powershell
输入: "LL"
输出: false
```

## 方法：

比较简单。

```cpp
class Solution {
public:
    bool judgeCircle(string moves) {
        int iXaxis = 0;
        int iYaxis = 0;
        for (auto c : moves)
        {
            switch (c)
            {
                case 'R':
                    iXaxis++;
                    break;
                case 'L':
                    iXaxis--;
                    break;
                case 'U':
                    iYaxis++;
                    break;
                case 'D':
                    iYaxis--;
                    break;
            } 
        }
        
        return (!iXaxis && !iYaxis) ? true : false;
    }
};
```
