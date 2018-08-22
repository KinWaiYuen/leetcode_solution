# Student Attendance Record I

@(算法)

给定一个字符串来代表一个学生的出勤纪录，这个纪录仅包含以下三个字符：

1. **'A'** : Absent，缺勤
2. **'L'** : Late，迟到
3. **'P'** : Present，到场
如果一个学生的出勤纪录中**不超过一个'A'(缺勤)并且不超过两个连续的'L'(迟到)**,那么这个学生会被奖赏。

你需要根据这个学生的出勤纪录判断他是否会被奖赏。

**示例 1:**
```powershell
输入: "PPALLP"
输出: True
```

**示例 2:**
```powershell
输入: "PPALLL"
输出: False
```

## 方法：

```python
class Solution(object):
    def checkRecord(self, s):
        """
        :type s: str
        :rtype: bool
        """
        return True if s.count("A") <= 1 and s.count("LLL") == 0 else False;
```
