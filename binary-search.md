## 二分查找

考虑一个查找问题，在序列arr中查找关键字key，如果该序列已经排好序，就可以将该序列的中点与key进行比较，根据比较的结果，原序列有一半就可以不用再做进一步的查找了。二分查找算法重复这个过程，每次都将序列剩余部分的规模减半，直到找到key或者返回-1。

迭代版本：

```java
public int iterativeBinarySearch(int[] arr, int key) {
    int low = 0;
    int high = arr.length = 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (key == arr[mid]) {
            return mid;
        } else if (key < arr[mid]) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return -1;
}
```

递归版本：

```java
public int recursiveBinarySearch(int[] arr, int key, int low, int high) {
    if (low > high) {
        return -1;
    }
    int mid = (low + high) / 2;
    if (key == arr[mid]) {
        return mid;
    } else if (key < arr[mid]) {
        return recursiveBinarySearch(arr, key, low, mid - 1);
    } else {
        return recursiveBinarySearch(arr, key, mid + 1, high);
    }
}
```
