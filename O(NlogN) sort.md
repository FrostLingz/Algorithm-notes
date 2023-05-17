## 复杂度为O(NlogN)的排序

**arr[L..R] 范围上求最大值**

```java
public static int process(int[] arr, int L, int R) {
  if (L == R) {
    return arr[L];
  }
  int mid = L + ((R - L) >> 1);
  int leftMax = process(arr, L, mid);
  int rightMax = process(arr, mid + 1, R);
  return Math.max(leftMax, rightMax);
}
```

**Merge Sort**

```java
   public static void mergeSort(int[] arr) {
      if (arr == null || arr.length < 2) {
        return;
      }
      process(arr, 0, arr.length - 1);
   }
   
   public static void process(int[] arr, int L, int R) {
      if (L == R) {
        return;
      }
      int mid = L + ((R - L) >> 1);
      process(arr, L ,mid);
      process(arr, mid + 1, R);
      merge(arr, L mid, R);
   }
   
   public static void merge(int[] arr, int L, int M, int R) {
      int[] help = new int[R - L + 1];
      int i = 0;
      int p1 = L1;
      int p2 = M + 1;
      while (p1 <= M && p2 <= R) {
        help[i++] = arr[p1] <= arr[p2] ? arr[p1++] : arr[p2++];
      }
      while (p1 <= M) {
        help[i++] = arr[p1++];      
      }
      while (p2 <= R) {
        help[i++] = arr[p2++];
      }
      for (; i < help.length; i++) {
        arr[L + i] = help[i]; 
      }
   }
```

**小和问题**
> 在一个数组中，每一个数左边比当前数小的累加起来，叫做这个数组的小和。求一个数组的小和。  
> 例: [1, 3, 4, 2, 5] 1 + 1 + 3 + 1 + 1 + 3 + 4 + 2 =16

归并排序的过程，可以保证小和计算的不重不漏。
左边比当前数字小 = 右边比当前数字大 在归并排序的过程中，左边p1位置的数和右边p2位置的数比较，
> 1. arr[p1] < arr[p2]，那么说明右边有(R - p2 + 1)个数大于左边p1位置的数。  
> 小和sum += arr[p1] * (R - p2 + 1)。 arr[p1]放入help，p1++。  
> 2. arr[p1] > arr[p2], p2位置的数放入help，p2++。  
> 3. arr[p1] > arr[p2], **将p2位置的数放入help，p2++。不能拷贝p1位置，因为两边相等，无法知道右边有多少个数比左边大，所以拷贝右边。**

```java
    
```




