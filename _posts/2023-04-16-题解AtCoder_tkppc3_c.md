
# 题目大意
给你一个长度为 $n$ 的正整数数列 $a$ ，再给出一个 $p$ ，问你 $a$ 中是否存在**连续**的一段数乘积为 $p$ ，如果存在，输出 "Yay!" ，否则输出 ":(" 。

# 解析
我们可以把一部分的数都乘一下。
```cpp
ans*=a[i];
```
 
如果结果等于了 $p$ ，那么输出 "Yay!"，然后结束。
```cpp
if(ans==p){
    cout<<"Yay!";
    return 0;
}
```

如果结果大于了 $p$ ，那么将结果与前面的数相除。
```cpp
while(ans>p) ans/=a[++siz];
```


如果乘积已经小于 $p$ ，那么进行下一次循环，什么都不写。

# 注意点
- 必须开 `long long` 。
- 输出 "Yay!" 以后记得 `return 0` 。

# 代码
为了大家的安全起见，请不要抄代码，但你可以按我的思路自己打一遍。
```cpp
#include<bits/stdc++.h> // 万能头我的最爱
using namespace std; // 使用命名空间
typedef long long ll; // 你想见祖宗吗？
ll n,p,a[100005];
ll ans=1,siz=0;
int main(){ // 主函数
    ios_base::sync_with_stdio(false); // 断开cin,scanf连接
    cin.tie(NULL),cout.tie(NULL); // cin,cout加速
    cin>>n>>p;
    for(int i=1;i<=n;i++) cin>>a[i];
    for(int i=1;i<=n;i++){
        ans*=a[i];
        while(ans>p) ans/=a[++siz]; // 大于
        if(ans==p){ // 如果等于了，即存在，那么输出"Yay!"
            cout<<"Yay!";
            return 0; // 直接结束
        }
    }
    cout<<":("; // 如果不存在，输出":("
    return 0; // 好习惯
}
```
