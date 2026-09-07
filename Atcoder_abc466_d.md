## Atcoder466 D. Placing Rooks
## 問題
[問題](https://atcoder.jp/contests/abc466/tasks/abc466_d)
## 解法
```
def main():
    N, M = map(int, input().split())

    query = []
    for _ in range(M):
        query.append(list(map(int, input().split())))
        
    res = 0
    R = set()
    C = set()
    for i in range(M-1, -1, -1):
        r, c = query[i]
        if r not in R and c not in C:
            res += 1
        R.add(r)
        C.add(c)
    print(res)
        
main()
```
