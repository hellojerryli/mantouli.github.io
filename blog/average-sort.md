## 平均排序

假设我们不是要完全排序一个数组，而只是要求数组中的元素在平均情况下是升序的，更准确的说，如果对所有的i=0, 1, 2, 3, ..., n-1-k,有arr[i] <= arr[i + k]成立，我们就称一个包含n个元素的数组arr是k排序的(k-sorted)。

下面的算法能在O(n * lg(n / k))时间内对一个包含n个元素的数组进行k排序，当k是一个常数时，对包含n个元素的数组进行k排序需要Ω(n * lgn)的时间。

```java
public void kSort(int[] arr, int k, int p, int r) {
    if (p < r && r - p >= k) {
        int q = partition(arr, p, r);
        kSort(arr, k, p, q - 1);
        kSort(arr, k, q + 1, r);
    }
}

private int partition(int[] arr, int p, int r) {
    int i = p - 1;
    for (int j = p; j <= r - 1; j++) {
        if (arr[j] <= arr[r]) {
            i++;
            swap(arr, i, j);
        }
    }
    swap(arr, i + 1, r);
    return i + 1;
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```
