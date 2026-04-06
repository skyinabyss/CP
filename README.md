# ÔN THI TIN
## 1. Prefix sum + mảng đánh dấu
* **trick cộng và tick**
    - lưu ý khi nào cộng trước, khi nào tick trước
    - lưu ý khi nào dùng map khi nào dùng mảng để đánh dấu
    - list bài
        + https://lqdoj.edu.vn/problem/cppb2p112
        + https://lqdoj.edu.vn/problem/cntpair0sum
        + https://lqdoj.edu.vn/problem/cpair
        + ...
* **trick kiểm tra số lượng trong một đoạn**
    - lưu ý biến đổi phần tử cần đếm thành giá trị có nghĩa và các phần từ còn lại thành không có nghĩa.
    - lưu ý giới hạn giá trị của phần tử mảng.
    - lưu ý dùng đánh dấu mảng cộng dồn thì $cnt[0] = 1$
    - list bài
        + https://lqdoj.edu.vn/problem/24hsg9dna3
        + https://lqdoj.edu.vn/problem/countchar
        + https://lqdoj.edu.vn/problem/minict06
        + ...

## 2. Toán
* **Form code**
```cpp
bool snt[100000001]; 
void era(int n) // có thể sàng lên tới 1e7;
{
	snt[1] = 1;
	for (int i=1;i*i<=n;i++)
	{
		if (snt[i]) continue;
		for (int j=i*i;j<=n;j+=i) snt[j] = 1;
	}
}

long long gcd(long long a, long long b)
{
    if (b==0) return a;
    return gcd(b,a%b);
}

long long lcm(long long a, long long b)
{
    return a/gcd(a,b)*b; // chia trước nhân sau.
}
```
* **số nguyên tố, sàng nguyên tố, đếm ước, sàng ước, phân tích thành thừa số nguyên tố ...**
    - Lưu ý khi nào dùng sàng, khi nào không dùng
    - list bài
        + https://lqdoj.edu.vn/problem/cppb2p302
        + https://lqdoj.edu.vn/problem/factor
        + https://lqdoj.edu.vn/problem/factor02004
        + https://lqdoj.edu.vn/problem/natdiv20
        + ...

* **đếm số chia hết cho n, số chia hết cho a hoặc b, số chia hết chỉ cho a hoặc b, số chính phương...**
    - Lưu ý đọc kĩ yêu cầu chia hết cho cả 2 hay là phải từng số
    - List bài
        + https://lqdoj.edu.vn/problem/25hsg9dna2
        + https://lqdoj.edu.vn/problem/25hsg9nab1
        + https://lqdoj.edu.vn/problem/25hsg9bgi1
        + https://lqdoj.edu.vn/problem/24hvab4
        + ...

* **Tính chia hết**
    -  Lưu ý sử dụng tính chất của phép mod đối với phép trừ (hay áp dụng vào prefix sum) như sau
    ```math
    \begin{cases}
    a \bmod m = r \\
    b \bmod m = r
    \end{cases}
    \Rightarrow (a-b) \bmod m = 0
    ```

    - Lưu ý sử dụng tính chất của phép mod đối với phép cộng (áp dụng cho tìm cặp số)
    ```math
    \begin{cases}
    a \bmod m = r_1 \\
    b \bmod m = r_2 \\
    r_1 + r_2 = m
    \end{cases}
    \Rightarrow (a + b) \bmod m = 0
    ```

    - List bài
        + https://lqdoj.edu.vn/problem/cses1662
        + ...

## 3. Chặt nhị phân
* **Form Code**
```cpp
int l,r;
int res = -1 //(Giá trị vô lý để check nếu không tìm được)
while (l<=r)
{
    int m = (l+r) / 2;
    if ("điều kiện đúng")
    {
        res = m; // lưu giá trị đúng
        r = m - 1; // nếu bỏ bên phải hoặc ngược lại 
    } 
    else l = m + 1; // chỉ cần ngược lại ở trên 
}
```
* **Áp dụng**
    - Lưu ý muốn chặt được phải có tính chất bỏ được 1 trong 2, ví dụ như mảng phải được sort,...
    - Lưu ý xét điều kiện đúng nên bỏ bên nào.
    - Điều kiện có thể là một thuật nào đó để check chứ không hẳn chỉ là một phép tính bình thường.
    - Lưu ý bài nào giải bằng 2 con trỏ được thì sẽ giải được bằng chặt nhị phân (chặt nhị phân chạy lâu hơn nhưng vẫn đủ AC), hạn chế dùng 2 con trỏ nếu không chắc chắn.
    - List bài
        + https://lqdoj.edu.vn/problem/np003
        + https://lqdoj.edu.vn/problem/nthclonehv
        + https://lqdoj.edu.vn/problem/twopointeriic


## 4. Quy hoạch động
* **Form code**
```cpp
int f(int n) // có thể nhiều biến hơn tùy trạng thái bài toán
{
    if (n<0) return 0; // điều kiện vô lý return giá trị vô hại
    if (n==1) return 1; // điều kiện dừng
    
    if (chk[n]) return dp[n]; 
    chk[n] = 1; // check đã tính chưa

    int res = 0;  // tạo biến lưu kết quả

    res = f(n-1) + f(n-2); // tính toán dựa trên công thức đã phân tích
    res %= mod; // nếu có mod

    dp[n] = res; // nhớ lưu trữ sau khi tính
    return res;
}

int main()
{
    int res = 0;
    for (int i=1;i<=n;i++) res=max(res,f(i)); // không phải lúc nào cũng chỉ gọi f(n) hoặc cũng có thể chỉ đơn giản như bên dưới
    cout<<f(n); // có thể kết quả của bài toán f(n) thôi là chưa đủ
}
```

* **Áp dụng**
    - Lưu ý, các bài quy hoạch động gần như rất khó để cày trâu, nên khó quá thì dành thời gian cho các bài còn lại.
    - Lưu ý kỹ điều kiện dừng và điều kiện vô lý cũng như là cách gọi nó như đã đề cập trên form code
    - List bài
      	+ https://lqdoj.edu.vn/problem/stonefrog1
      	+ https://lqdoj.edu.vn/problem/knapsack1
        + https://lqdoj.edu.vn/problem/moverd
        + https://lqdoj.edu.vn/problem/nktick
        + ...


## 5. SEGMENT TREE
* **Form code**
```cpp
void update(int id, int l, int r, int k, int u)
{
    if (k<l || r<k) return;
    if (l==r)
    {
        seg[id] = u;
        return;
    }
    int m = (l+r) / 2;
    update(id*2,l,m,k,u);
    update(id*2+1,m+1,r,k,u);
    seg[id] = seg[id*2] + seg[id*2+1]; // chỉ cần thay thế phép toán ở đây
}
long long get(int id, int l, int r, int u, int v)
{
    if (v<l || r<u) return 0; // thay thế giá trị vô hại với phép toán
    if (u<=l && r<=v) return seg[id];
    int m = (l+r) / 2;
    return get(id*2,l,m,u,v) + get(id*2+1,m+1,r,u,v); // thay thế phép toán ở đây
}
int main()
{
    for (int i=1;i<=n;i++) update(1,1,n,i,a[i]); // nhớ build cây
    update(1,1,n,l,r); // 3 đối số đầu tiên luôn luôn là 1,1,n
    get(1,1,n,l,r);    // tương tự 3 đối số đầu tiên là 1,1,n
}
```
* **Áp dụng**
    - Lưu ý khai báo giới hạn mảng **Gấp 4 lần** giới hạn mảng của đề
    - Lưu ý **Build** cây trước khi làm gì tiếp theo
    - Nếu không nhớ segment tree thì cày trâu
    - List bài
        + https://lqdoj.edu.vn/problem/cses1648
        + https://lqdoj.edu.vn/problem/findmax2
        + https://lqdoj.edu.vn/problem/gcd
        + ...

## 6. HASH
* **Form code**
```cpp
const long long base = 1612; // chọn base lớn hơn 255 nhưng cũng không cần lớn quá;
const long long mod = 1161220251; // mod khoảng 1e9 tức là số 1 cộng 9 số phía sau, mod không được lớn quá.
void build()
{
    h[0] = s[0];
    for (int i=1;i<n;i++) 
    {
        h[i] = h[i-1] * base + s[i];
        h[i] %= mod;
    }
    p[0] = 1;
    for (int i=1;i<=n;i++)
    {
        p[i] = p[i-1] * base;
        p[i] %= mod;
    }
}
long long get(int l, int r)
{
    if (l==0) return h[r];
    long long res = (h[r] + ((-h[l-1] + mod) * p[r-l+1]) % mod) % mod;
    return res;
}
```

* **Áp dụng**
    - Lưu ý cái này là hash từ trái sang phải, nên viết hash từ phải sang trái (nếu dùng) thì không phải cứ ngược lại mà cần đọc hiểu
    - chọn base lớn hơn 255;
    - Tương tự code hash cũng khá khó, nếu không nhớ thì cày trâu.
    - List bài:
        + https://lqdoj.edu.vn/problem/cses1753
        + https://lqdoj.edu.vn/problem/cses1732
        + ...

## 100. Luyện tư duy 
1. **Đề tuyển sinh LQĐ các năm gần đây (2021-2025)**
    - List bài:
        + https://lqdoj.edu.vn/problem/25ts10lqdb3
        + https://lqdoj.edu.vn/problem/21ts10dna2
        + https://lqdoj.edu.vn/problem/21ts10dna3
        + https://lqdoj.edu.vn/problem/25ts10lqdb1
        + https://lqdoj.edu.vn/problem/21ts10dna4
        + https://lqdoj.edu.vn/problem/25ts10lqdb2
        + https://lqdoj.edu.vn/problem/24ts10dna2
        + ...
2. **Chặt nhị phân + prefix sum/mảng đánh dấu/toán**
    - List bài:
        + https://lqdoj.edu.vn/problem/ksum
		+ https://lqdoj.edu.vn/problem/ndivi
		+ https://lqdoj.edu.vn/problem/candyboxes
        + https://lqdoj.edu.vn/problem/partition3
        + https://lqdoj.edu.vn/problem/21thtska3
		+ https://lqdoj.edu.vn/problem/tht24bngbbc4
		+ https://lqdoj.edu.vn/problem/25ts10dth4
		+ https://lqdoj.edu.vn/problem/24tht255a2
		+ https://lqdoj.edu.vn/problem/bnhan
        + https://lqdoj.edu.vn/problem/sumconset
        + https://lqdoj.edu.vn/problem/findingk
        + https://lqdoj.edu.vn/problem/skydef
        + https://lqdoj.edu.vn/problem/cppb2p124
    	+ ...
3. **chặt nhị phân + quy hoạch động/segment tree/hash**
    - List bài:
        + https://lqdoj.edu.vn/problem/trauanco
        + https://lqdoj.edu.vn/problem/23ththnc2
        + https://lqdoj.edu.vn/problem/cses1749
        + https://lqdoj.edu.vn/problem/cses1143
        + https://lqdoj.edu.vn/problem/cses1111
        + https://lqdoj.edu.vn/problem/23ts10dna2
        + ...
4. **Hỗn hợp nhiều thuật**
    - List bài:
        + https://lqdoj.edu.vn/problem/cses2420
        + https://lqdoj.edu.vn/problem/cses2106
        + https://lqdoj.edu.vn/problem/pun
        + https://lqdoj.edu.vn/problem/cses1145
        + ...
