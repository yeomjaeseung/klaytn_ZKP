# How does it work

This code is a new pr for Num2BitNeg
```
template Num2BitsNeg(n) {
    signal input in;
    signal output out[n];
    var lc1 = 0;

    component isZero;

    isZero = IsZero();

    var neg = in < 0 ? 2**n + in : in;

    for (var i = 0; i < n; i++) {
        out[i] <-- (neg >> i) & 1;
        out[i] * (out[i] - 1) === 0;
        lc1 += out[i] * 2**i;
    }

    in ==> isZero.in;

    lc1 + isZero.out * 2**n === (in < 0 ? 2**n + in : in);
}
```
If the input signal is set to -42 and n is set to 8, the Num2BitsNeg circuit will output the two's complement binary representation of -42 using 8 bits: 11010110.

1. To obtain this result, the following steps are taken by the Num2BitsNeg circuit:

2. The in signal is checked to determine whether it is negative. Since -42 is negative, the condition in < 0 is true.

3. The variable neg is computed using the formula 2**n + in, which in this case gives 2**8 - 42 = 214.

4. The for loop iterates over the n bits of the output array out, starting with the least significant bit. For each bit, the expression (neg >> i) & 1 is evaluated to extract the corresponding bit of the neg value. This value is stored in the out array.

5. The loop also checks that each bit in the out array is either 0 or 1, by evaluating the expression out[i] * (out[i] - 1) === 0. This ensures that the output is a valid binary number.

6. The loop computes the decimal value of the two's complement representation by accumulating the product of each bit in the out array with the corresponding power of 2, using the formula lc1 += out[i] * 2**i.

7. The in signal is connected to the in input of the isZero component, which checks whether in is zero.

8. The output of the isZero component, which is either 0 or 1, is added to the accumulated value lc1 multiplied by 2**n. This ensures that the final value is equal to 2**n - in if in is negative, or in if in is non-negative.

9. In this case, since in is negative and equal to -42, the final output of the Num2BitsNeg circuit will be the two's complement binary representation of -42 using 8 bits, which is 11010110.

## Two's complement representation

Two's complement is a mathematical operation used to represent negative numbers in binary (base-2) form. In two's complement representation, the negative of an n-bit binary number is represented by the bitwise complement of the number (i.e., flipping all the bits) and adding 1.

Here's an example of how to convert the decimal value -42 to its two's complement binary representation using 8 bits:

1. Convert the absolute value of the decimal number (i.e., 42) to binary form:
```
42 = 00101010
```
2.Take the bitwise complement of the binary number (i.e., flip all the bits):
```
00101010
--------  bitwise complement (flip all the bits)
11010101
```
3. Add 1 to the bitwise complement:
```
11010101
+ 00000001
---------
11010110
```
Therefore, the two's complement representation of the decimal value -42 in 8 bits is 11010110. This is the binary representation that is used in many computer systems to represent negative numbers.

## Why it should be changed?

1. The condition n == 0 ? 0 : 2**n - in is not correct for computing the two's complement representation of in. It should be in < 0 ? 2**n + in : in instead, as I explained in a previous answer. This is because in two's complement representation, the most significant bit (i.e., the leftmost bit) is used to indicate the sign of the number, so we need to check if in is negative and compute the complement accordingly.

2. The assertion out[i] * (out[i] - 1) === 0 is not necessary and does not contribute to the correctness of the code. This assertion checks that out[i] is either 0 or 1, which is always true because of the bitwise operation used to compute out[i]. Therefore, it can be removed without affecting the behavior of the code.