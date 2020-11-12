# Core logics

## Table of Contents
- [Linked List](#linked-list)
    - [Reverse](#reverse)
    - [Reverse K](#reverse-k)
- [Arrays](#arrays)
    - [Quick sort partition](#quick-sort-partition)
    - [k Smallest](#k-smallest)
    - [sort 0 1 2](#sort-0-1-2)
    - [rotate](#rotate)
    - [Kadane Algo](#kadane-algo)

## Linked List

### Reverse

```java 
Node current = start;
Node prev = null;
while(current != null){
  Node nxt = current.next;
  current.next = prev;
  prev = current;
  current = nxt;
}
start = prev;
```
### reverse k

```java 
Node current = head;
Node prev = null;
Node next = null;
int i = 0;
while(i < k && current != null){
    next = current.next;
    current.next = prev;
    prev = current;
    current = next;
	  i++;
}
if(next!=null)head.next = reverse(next,k);
return prev;
```

## Arrays
### Quick sort partition
```java 
	int partition(int arr[],int p,int q){
		int piv = q;
		int i = p;
		for(int j = p; j<q; j++){
			if(arr[j] > arr[piv]){
				int temp = arr[i];
				arr[i] = arr[j];
				arr[j] = temp;
				i++;
			}
		}
		int temp = arr[piv];
		arr[piv] = arr[i];
		arr[i] = temp;
		return i;
	}
```
### k Smallest
```java 
	int k_smallest(int arr[],int p, int q, int i){
		if(p>=q) return q;
		int r = partition(arr,p,q);
	    int k = p - r + 1; // rank of r in arr
	    if(k == i) return arr[r];
	    if(i > k){
	    	return k_smallest(arr,r+1,q,k-i);
	    }
	    return k_smallest(arr,p,r-1,i);
	}
```

### sort 0 1 2
```java 
void sort(int arr[]){
		int low = 0;
		int mid = 0;
		int high = arr.length - 1;
		int i = 0;
		while(i<=high){
			if(arr[i] == 0){
			    swap(arr,low,i);
			    low++;
			    mid++;
			}
			else if(arr[i] == 1) {
				swap(arr,mid,i);
				mid++;
			}else if(arr[i] == 2){
				swap(arr,high,i);
				high--;
				continue;
			}
			i++;
		}	
	}
```

### rotate 
```java
reverse(arr,0,k-1);
reverse(arr,k,arr.length-1);
reverse(arr,0,arr.length-1);
```

### Kadane Algo

```java
int findMaximumSum(int arr[]){
	int maxendinghere = 0;
	int max = 0;
	for(int n: arr){
	  maxendinghere = math.max(maxendinghere+n,n);
	  max = math.max(maxendinghere,max);
	}
	return max;
}
```
