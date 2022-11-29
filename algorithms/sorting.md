# 시간 복잡도 O(n²)
## 1. Insertion Sort
```java
public class Insertion_Sort {
    public static void sort(int[] arr) {
        for (int end = 1; end < arr.length; end++) {
            int i = end;
            while (i > 0 && arr[i - 1] > arr[i]) {
                swap(arr, i - 1, i);
                i--;
            }
        }
    }

    private static void swap(int[] arr, int a, int b) {
        int tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
}
```

## 2. Selection Sort
```java
public class Selection_Sort {
    public static void sort(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            int minIdx = i;
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[minIdx])
                    minIdx = j;
            }
            swap(arr, i, minIdx);
        }
    }

    private static void swap(int[] arr, int a, int b) {
        int tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
}
```

## 3. Bubble Sort
```java
public class Bubble_Sort {
    public static void sort(int[] arr) {
        for (int i = arr.length - 1; i > 0; i--) {
            for (int j = 0; j <= i; j++) {
                if (arr[j] > arr[j + 1])
                    swap(arr, j, j + 1);
            }
        }
    }

    private static void swap(int[] arr, int a, int b) {
        int tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
}
```

<br>

# 시간 복잡도 O(n log n)
## 1. Quick Sort
```java
public class Quick_Sort {
    public static List<Integer> quickSort(List<Integer> list) {
        if (list.size() <= 1) return list;
        int pivot = list.get(list.size() / 2);

        List<Integer> lesserArr = new LinkedList<>();
        List<Integer> equalArr = new LinkedList<>();
        List<Integer> greaterArr = new LinkedList<>();

        for (int num : list) {
            if (num < pivot) lesserArr.add(num);
            else if (num > pivot) greaterArr.add(num);
            else equalArr.add(num);
        }

        return Stream.of(quickSort(lesserArr), equalArr, quickSort(greaterArr))
                .flatMap(Collection::stream)
                .collect(Collectors.toList());
    }
}
```

## 2. Merge Sort
```java
public class Merge_Sort {
    public static int[] sort(int[] arr) {
        if (arr.length < 2) return arr;

        int mid = arr.length / 2;
        int[] low_arr = sort(Arrays.copyOfRange(arr, 0, mid));
        int[] high_arr = sort(Arrays.copyOfRange(arr, mid, arr.length));

        int[] mergedArr = new int[arr.length];
        int m = 0, l = 0, h = 0;
        while (l < low_arr.length && h < high_arr.length) {
            if (low_arr[l] < high_arr[h])
                mergedArr[m++] = low_arr[l++];
            else
                mergedArr[m++] = high_arr[h++];
        }
        while (l < low_arr.length) {
            mergedArr[m++] = low_arr[l++];
        }
        while (h < high_arr.length) {
            mergedArr[m++] = high_arr[h++];
        }
        return mergedArr;
    }
}
```
