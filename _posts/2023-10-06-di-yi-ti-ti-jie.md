---
layout:     post
title:      国庆模拟考第一题题解
subtitle:   题解
date:       2023-10-06
author:     chicken2011
header-img: img/the-first.png
catalog:   true
tags:
    - OI
---

从左到右遍历每个字符，如果这个字符是 s，下一个字符是 f，那就调换位置，`break;`。

代码：
```cpp
#include <bits/stdc++.h>
using namespace std;

string s;

int main() {
    //freopen("string.in", "r", stdin);
    //freopen("string.out", "w", stdout);
    cin >> s;
    for (int i = 0; i < s.size() - 1; i++) {
        if (s[i] == 'f' && s[i + 1] == 's') {
            char t = s[i];
            s[i] = s[i + 1];
            s[i + 1] = t;
            break;
        }
    }
    cout << s;
    
    return 0;
}
```
