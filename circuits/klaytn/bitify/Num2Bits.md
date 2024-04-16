# How does it work

The Num2Bits(n) template takes a single input parameter n, which is used to determine the number of output bits in the resulting binary representation. The in input signal is used to pass in the unsigned integer to be converted, while the out output signal is used to produce the resulting binary representation.

The code then initializes two variables, lc1 and e2, which are used to perform the binary conversion. The e2 variable is initialized to 1 and is doubled in each iteration of the loop, while lc1 is initially set to 0 and is used to accumulate the value of the binary representation.

The loop then iterates over each bit in the binary representation, from the least significant bit to the most significant bit. In each iteration, the corresponding bit of the input integer is extracted and stored in the corresponding element of the output signal, using the expression out[i] <-- (in [>>](#what-is--operation) i) [&](#-operation) 1. This expression shifts the input integer right by i bits and then performs a bitwise AND with 1, effectively extracting the ith bit of the input integer.

The expression out[i] * (out[i] -1 ) === 0 checks that each output bit is either 0 or 1, ensuring that the binary representation is valid.

Finally, the expression lc1 === in checks that the accumulated value of the binary representation is equal to the original input integer, ensuring that the conversion was performed correctly.

In summary, this code defines a template for a function that converts an unsigned integer to its binary representation, and performs some validity checks to ensure that the binary representation is correct.


## Here's an example of how the code out[i] <-- (in >> i) & 1 would extract the individual bits of the integer 4:
```
var in = 4; // binary representation: 100

// Initialize output array
var out = [0, 0, 0];

// Extract individual bits and store in output array
for (var i = 0; i < 3; i++) {
    out[i] <-- (in >> i) & 1;
}

// Print output array
console.log(out); // [0, 0, 1]
```
In this example, the input integer is 4, which has a binary representation of 100. The output array out is initialized as [0, 0, 0] to hold the individual bits of the input integer.

The loop then iterates over each bit position from the least significant bit to the most significant bit. In the first iteration, the expression (in >> i) & 1 evaluates to (4 >> 0) & 1, which is equal to 0 & 1 = 0. This value is then stored in the first element of the out array using the <-- operator.

In the second iteration, the expression (in >> i) & 1 evaluates to (4 >> 1) & 1, which is equal to 1 & 1 = 1. This value is then stored in the second element of the out array using the <-- operator.

In the third iteration, the expression (in >> i) & 1 evaluates to (4 >> 2) & 1, which is equal to 0 & 1 = 0. This value is then stored in the third element of the out array using the <-- operator.

Finally, the output array is printed to the console, which displays the binary representation of the input integer as [0, 0, 1].


## & operation

The bitwise AND operation is a binary operation that takes two numbers and performs a logical AND on their individual bits, producing a new number that has a 1 in each bit position where both input numbers have a 1, and a 0 in all other positions.

Here's an example:

Let's say we have two numbers, a = 10 (binary representation: 1010) and b = 6 (binary representation: 0110). If we perform the bitwise AND operation a & b, we get:

```
   1010 (a)
 & 0110 (b)
   ------
   0010
```
The result is 2 (binary representation: 0010), which has a 1 in the second bit position because both a and b have a 1 in that position.

In the context of the code out[i] <-- (in >> i) & 1, the bitwise AND operation is used to extract the ith bit of the input integer in by performing a logical AND with the binary value 1, which has a 1 in the least significant bit position and 0s in all other positions. By performing the AND operation, the result is either 0 or 1, depending on whether the ith bit of in is 0 or 1. This value is then stored in the ith element of the output array out.

## what is >> operation

The >> (double greater than) symbol is a bitwise shift operator in programming languages. It shifts the bits of a binary number to the right by a specified number of positions, effectively dividing the number by a power of two.

The >> operator takes two operands: the first operand is the number to be shifted, and the second operand is the number of bit positions to shift the number. For example, the expression x >> n shifts the bits of x to the right by n positions.

Here's an example:

Let's say we have the number 5, which has a binary representation of 101. If we shift the bits of 5 to the right by 1 position using the expression 5 >> 1, we get:

```
  101 (5)
>> 1
  ---
   10 (2)
```

The result is 2, which is the integer value of the binary number 10. This is equivalent to dividing 5 by 2 and rounding down.

In the context of the code out[i] <-- (in >> i) & 1, the >> operator is used to extract the ith bit of the input integer in by shifting the bits of in to the right by i positions. This shifts the ith bit of in to the least significant bit position, which can then be extracted using the & operator to perform a bitwise AND with the binary value 1.