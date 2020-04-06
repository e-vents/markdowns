```java
//Selection-Sort
public void selectionSort(int[] array){
	for (int i = 0; i < array.length-1; i++){
		int smallest = i;
		for (int j = i+1; j < array.length; j++){
			if (array[j] < array[smallest])
				smallest = j;
		}
		this.swap(array, i, smallest);
	}
}	
		
//Insertion-Sort	
public void insertionSort(int[] array) {
	for (int i=1; i<array.length; i++)      // insert i-th record
		for (int j=i; (j>0) && (array[j]<array[j-1]); j--)
			this.swap(array, j, j-1);  // bubble into correct position
}
				
//Merge-Sort
public void mergeSort(int[] array, int p, int r) {
	if(p<r){
		int q=(p+r)/2;
		this.mergeSort(array, p, q);
		this.mergeSort(array, q+1, r);
		this.merge(array, p, q, r);
	}
}
		
//Quick-Sort
public  void quickSort(int[] array, int p, int r) {
	if (p<r){
		int q = partition(array,p,r);
		this.quickSort(array, p, q-1);
		this.quickSort(array, q+1, r);
	}
}
```