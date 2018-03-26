## 逆序对

对于数组arr，若i < j且arr[i] > arr[j]，则对偶(i, j)称为数组arr的一个逆序对，例如，数组[2, 3, 8, 6, 1]所有的逆序对为(0, 4)、(1, 4)、(2, 3)、(2, 4)、(3, 4)。

可以通过修改归并排序，来确定在任意一个数组中逆序对的数量，与归并排序相同，最坏情况需要O(n * lgn)的时间。

```java
public int mergeSort(int[] arr, int p, int r) {
    if (p < r) {
        int q = (p + r) / 2;
        return mergeSort(arr, p, q) + mergeSort(arr, q + 1, r) + merge(arr, p, q, r);
    }
    return 0;
}

private int merge(int[] arr, int p, int q, int r) {
    int n1 = q - p + 1;
    int n2 = r - q;
    int[] left = new int[n1];
    int[] right = new int[n2];
    for (int i = 0; i < n1; i++) {
        left[i] = arr[p + i];
    }
    fot (int i = 0; i < n2; i++) {
        right[i] = arr[q + 1 + i];
    }
    int i = 0, j = 0, k = p, inv = 0;
    while (i < n1 && j < n2) {
        if (left[i] <= right[j]) {
            arr[k++] = left[i++];
        } else {
            arr[k++] = right[j++];
            inv += n1 - i;
        }
    }
    if (i == n1) {
        while (j < n2) {
            arr[k++] = right[j++];
        }
    } else {
        while (i < n1) {
            arr[k++] = left[i++];
        }
    }
    return inv;
}
```
