# 归并排序算法及其应用

## 归并排序简介

归并排序的思想也是分治思想，如果我们要排序一个无序数组，我们先把数组从中间分成前后两部分，然后对前后2部分分别排序，再将排序好的两部分合并到一起，这样整个数组就都有序了。



## 归并排序算法实现

```java
/**
 * 归并排序算法
 * 时间复杂度是O(nlogn)
 */
@Data
public class MergeSort {

    public void mergeSort(int[] a, int n) {
        mergeSortPartition(a, 0, n - 1);
    }

    private void mergeSortPartition(int[] a, int p, int r) {
        if (p >= r) return;
        int mid = (p + r) / 2;
        mergeSortPartition(a, p, mid);
        mergeSortPartition(a, mid + 1, r);
        merge(a, p, r, mid);
    }

    /**
     * 归并排序
     * @param a
     */
    private void merge(int[] a, int p, int r, int mid) {
        int i = p;
        int j = mid + 1;
        int k = 0;
        int[] temp = new int[r-p];
        while (i <= mid && j <= r) {
            if (a[i] <= a[j]) {
                temp[k++] = a[i++];
            } else {
                temp[k++] = a[j++];
            }
        }

        // 判断数组两边那一边先跑完了
        int start = i;
        int end = mid;
        if (j <= r) {
            start = j;
            end = r;
        }

        // 把排序好的临时数组的数据重新复制到要排序的数组中
        for (int t= 0; t < r-p; t++) {
            a[p+t] = temp[t];
        }
    }
}

```

