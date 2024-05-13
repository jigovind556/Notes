# Power of a double value 

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if (n == 0)
            return 1;
        if (n == 1)
            return x;
        if (x == 1)
            return 1;
        else if (x == -1) {
            if (n % 2 == 0) {
                return 1;
            } else {
                return -1;
            }
        }
        if (n < 0) {
            if (n == INT_MIN){
                double posPow = myPow(x, abs(n+1));
                return 1 / posPow*x;
            }
                

            double posPow = myPow(x, abs(n));
            return 1 / posPow;
        }

        if (n & 1) {
            double halfPower = myPow(x, (n - 1) / 2);
            return x * halfPower * halfPower;
        } else {
            double halfPower = myPow(x, n / 2);
            return halfPower * halfPower;
        }
    }
};

```