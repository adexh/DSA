### Selection Sort
- Select minimum in a range, and replace from the starting pointer
- Replace `[0]` with `min( [0,n-1] )`, then `[1]` with `min( [1,n-1] )` ...

```Javascript
    for( let i=0; i<nums.length; i++) {
        let min = Infinity;
        let mini = -1;
        
        for( let i2 = i; i2<nums.length; i2++) {
            if( nums[i2] < min ) {
                min = nums[i2];
                mini = i2;
            }
        }
        swap(nums, i, mini);
    }
    return nums;
```

### Bubble Sort
- Bubbles go high
- So make the largest num go to the last by swapping adjacent elements

```Javascript

function bubbleSort(nums) {
	let i = 0;
	while( (i+1) < nums.length ) {
		if( nums[i] > nums[i+1] ) {
			let temp = nums[i];
			nums[i] = nums[i+1];
			nums[i+1] = temp;
			i=0; // This is important, this makes the loop to restart from 0
		} else {
			i++;
		}
	}
	return nums;
}
```

## Insertion Sort
- In a increasing range like `[0,i-1]` make the `i-1` element in the correct place by swapping back

```Javascript
function insertionSort(nums) {
	for(let i=1; i<nums.length; i++) {
		for(let j=i; j>0; j--) {
			if( nums[j-1] <= nums[j] ) break; // Since its in correct position
			swap(nums, j, j-1);
		}
	}
	return nums;
}
```

### Merge Sort
- Divide the array, and then merge into one by comparing from the divided

```javascript
  

function mergeSort(nums) {
    divide(nums, 0, nums.length-1);
    return nums;
}

function divide(nums, l, r){
    if( l<r ) {
        let m = Math.floor((l + r) / 2);;
        divide(nums, l, m);
        divide(nums, m+1, r);

        merge(nums, l, m, r);
    }
}
  
function merge(nums, l, m, r) {

	//Slice is slice(start-0-based-index, end-1-based-index)
    let larr = nums.slice(l,m+1);
    let rarr = nums.slice(m+1,r+1);
  
    let k = l;
    let ll = 0;
    let rr = 0;
    
    while( ll<larr.length && rr<rarr.length ) {
        if( larr[ll] <= rarr[rr] ) {
            nums[k] = larr[ll++];
        } else {
            nums[k] = rarr[rr++];
        }
        k++;
    }

    while( ll<larr.length ) {
        nums[k++] = larr[ll++];
    }
    
    while( rr<rarr.length ) {
        nums[k++] = rarr[rr++];
    }

}
```

### Quick-Sort
- Select a pivot, place it at its correct position, return the partition
- user partition to sort the left and right array

```Javascript
class Solution {
	
    quickSort(nums) {
        let n = nums.length;
        this.qs(nums, 0, n - 1);
        return nums;
    }

	// The quicksort helper function
    qs( nums, low, high ) {
    
        if( low < high ) {
	        // Get 
            let pIndex = this.pivotSort(nums, low, high);
            this.qs(nums, low, pIndex - 1);
            this.qs(nums, pIndex + 1, high);
        }
    }

  
    pivotSort( nums, low, high ) {

        let pivot = nums[low];
        let i = low;
        let j = high;

        while( i<j ) {
            while( i <= high-1 && nums[i] <= pivot ) {
                i++;
            }
  
            while( j>=low+1 && nums[j] > pivot  ){
                j--;
            }
  
            if( i<j ) {
                [nums[i], nums[j]] = [nums[j], nums[i]];
            }
        }

        [nums[low], nums[j]] = [nums[j], nums[low]];

        return j;
    }
}
```


![[assets/Pasted image 20241107152728.png]]