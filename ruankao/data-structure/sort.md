## 排序

### 1. 排序的概念

- 稳定与不稳定

  > 若在待排序的序列中，Ri和Rj关键字相同，若在排序后，两者的相对位置保持不变，则排序是稳定的，否则是不稳定的。

### 2. 简单排序

#### 2.1 直接插入排序

- **概念**

  在插入第i个记录时，R1, R2....Ri-1已经排好序，这是将Ri的关键字k一次与已经排好序的序列比较，找到插入的位置，插入位置及其后的记录依次向后移动。

- **代码**

  ```java
  public int[] insertSort(int[] array) {
          // 直接插入排序
          for (int i = 1; i < array.length; i++) {
              int tmp = array[i];
              int j = i;
              while (tmp < array[j - 1]) {
                  array[j] = array[j - 1];
                  j--;
              }
              array[j] = tmp;
          }
          return array;
      }
  ```

- **分析**

  直接插入排序是一种**稳定**的排序方法，其时间复杂度为**O(n^2)**。在排序过程中仅需要一个元素的辅助空间，空间复杂度为**O(1)**。

#### 2.2 冒泡排序

- 概念

  首先将第一个记录的关键字和第二个记录的关键字进行比较，若为逆序，则交换这两个记录的顺序；然后比较第二个和第三个记录，直到比完所有的记录。这样每一趟就会将最大的数移到序列的后面。

- 代码

  ```java
  public int[] sort2(int[] array) {
          // 冒泡排序
          for (int i = 0; i < array.length; i++) {
              for (int j = 0; j < array.length - 1 - i; j++) {
                  if (array[j] > array[j + 1]) {
                      int tmp = array[j];
                      array[j] = array[j + 1];
                      array[j + 1] = tmp;
                  }
              }
          }
          return array;
      }
  ```

- 分析

  冒泡排序是一中**稳定**的排序方法，其时间复杂度为O(n^1)，在排序过程中仅需要一个元素的辅助空间用于元素的交换，空间复杂度为O(1)。

#### 2.3 简单选择排序

- 概念

  通过n-i次关键字之间的比较，从n-i-1个记录中选出关键字最小的记录，并和第i个记录进行交换，当i等于n时所有记录有序排列。

- 代码

  ```java
  public int[] sort3(int[] array) {
          // 简单选择排序
          for (int i = 0; i < array.length; i++) {
              int minIndex = i;
              for (int j = i; j < array.length; j++) {
                  if (array[j] < array[minIndex]) {
                      minIndex = j;
                  }
              }
              int tmp = array[i];
              array[i] = array[minIndex];
              array[minIndex] = tmp;
          }
          return array;
      }
  ```

- 分析

  这是一种**不稳定**的排序方法。时间复杂度为O(n^2)，在排序过程仅需要一个元素的辅助空间用于数组元素值的交换，空间复杂度为O(1)。

#### 2.3希尔排序

略

#### 2.4 快速排序

- 概念

  通过一趟排序将待排的记录划分为独立的两个部分，称为前半区和后半区，其中，前半区中记录的关键字均不大于后半区记录的关键字，然后再分别对这两部分记录继续进行快速排序。

- 代码

  ```java
  public void sort4(int[] array, int left, int right) {
          // 递归实现快排
          if (left < right) {
              int tmp = array[left];
              int i = left, j = right;
              while (i < j) {
                  while (i < j && array[j] >= tmp) j--;
                  array[i] = array[j];
                  while (i < j && array[i] <= tmp) i++;
                  array[j] = array[i];
              }
              array[i] = tmp;
              sort4(array, left, i - 1);
              sort4(array, i + 1, right);
          }
      }
  ```

- 分析

  这是一种**不稳定**的排序方法，时间复杂度为**O(nlogn)**，空间复杂度为O(1)。该排序算法是平均性能最好的一种。但是如果初始记录序列基本有序时，即每次都是将序列划分为某一半序列的长度为0的情况，此时快速排序的时间复杂度将退化为**O(n^2)**。