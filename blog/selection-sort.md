## Selection sort

Consider sorting n numbers stored in array A by first finding the smallest element
of A and exchanging it with the element in A[0]. Then find the second smallest
element of A, and exchange it with A[1]. Continue in this manner for the first n-1
elements of A. Write implementation for this algorithm, which is known as **_selection sort_**.

```java
public void selectionSort(int[] A) {
    int n = A.length;
    for (int i = 0; i < n - 1; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++) {
            if (A[j] < A[min]) {
                min = j;
            }
        }
        if (min != i) {
            swap(A, min, i);
        }
    }
}

private void swap(int[] A, int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
```
