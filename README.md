# CSIE1218

這次作業最後一題蠻超綱的 其他題目幾乎沒難度 看懂題目就好

## BitcountInProduct
```c
用了之前交的位元移動 這樣比較快
#include <stdio.h>

int main(void){
    long long a,b;
    long long tnum;
    while(scanf("%ld %ld",&a,&b)!=EOF){
        tnum = a*b;
        int cnt = 0;
        while(tnum > 0){
            if((tnum%2) == 1)
                cnt++;
            tnum >>= 1;
        }
        printf("%d\n",cnt);
    }
    return 0;
}
```
--------
## Coding Prefix Permutations
```c
練習用qsort
#include <stdio.h>  
#include <stdlib.h>  
  
int cmp(const void *a, const void *b){  
   return *(int*)a - *(int*)b;  
}  
  
int main(void) {  
    int arr[1000000];  
    int ptr = 0;  
    while(scanf("%d", &arr[ptr]) != EOF){  
        ptr++;  
    }  
    int cnt = ptr;  
    for(int i = 0; i < ptr; ++i){  
        qsort(arr,i+1,sizeof(int),cmp);  
        for(int j = 0; j <= i; ++j){  
            if(arr[j] != j+1){  
                cnt--;  
                break;  
            }  
        }  
    }  
    printf("%d\n",cnt);  
      
    return 0;  
}  
```
-----------
## Sorted Swap

```c
純靠解題邏輯
#include <stdio.h>
#include <stdlib.h>

int cmp(const void *a, const void *b){
   return *(int*)a - *(int*)b;
}

int checkSorted(int n, int arr[]){
    int b[n+1];
    for (int i = 0; i < n; i++)
        b[i] = arr[i];
    qsort(b, n, sizeof(int), cmp);
    int ct = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] != b[i])
            ct++;
    if (ct == 0 || ct == 2)
        return 1;
    else
        return 0;
}

int main(){
    int arr[1000000];
    int cnt = 0;
    while(scanf("%d", &arr[cnt]) != EOF){
        cnt++;
    }
    if(checkSorted(cnt, arr))
        printf("true\n");
    else
        printf("false\n");
    return 0;
}
```
## Max Sum Distance
```c
#include <stdio.h>
#include <stdlib.h>

int main(){
    int cnt = 0;
    int A[100];
    int maxnum = 0, nownum = 0;
    while(scanf("%d", &A[cnt]) != EOF){
        cnt++;
    }
    for(int i = 0; i < cnt; ++i){
        for(int j = 0; j < cnt; ++j){
            nownum = A[i] + A[j] + abs(i-j);
            if(nownum >= maxnum){
                maxnum = nownum;
            }
        }
    }
    printf("%d\n",maxnum);
    return 0;
}
```
--------
## Reversing Coins

```c
#include <stdio.h>

int main(void) {
  int i = 0;
  int coinarr[100];
  int c_0 = 0, c_1 = 0;
  while(scanf("%d",&coinarr[i]) != EOF){
      if(coinarr[i] == 1)
          c_1++;
      else
          c_0++;
      i++;
  }
  if(c_1 >= c_0)
      printf("%d\n", c_0);
  else
      printf("%d\n", c_1);
  return 0;
}
```
------------
## Fib
這題聽上課講會感覺聽不懂或是沒難度，但其實這題是矩陣快速冪+大數運算 <br>
N的範圍是2^32-1，所以要邊算邊mod，而這動作是為了防止overflow <br>
數字很容易超過2^64-1<br>
看不懂code可以去用"矩陣快速冪"這個關鍵字
```c
#include <stdio.h>

#define int long long

void multiply(int F[2][2], int M[2][2]){
    int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];
    F[0][0] = x%1000000;
    F[0][1] = y%1000000;
    F[1][0] = z%1000000;
    F[1][1] = w%1000000;
}

void power(int F[2][2],int n){
    if(n == 0||n == 1)
        return;
    int M[2][2] = {{1,1},{1,0}};
    power(F, n/2);
    multiply(F,F);
    if(n%2 != 0)
        multiply(F,M);
}

int fib(int n){
    int F[2][2] = {{1,1},{1,0}};
    if(n == 0)
        return 0;
    power(F,n-1);
    return F[0][0];
}
int main(){
    int n;
    scanf("%ld",&n);
    printf("%ld\n",fib(n));
    return 0;
}
```
