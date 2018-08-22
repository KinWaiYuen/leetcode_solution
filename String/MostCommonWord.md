# Most Common Word

@(算法)

给定一个段落 (paragraph) 和一个禁用单词列表 (banned)。返回出现次数最多，同时不在禁用列表中的单词。题目保证至少有一个词不在禁用列表中，而且答案唯一。

禁用列表中的单词用小写字母表示，不含标点符号。段落中的单词不区分大小写。答案都是小写字母。

```powershell
示例:
输入: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
输出: "ball"
解释: 
"hit" 出现了3次，但它是一个禁用的单词。
"ball" 出现了2次 (同时没有其他单词出现2次)，所以它是段落里出现次数最多的，且不在禁用列表中的单词。 
注意，所有这些单词在段落里不区分大小写，标点符号需要忽略（即使是紧挨着单词也忽略， 比如 "ball,"）， 
"hit"不是最终的答案，虽然它出现次数更多，但它在禁用单词列表中。
```

**说明:**

+ `1 <= 段落长度 <= 1000`.
+ `1 <= 禁用单词个数 <= 100`.
+ `1 <= 禁用单词长度 <= 10`.
+ 答案是唯一的, 且都是小写字母 (即使在 `paragraph` 里是大写的，即使是一些特定的名词，答案都是小写的。)
+ `paragraph` 只包含字母、空格和下列标点符号`!?',;.`
+ `paragraph` 里单词之间都由空格隔开。
+ 不存在没有连字符或者带有连字符的单词。
+ 单词里只包含字母，不会出现省略号或者其他标点符号。


## 方法

```python
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        """
        :type paragraph: str
        :type banned: List[str]
        :rtype: str
        """
        result_map = {}
        clean = lambda x : x.strip("!?',;.")
        result_set = map(clean, paragraph.split(" "))
        for word in result_set:
            if word.lower() not in banned and word.lower() not in result_map.keys():
                result_map[word.lower()] = 1
            elif word.lower() not in banned and word.lower() in result_map.keys():
                result_map[word.lower()] += 1
            
        return max(result_map.items(), key=lambda x: x[1])[0]
```

**后面发现原来`python`有计数器这一数据结构，孤陋寡闻了。**

```python
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        """
        :type paragraph: str
        :type banned: List[str]
        :rtype: str
        """
        tokens = re.sub('[\!\?\'\,;\.]', '', paragraph.lower()).split()
        cnt = collections.Counter(tokens)
        for ban in banned:
            if ban in cnt:
                del cnt[ban]
        return cnt.most_common(1)[0][0]
```
