# ICS4U - Algorithms
- - - -
## Sorting Algorithms

### Insertion Sort

```java
public static double insertionSort(int[] arr, boolean visualized){
        Stopwatch watch = new Stopwatch();
        int N = arr.length;
        for(int i = 1; i < N; i++){
            for(int j = i; j > 0; j--){
                if(arr[j-1] > arr[j]) {
                    exch(arr, j, j-1);
                    if(visualized)
                        visualize(arr);
                } 
                else break;
            }
        }
        return watch.elapsedTime();
    }
```

* Complexity: O(n^2) because nested for loops
* Maintains a sorted sublist in the lower positions of the list. Each new item is then “inserted” back into the previous sublist such that the sorted sublist is one item larger.

### Selection Sort

```java
public static double selectionSort(int[] arr, boolean visualized){
        Stopwatch watch = new Stopwatch();
        int min = 0;
        for(int i = 0; i < arr.length; i++){
            for(int j = i + 1; j < arr.length; j++){
                if(arr[j] < arr[min]) min = j;

            }
            exch(arr, i, min);
            if(visualized) visualize(arr);
        }
        return watch.elapsedTime();
    }
```

* Complexity: O(n^2) because nested for-loops
* On each pass, the unsorted element with the smallest (or largest) value is moved to its proper position in the array.

### Merge Sort

```java
public static double mergesort(int[] a, boolean visualized) { 
        Stopwatch watch = new Stopwatch();
        int[] aux = new int[a.length];
        mergesort(a, aux, 0, a.length - 1, visualized);
        return watch.elapsedTime();
    }

    private static void mergesort(int[] a, int[] aux, int lo, int hi, boolean visualized) {
        // Array is sorted if low is greater than high
        if (lo >= hi)  return;
        int mid = (lo + hi) / 2;  //index of middle element

        mergesort(a, aux, lo, mid, visualized);    //Sort left side of array
        mergesort(a, aux, mid + 1, hi, visualized);//Sort right side of array
        merge(a, aux, lo, mid, hi, visualized);    //Combine both halves

    } 

    private static void merge(int[] a, int[] aux, int lo, int mid, int hi, boolean visualized){
        // copy
        for(int k = lo; k <= hi; k++)
            aux[k] = a[k];
        // merge
        int i = lo;
        int j = mid + 1;
        for (int k = lo; k <= hi; k++)
        {
            if      (i > mid)           a[k] = aux[j++];
            else if (j > hi)            a[k] = aux[i++];
            else if (aux[j] < aux[i])   a[k] = aux[j++];
            else                        a[k] = aux[i++];
            if(visualized) visualize(a);
        }
    }
```

* Complexity: O(n log n)
* Continuously splits and sorts the list, then merges the two halves, recursively.

### Quick Sort

```java
/**
     * Partition Method: helper method for quickSort.
     */
    public static int partition(int arr[], int left, int right, boolean visualized)
    {
        int i = left, j = right;
        int tmp;
        int pivot = arr[(left + right) / 2];

        while (i <= j) {
            while (arr[i] < pivot)
                i++;
            while (arr[j] > pivot)
                j--;
            if (i <= j) {
                exch(arr, i, j);
                if(visualized) visualize(arr);
                i++;
                j--;
            }
        };

        return i;
    }

    public static double quickSort(int arr[], int left, int right, boolean visualized) {
        Stopwatch watch = new Stopwatch();
        int index = partition(arr, left, right, visualized);
        if (left < index - 1)
            quickSort(arr, left, index - 1, visualized);
        if (index < right)
            quickSort(arr, index, right, visualized);
        return watch.elapsedTime();
    }
```

* Complexity O(n log n) on average, O(n^2) worst
* Repeatedly divide the array into “partitions” and recursively sort these partitions. It divides using a pivot, finding which elements are lesser and greater, and then sorts them into two different sub partitions. (One for values lesser than the pivot, one for those values greater than the pivot)

## Searching Algorithms
### Linear Search

```java
public static int linearSearch(int[] arr, int val){
        for(int i = 0; i < arr.length; i++){
            if(arr[i] == val){
                return i;
            }
        }
        return -1;
    }
```

* Complexity: O(n)
* Simple algorithm, iterate through the array and check if the value is at the current index. Doesn’t require the array to be sorted
### Binary Search

``` java 
public static int binarySearch(int[] arr, int value, int lo, int hi){
        if(hi < lo) return -1;
        int mid = (hi + lo)/2;
        if(arr[mid] > value){
            return binarySearch(arr, value, lo, mid -1);
        } else if(arr[mid] < value) {
            return binarySearch(arr, value, mid + 1, hi);
        }
        return mid;
    }
```

* Complexity O(log n)
* Only works on SORTED arrays. Takes the midpoint of the array and checks if the value is less than or greater than the midpoint, then either increments or  decrements the midpoint value until the value is found. It is called “Binary Search” because the array is split into 2 (thus, binary).

