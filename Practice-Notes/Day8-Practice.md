# 📝 LeetCode 学习日志 Day 8

<br>

## 151. 翻转字符串里的单词
- 题目链接：[**LeetCode 151. Reverse Words in a String**](https://leetcode.com/problems/reverse-words-in-a-string/)
- 关键词：**String, Two Pointers**  

<br>

## 💡 思路
这道题比较的繁琐，主要是有三个步骤：
 
 - 去除掉多余的空格：
     - 设定一个start指向string的开始，end指向string的末尾，先去除开始和结尾的空格，当start指向第一个字母和end指向最后一个字母时，创建一个新的StringBuilder，将所有字母加入进去，中间多的空格跳过。

 - 反转整个String：
     - 跟swap一样。

 - 反转每个单词：采用双指针的办法，设定start = 0， end = 1，然后先让end找到单词末尾的空格，然后在这个范围里进行反转整个String，然后移动start和end直至start和end到结尾。

<br>

## 💻 代码实现
```java
class Solution {
    public String reverseWords(String s) {
        StringBuilder sb = removeExtraSpace(s);
        reverseString(sb, 0, sb.length() - 1);
        reverseEachWord(sb);
        return sb.toString();
    }

    private StringBuilder removeExtraSpace(String s){
        int start = 0;
        int end = s.length() -1;
        while(s.charAt(start) == ' ') start++;
        while(s.charAt(end) == ' ') end--;
        StringBuilder sb = new StringBuilder();
        while(start <= end){
            char c = s.charAt(start);
            if(c != ' ' || s.charAt(start - 1) != ' '){
                sb.append(c);
            }
            start++;
        }
        return sb;
    }

    public void reverseString(StringBuilder sb, int start, int end){
        while(start < end){
            char temp = sb.charAt(start);
            sb.setCharAt(start, sb.charAt(end));
            sb.setCharAt(end, temp);
            start++;
            end--;
        }
    }

    public void reverseEachWord(StringBuilder sb){
        int start = 0;
        int end = 1;
        int n = sb.length();
        while(start < n){
            while(end < n && sb.charAt(end) != ' ') end++;
            reverseString(sb, start, end-1);
            start = end + 1;
            end = start + 1;
        }
    }
}
```

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        words = s.split()
        words.reverse()
        return " ".join(words)
```

<br>

## 28. 实现 strStr()
- 题目链接：[**LeetCode 28. Find the Index of the First Occurance in a String**](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
- 关键词：**KMP Algorithm**

<br>

## 💡 思路
这道题是非常经典用到KMP算法的，KMP主要运用在字符串匹配上，KMP的主要思想是**当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了**。KMP算法是相当有难度去理解的，主要运用到的就是Next数组，也就是前缀表。

Next数组该如何实现呢？在这道题当中，设定一个指针指向前缀的末尾，另一个指针循环指向后缀的末尾，当前后缀末尾相等时，前缀末尾指针increment,直至最后，这样模式串的前缀表就生成好了。

然后开始进行字符串匹配，当出现字符串不匹配时，模式串会跳回之前一个index前缀的字符来继续进行匹配。

这就是KMP的算法精髓了。

<br>

## 💻 代码实现
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0) return 0;
        int[] next = new int[needle.length()];
        getNext(next, needle);

        int j = 0;
        for(int i = 0; i < haystack.length(); i++){
            while(j > 0 && needle.charAt(j) != haystack.charAt(i)){
                j = next[j - 1];
            }
            if(needle.charAt(j) == haystack.charAt(i)){
                j++;
            }
            if(j == needle.length()){
                return i - needle.length() + 1;
            }
        }
        return -1;
    }

    public void getNext(int[] next, String needle){
        int j = 0;
        next[0] = 0;
        for(int i = 1; i < needle.length(); i++){
            while(j > 0 && needle.charAt(i) != needle.charAt(j)){
                j = next[j-1];
            }
            if(needle.charAt(i) == needle.charAt(j)){
                j++;
            }
            next[i] = j;
        }
    }
}
```

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        n= len(haystack)
        m = len(needle)

        for i in range(n - m + 1):
            if haystack[i:i+m] == needle:
                return i
        return -1
```

<br>

## 459. 重复的子字符串
- 题目链接：[**LeetCode 459. Repeated Substring Pattern**](https://leetcode.com/problems/repeated-substring-pattern/)
- 关键词：**KMP Algorithm**

<br>

## 💡 思路
这道题同28一样也是运用到了KMP算法。关于KMP算法的应用可以详细看28题。

这道题先创建了next数组表，然后看最后一个数字的前缀是否满足重复：
 - 是否大于0
 - 整个长度减去前缀之后是否还能被整个长度整除

<br>

## 💻 代码实现
```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int[] next = new int[s.length()];
        int j = 0;
        int n = s.length();
        next[0] = 0;
        for(int i = 1; i < n; i++){
            while(j > 0 && s.charAt(i) != s.charAt(j)){
                j = next[j-1];
            }
            if(s.charAt(i) == s.charAt(j)){
                j++;
            }
            next[i] = j;
        }
        
        if (next[n - 1] > 0 && n % (n - next[n - 1]) == 0) {
            return true; 
        } 
        else {
            return false;
        }
    }
}
```

```python
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        return s in (s+s)[1:-1]
```

<br>

## 📝 今日心得
今天的这两道KMP算法相当有难度，有时间时需要多复习加深印象，主要就是要理解Next数组是如何计算的，然后回退到前缀的index又是具体怎么操作的，第一次不理解没关系，重复多次硬啃下来还是可以的。