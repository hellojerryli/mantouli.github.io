## 最大子数组问题

我们来思考如何使用分治法来求解最大子数组问题。假定我们要寻找子数组arr[low...high]的最大子数组。使用分治技术意味着我们要将子数组划分为两个规模尽可能相等的子数组，也就是说，找到子数组的中央位置，比如mid，然后考虑求解两个子数组arr[low...mid]和arr[mid + 1...high]。如图所示，arr[low...high]的任何连续子数组arr[i...j]所处的位置必然是以下三种情况之一：

* 完全位于子数组arr[low...mid]中，因此low <= i <= j <= mid。
* 完全位于子数组arr[mid + 1, high]中，因此mid < i <= j <= high。
* 跨越了中点，因此low <= i <= mid < j <= high。

因此，arr[low...high]的一个最大子数组所处的位置必然是这三种情况之一。实际上，arr[low...high]的一个最大子数组必然是完全位于arr[low...mid]中、完全位于arr[mid + 1...high]中或者跨越中点的所有子数组中的和最大者。我们可以递归地求解arr[low...mid]和arr[mid + 1...high]，因为这两个问题仍然是最大子数组问题，只是规模更小。因此，剩下的工作就是寻找跨越中点的最大子数组，然后在三种情况中选择和最大者。

```java
public class MaximumSubarray {
    public int[] maximumSubarray(int[] arr, int low, int high) {
        if (low == high) {
            return new int[]{low, high, arr[low]};
        } else {
            int mid = (low + high) / 2;
            int[] left = maximumSubarray(arr, low, mid);
            int[] right = maximumSubarray(arr, mid + 1, high);
            int[] cross = maxCrossingSubarray(arr, low, mid, high);
            int leftSum = left[2];
            int rightSum = right[2];
            int crossSum = cross[2];
            if (leftSum >= rightSum && leftSum >= crossSum) {
                return left;
            } else if (rightSum >= leftSum && rightSum >= crossSum) {
                return right;
            } else {
                return cross;
            }
        }
    }
    
    private int[] maxCrossingSubarray(int[] arr, int low, int mid, int high) {
        int sum = 0;
        int leftSum = Integer.MAX_VALUE;
        int leftIndex = mid;
        for (int i = mid; i >= low; i--) {
            sum += arr[i];
            if (sum > leftSum) {
                leftSum = sum;
                leftIndex = i;
            }
        }
        sum = 0;
        int rightSum = Integer.MAX_VALUE;
        int rightIndex = mid + 1;
        for (int i = mid + 1; i <= high; i++) {
            sum += arr[i];
            if (sum > rightSum) {
                rightSum = sum;
                rightIndex = i;
            }
        }
        return new int[]{leftIndex, rightIndex, leftSum + rightSum};
    }
}
```
