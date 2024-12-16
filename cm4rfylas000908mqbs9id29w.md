---
title: "Helpful code snippets for interview preparation"
datePublished: Mon Dec 16 2024 19:42:14 GMT+0000 (Coordinated Universal Time)
cuid: cm4rfylas000908mqbs9id29w
slug: helpful-code-snippets-for-interview-preparation
tags: problem-solving, interview-preparations

---

# When you need to traverse up, down, left, right

```java
int[][] offsets = {
            {0, 1}, {1, 0}, {0, -1}, {-1, 0}
        };
        for (int[] offset: offsets) {
            int rowOffset = offset[0];
            int colOffset = offset[1];
            result = depthFirstSearch(row + rowOffset, col + colOffset);
```

# When you need to have a map ascendingly by value

```plaintext
hashmap.entrySet().stream()
        .sorted(Map.Entry<String, Integer> comparingByValue())
        .forEach((fruit)->System.out.println(fruit.getKey() + " -> " + fruit.getValue()));
```

## Lambda way

```java
Map<Character, Integer> frequencies = new HashMap<>();

for (char t : tasks) {
frequencies.put(t, frequencies.getOrDefault(t, 0) + 1);
}

List<Map.Entry<Character, Integer>> sortedFrequencies = new ArrayList<>(frequencies.entrySet());
Collections.sort(sortedFrequencies, (lhs, rhs) -> lhs.getValue().compareTo(rhs.getValue()));
```

# When you need to iterate a map

```jsx
 for(Entry<String, String> entry: languages.entrySet())
```

## PriorityQueue Comparator

```jsx
PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue<>((o1, o2) -> o1.getValue() - o2.getValue());
```

```java
PriorityQueue<Integer> maxHeapForSmallNum; 
PriorityQueue<Integer> minHeapForLargeNum;
PriorityQueue<int[]> capitalMinHeap = new PriorityQueue<>((a, b) -> a[0] - b[0]);
```

```java

maxHeapForSmallNum = new PriorityQueue<>((a, b) -> b - a);
minHeapForLargeNum = new PriorityQueue<>((a, b) -> a - b);
```

## Negative Modulos

```java
(((a % b) + b) % b
```

## Permutations

```java
public List<List<Integer>> permute(int[] nums) {
   List<List<Integer>> list = new ArrayList<>();
   // Arrays.sort(nums); // not necessary
   backtrack(list, new ArrayList<>(), nums);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums){
   if(tempList.size() == nums.length){
      list.add(new ArrayList<>(tempList));
   } else{
      for(int i = 0; i < nums.length; i++){ 
         if(tempList.contains(nums[i])) continue; // element already exists, skip
         tempList.add(nums[i]);
         backtrack(list, tempList, nums);
         tempList.remove(tempList.size() - 1);
      }
   }
}
```

## Sort with a criteria

```java
class SortByNameAndRollNum implements Comparator<Student> {
	// Used for sorting in ascending order of
	// roll name
	public int compare(Student a, Student b) {

		// for comparison
		int NameCompare = a.getName().compareTo(b.getName());
		int RollNumCompare = a.getRollno().compareTo(b.getRollno());

		// 2-level comparison using if-else block
		if (NameCompare == 0) {
			return ((RollNumCompare == 0) ? NameCompare : RollNumCompare);
		} else {
			return NameCompare;
		}

	}
}
```

## QuickSelect

```java
public static int partition(int[] arr, int low,
                                int high)
    {
        int pivot = arr[high], pivotloc = low;
        for (int i = low; i <= high; i++) {
            // inserting elements of less value
            // to the left of the pivot location
            if (arr[i] < pivot) {
                int temp = arr[i];
                arr[i] = arr[pivotloc];
                arr[pivotloc] = temp;
                pivotloc++;
            }
        }
  
        // swapping pivot to the final pivot location
        int temp = arr[high];
        arr[high] = arr[pivotloc];
        arr[pivotloc] = temp;
  
        return pivotloc;
    }
  
    // finds the kth position (of the sorted array)
    // in a given unsorted array i.e this function
    // can be used to find both kth largest and
    // kth smallest element in the array.
    // ASSUMPTION: all elements in arr[] are distinct
    public static int kthSmallest(int[] arr, int low,
                                  int high, int k)
    {
        // find the partition
        int partition = partition(arr, low, high);
  
        // if partition value is equal to the kth position,
        // return value at k.
        if (partition == k - 1)
            return arr[partition];
  
        // if partition value is less than kth position,
        // search right side of the array.
        else if (partition < k - 1)
            return kthSmallest(arr, partition + 1, high, k);
  
        // if partition value is more than kth position,
        // search left side of the array.
        else
            return kthSmallest(arr, low, partition - 1, k);
    }
```

| Comparable | Comparator |
| --- | --- |
| 1) Comparable provides a **single sorting sequence**. In other words, we can sort the collection on the basis of a single element such as id, name, and price. | The Comparator provides **multiple sorting sequences**. In other words, we can sort the collection on the basis of multiple elements such as id, name, and price etc. |
| 2) Comparable **affects the original class**, i.e., the actual class is modified. | Comparator **doesn't affect the original class**, i.e., the actual class is not modified. |
| 3) Comparable provides **compareTo() method** to sort elements. | Comparator provides **compare() method** to sort elements. |
| 4) Comparable is present in **java.lang** package. | A Comparator is present in the **java.util** package. |
| 5) We can sort the list elements of Comparable type by **Collections.sort(List)** method. | We can sort the list elements of Comparator type by **Collections.sort(List, Comparator)** method. |

**String is immutable whereas StringBuffer and StringBuilder are mutable classes**. StringBuffer is thread-safe and synchronized whereas StringBuilder is not. That's why StringBuilder is faster than StringBuffer