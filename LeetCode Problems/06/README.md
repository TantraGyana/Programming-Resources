# [ZigZag Conversion][title]

## Description

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

**Tags:** String


## Solution

```
0                           2n-2                        4n-4
1                    2n-3   2n-1                 4n-5   4n-5
2              2n-4         2n               4n-6       .
.           .               .             .             .
.       n+1                 .          3n-1             .
n-2   n                     3n-4   3n-2                 5n-6
n-1                         3n-3                        5n-5
```

```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows <= 1) return s;
        int len = s.length();
        char[] chars = s.toCharArray();
        int cycle = 2 * (numRows - 1);
        StringBuilder sb = new StringBuilder();
        for (int j = 0; j < len; j += cycle) {
            sb.append(chars[j]);
        }
        for (int i = 1; i < numRows - 1; i++) {
            int step = 2 * i;
            for (int j = i; j < len; j += step) {
                sb.append(chars[j]);
                step = cycle - step;
            }
        }
        for (int j = numRows - 1; j < len; j += cycle) {
            sb.append(chars[j]);
        }
        return sb.toString();
    }
}
```


## 1 Using StringBuilder
```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows <= 1) return s;
        int len = s.length();
        char[] chars = s.toCharArray();
        StringBuilder[] sbs = new StringBuilder[numRows];
        for (int i = 0; i < numRows; i++) {
            sbs[i] = new StringBuilder();
        }
        int i = 0;
        while (i < len) {
            for (int j = 0; j < numRows && i < len; ++j) {
                sbs[j].append(chars[i++]);
            }
            for (int j = numRows - 2; j >= 1 && i < len; --j) {
                sbs[j].append(chars[i++]);
            }
        }
        for (i = 1; i < numRows; i++) {
            sbs[0].append(sbs[i]);
        }
        return sbs[0].toString();
    }
}
```




[title]: https://leetcode.com/problems/zigzag-conversion
[Java-leetcode]: https://github.com/Blankj/awesome-java-leetcode
