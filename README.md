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
#### Explanation
```
partition: arr = [24, 28, 14, 82, 8, 58, 64, 12, 94, 29]
let:
lb = 0
ub = n-1 = 9
e = lb
f = ub
num=arr[lb]

1 increment e untill encounter arr[e] which is > num or e == ub
2 decrement f untill encounter arr[e] which is <= num or f==lb
3 if e and f crosses ( e > f) then swap values at index lb and f. return f.
4 if not then swap values at index e and f continue from 1

eg:
arr = [24, 28, 14, 82, 8, 58, 64, 12, 94, 29]
lb = 0, ub = 9, e = 0, f = 9
num = 24
after step 1:
arr = [24, 28, 14, 82, 8, 58, 64, 12, 94, 29]
e = 1
after step 2:
arr = [24, 28, 14, 82, 8, 58, 64, 12, 94, 29]
f = 7
step 3 does not apply
after step 4
arr = [24, 28, 14, 82, 8, 58, 64, 12, 94, 29]
arr = [24, 12, 14, 82, 8, 58, 64, 28, 94, 29]
back to step1
after step1:
arr = [24, 12, 14, 82, 8, 58, 64, 28, 94, 29]
e = 3
after step2:
arr = [24, 12, 14, 82, 8, 58, 64, 28, 94, 29]
f = 4
step3 does not apply
after step 4
arr = [24, 12, 14, 8, 82, 58, 64, 28, 94, 29]
back to step1
after step1
arr = [24, 12, 14, 8, 82, 58, 64, 28, 94, 29]
e = 4
after step2
arr = [24, 12, 14, 8, 82, 58, 64, 28, 94, 29]
f = 3
after step3 (which applies now since e = 4, f = 3 hence e > f)
arr = [8, 12, 14, 24, 82, 58, 64, 28, 94, 29]
** now the element 24 is at the position on which it sould be in a ascending order, all the elements which are greater than this are on the right side and all the smaller elements are on the left side, here the value of f should be returned which is 3 and the parition point **
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
