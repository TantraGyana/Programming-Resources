# [Longest Palindromic Substring][title]

## Description

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"

Output: "bb"
```

**Tags:** String, Dynamic Programming


## Solution 0

Complexity: O(n^2)

```java
class Solution {
    int st, end;

    public String longestPalindrome(String s) {
        int len = s.length();
        if (len <= 1) return s;
        char[] chars = s.toCharArray();
        for (int i = 0; i < len; i++) {
            helper(chars, i, i);
            helper(chars, i, i + 1);
        }
        return s.substring(st, end + 1);
    }

    private void helper(char[] chars, int l, int r) {
        while (l >= 0 && r < chars.length && chars[l] == chars[r]) {
            --l;
            ++r;
        }
        if (end - st < r - l - 2) {
            st = l + 1;
            end = r - 1;
        }
    }
}
```


## Solution 1 

1. if `i == j`  and `dp[i][j] = true`；

2. if `i + 1 == j` and `dp[i][j]` , `s[i] == s[j]`；

3.  if `i + 1 < j` then `dp[i][j]` else `dp[i + 1][j - 1] && s[i] == s[j]`

Complexity  `O(n^2)`

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len <= 1) return s;
        int st = 0, end = 0;
        char[] chars = s.toCharArray();
        boolean[][] dp = new boolean[len][len];
        for (int i = 0; i < len; i++) {
            dp[i][i] = true;
            for (int j = 0; j < i; j++) {
                if (j + 1 == i) {
                    dp[j][i] = chars[j] == chars[i];
                } else {
                    dp[j][i] = dp[j + 1][i - 1] && chars[j] == chars[i];
                }
                if (dp[j][i] && i - j > end - st) {
                    st = j;
                    end = i;
                }
            }
        }
        return s.substring(st, end + 1);
    }
}
```




[title]: https://leetcode.com/problems/longest-palindromic-substring
[ajl]: https://github.com/Blankj/awesome-java-leetcode
