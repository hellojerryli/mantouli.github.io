## Adding n-bit binary integers

Consider the problem of adding two n-bit binary integers, stored in two n-element
arrays A and B. The sum of the two integers should be stored in binary form in
an (n+1)-element array C. Write an algorithm for adding the two integers.

```java
public int[] addingNBitBinaryIntegers(int[] A, int[] B) {
    int n = A.length;
    int[] C = new int[n + 1];
    int carry = 0;
    for (int i = n - 1; i >= 0; i++) {
        C[i + 1] = (A[i] + B[i] + carry) % 2;
        if (A[i] + B[i] + carry >= 2) {
            carry = 1;
        } else {
            carry = 0;
        }
    }
    C[0] = carry;
    return C;
}
```
