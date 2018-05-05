## 随机样本

假设我们希望创建集合[1, 2, 3, ..., n]的一个随机样本，即一个具有m个元素的集合S，其中0 <= m <= n，使得每个m集合能够等可能地创建。一种方法是先随机排列数组，然后取前面的m个元素，这种方法对随机化过程random调用了n次。如果n比m大很多，我们能够创建一个随机样本，只对random调用更少的次数。

下面的代码返回[1, 2, 3, ..., n]的一个随机m子集s，其中每个m子集是等可能的，然而只对random调用m次。

```java
public List<Integer> randomSample(int m, int n) {
    if (m == 0) {
        return new ArrayList<>();
    } else {
        List<Integer> s = randomSample(m - 1, n - 1);
        int i = (int) (Math.random() * (n + 1));
        if (s != null) {
            if (s.contains(i)) {
                s.add(n);
            } else {
                s.add(i);
            }
        }
        return s;
    }
}
```
