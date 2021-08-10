# Number Theory

### 1) Modular arithmetic

When one number is divided by another, the modulo operation finds the remainder. It is denoted by the **%** symbol

Properties : 

1) (a + b) % c = ((a % c) + (b % c)) % c
2) (a * b) % c = ((a % c) * (b % c)) % c
3) (a - b) \% c = ((a \% c) - (b \% c) + c) \% c
4) (a / b) \% c = ((a \% c) - (b<sup>-1</sup> \% c)) \% c



### 2) Modular exponentiation

Recursive
```cpp
int recursivePower(int x, int n)
{
    if(n == 0)
        return 1;
    return x * recursivePower(x, n-1);
}
```
Iterative
```cpp
int iterativePower(int x,int n)
{
    int res = 1;
    while(n--)
    {
        res *= x;
    }
    return res;
}
```

Binary Exponentiation
```cpp
int binaryExponentiation(int x, int n)
{
    if(n == 0)
        return 1;
    else if(n%2 == 0)        //n is even
        return binaryExponentiation(x*x, n/2);
    else                             //n is odd
        return x*binaryExponentiation(x*x, (n-1)/2);
}
```
iterative version
```cpp
int binaryExponentiation(int x, int n)
{
    int res = 1;
    while(n > 0)
    {
        if(n % 2 == 1)
            res *= x;
        x *= x; 
        n /= 2;
    }
    return res;
}
 ```
 
 Modular Exponentiation
 ```cpp
 int modularExponentiation(int x, int n, int M)
{
    if(n == 0)
        return 1;
    else if(n%2 == 0)        //n is even
        return modularExponentiation((x*x)%M, n/2,M);
    else                             //n is odd
        return (x*modularExponentiation((x*x)%M, (n-1)/2, M))%M;

}
 ```
 Iterative binary exponentiation
 ```cpp
 int modularExponentiation(int x,int n,int M)
{
    int result=1;
    while(n>0)
    {
        if(power % 2 ==1)
            result=(result * x)%M;
        x=(x*x)%M;
        n=n/2;
    }
    return result;
}
```
GCD
```cpp
int GCD(int A, int B) {
    int m = min(A, B), gcd;
    for(int i = m; i > 0; --i)
        if(A % i == 0 && B % i == 0) {
            gcd = i;
            return gcd;
        }
}
```
Euclid's algorithm
```cpp
int GCD(int A, int B) {
    if(B==0)
        return A;
    else
        return GCD(B, A % B);
}
```

Mod Inverse <br/>
1) Naive approach
```cpp
int modInverse(int A,int M)
{
    A=A%M;
    for(int B=1;B<M;B++)
        if((A*B)%M)==1)
            return B;
}
```
2) Euclid
```cpp
int d,x,y;
int modInverse(int A, int M)
{
    extendedEuclid(A,M);
    return (x%M+M)%M;    //x may be negative
}
```
3) Modular Exponentiation
```cpp
int modInverse(int A,int M)
{
    return modularExponentiation(A,M-2,M);
}
```
