# 快速排序算法(QuickSort) 及其应用

## 快速排序的概念

快速排序是冒泡排序的一种改进，采用的是分治思想，基本流程如下:

## 基本流程

> 1、从数据集中选择一个基准数；
>
> 2、小于基准数的数据放在数据的左边，大于基准数的数据放在数据的右边；
>
> 3、根据基准数将数据分为2部分，重复上述1、2的流程，直到2边数据都只要1个元素，则数据全局有序。



## 快速排序实现

```java
/**
 * 快速排序
 * 时间复杂度为O(nlogn)
 * 不稳定的原地排序算法
 */
@Data
public class QuickSort {

    public void quickSort(int[] a, int n) {
        quickSortPart(a, 0, n - 1);
    }

    public void quickSortPart(int[] a, int p, int r) {
        if (p >= r) return;
        int q = partition(a, p, r); // 获取分区点
        quickSortPart(a, p, q-1);
        quickSortPart(a, q + 1, r);
    }

    /**
     * 对数组进行分区，小于pivot的元素放在左边，大于pivot的元素放在右边
     *
     * @param a
     * @param p
     * @param r
     * @return
     */
    public int partition(int[] a, int p, int r) {
        int pivot = a[r]; // 中值是最后一个值
        int i = p;
        for (int j = p; j < r ; j++) {
            if (a[j] < pivot) { // 每次从未排序数组中取出一个数据到最小范围内
                swap(a, i, j);
                i++;
            }
        }
        swap(a, i, r);
        return i;
    }

    private void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
}

/**
 * 基于哨兵的方式实现
 * 实现方法二
 */
@Data
public class QuickSort2 {

    public void quickSort(int[] a, int low, int high) {
        if (high <= low) return;
        int i = low;
        int j = high;
        int base = a[high];
        while (i != j) {
            while (a[i] <= base && i < j) {
                i++;
            }
            while (a[j] >= base && i < j) {
                j--;
            }
            swap(a, i, j);
        }
        swap(a, j, high);

        quickSort(a, low, j - 1);
        quickSort(a, j + 1, high);
    }

    private void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
}
```



## 快速排序的应用

* 在一个无序数据集中，找出第k大的元素?