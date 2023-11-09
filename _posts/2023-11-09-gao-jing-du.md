---
layout:     post
title:      高精度
subtitle:   Bigint
date:       2023-11-09
author:     chicken2011
header-img: img/the-first.png
catalog:   true
tags:
    - OI
---

```cpp
struct BigInt {
	int a[2000];
	int len;
	BigInt(string s = "0") {
		memset(a, 0, sizeof(a));
		len = s.size();
		for (int i = 0; i < len; i++) {
			a[i] = s[len - i - 1] - '0';
		}
	}
	BigInt(long long x) {
		char cc[2000];
		sprintf(cc, "%lld", x);
		string s = cc;
		*this = s;
	}
	BigInt(int x) {
		char cc[2000];
		sprintf(cc, "%d", x);
		string s = cc;
		*this = s;
	}
	friend const int comp(const BigInt &a, const BigInt &b) {
		if (a.len > b.len) {
			return 1;
		}
		if (a.len < b.len) {
			return -1;
		}
		for (int i = a.len - 1; i >= 0; i--) {
			if (a.a[i] > b.a[i])return 1;
			if (a.a[i] < b.a[i])return -1;
		}
		return 0;
	}
	friend inline bool operator<(const BigInt& a, const BigInt &b) {
		return comp(a, b) == -1;
	}
	friend inline bool operator>(const BigInt& a, const BigInt &b) {
		return comp(a, b) == 1;
	}
	friend inline bool operator==(const BigInt& a, const BigInt &b) {
		return comp(a, b) == 0;
	}
	friend inline bool operator!=(const BigInt& a, const BigInt &b) {
		return comp(a, b) != 0;
	}
	friend inline bool operator<=(const BigInt& a, const BigInt &b) {
		return comp(a, b) != 1;
	}
	friend inline bool operator>=(const BigInt& a, const BigInt &b) {
		return comp(a, b) != -1;
	}
	friend const BigInt operator+(const BigInt &a, const BigInt &b) {
		BigInt ans;
		ans.len = max(a.len, b.len);
		for (int i = 0; i < ans.len; i++) {
			ans.a[i] += a.a[i] + b.a[i];
			ans.a[i + 1] += ans.a[i] / 10;
			ans.a[i] %= 10;
		}
		if (ans.a[ans.len])ans.len++;
		return ans;
	}
	friend const BigInt operator-(BigInt a, BigInt b) {
		for (int i = 0; i < a.len; i++) {
			a.a[i] -= b.a[i];
			if (a.a[i] < 0) {
				a.a[i + 1]--;
				a.a[i] += 10;
			}
		}
		for (; a.a[a.len - 1] == 0 && a.len > 1; a.len--);
		return a;
	}
	friend const BigInt operator*(const BigInt &a, const BigInt &b) {
		BigInt ans;
		ans.len = a.len + b.len;
		for (int i = 0; i < a.len; i++) {
			for (int j = 0; j < b.len; j++) {
				ans.a[i + j] += a.a[i] * b.a[j];
			}
		}
		for (int i = 0; i < ans.len; i++) {
			ans.a[i + 1] += ans.a[i] / 10;
			ans.a[i] %= 10;
		}
		for (; ans.a[ans.len - 1] == 0 && ans.len > 1; ans.len--);
		return ans;
	}
	friend const BigInt operator/(const BigInt &a, const BigInt &b) {
		BigInt sum = 0, ans = 0;
		ans.len = a.len;
		for (int i = a.len - 1; i >= 0; i--) {
			sum = sum * 10 + a.a[i];
			while (comp(sum, b) != -1) {
				sum = sum - b;
				ans.a[i]++;
			}
		}
		for (; ans.a[ans.len - 1] == 0 && ans.len > 1; ans.len--);
		return ans;
	}
	friend istream& operator>>(istream& is, BigInt &a) {
		string s;
		is >> s;
		a = s;
		return is;
	}
	friend ostream& operator<<(ostream& os, const BigInt &a) {
		for (int i = a.len - 1; i >= 0; i--)os << a.a[i];
		return os;
	}
};
```
