## 剑指 Offer II 001. 整数除法
```c++
int divide(int a, int b) {

        if (a == INT_MIN && b == -1) return INT_MAX;
        //INT_MIN = 0x80000000 = -2^31
        //INT_MAX = 0x7fffffff = 2^31
        //0xc0000000 = -2^30

        int sign = (a > 0) ^ (b > 0) ? -1 : 1;
        if (a > 0) a = -a;
        if (b > 0) b = -b;
        
        int res = 0;
        while (a <= b) {
            int value = b;
            int k = 1;
            while (value >= 0xc0000000 && a <= value + value) {
                value += value;
                if (k > INT_MAX / 2) return INT_MIN;
                k += k;
            }
            a -= value;
            res += k;
        }
        
        return sign == 1 ? res : -res;
}
```
## Attention: 
- Substract - divide
- Boundary: abs(INT_MIN) > abs(INT_MAX)
- Optimize: Minimize Dividend
