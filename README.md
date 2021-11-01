# Sum of subarray minimums
## https://leetcode.com/problems/sum-of-subarray-minimums

Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. 
Since the answer may be large, return the answer modulo 10^9 + 7.

```
Example 1:

Input: arr = [3,1,2,4]
Output: 17
Explanation: 
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4]. 
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.
```

### Naive approach : Sum the min of each subarray.
```
Input: arr = [3,1,2,4]
Subarrays of [3,1,2,4] will be :
[3] , [3,1] , [3,1,2] , [3,1,2,4]
[1] , [1,2] , [1,2,4]
[2] , [2,4]
[4]
```

# Implementation 1 : Overflow issue
```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
        if(arr == null || arr.length == 0)
            return 0;
        
        int sum = 0;
        for(int i = 0; i < arr.length; i++) {
            for(int j = i; j < arr.length; j++) {
                int[] subarr = subarray(arr, i, j);
                int min = getMin(subarr);
                sum += min;
            }
        }
        return sum;
    }
    
    private int[] subarray(int[] arr, int start, int end) {
        int[] num = new int[end-start+1];
        int index = 0;
        for(int i = start; i <= end; i++) {
            num[index++] = arr[i];
        }
        return num;
    }
    
    private int getMin(int[] arr) {
        int min = arr[0];
        for(int i = 1; i < arr.length; i++)
            min = Math.min(min, arr[i]);
        return min;
    }
}
```

## Note : Since the answer may be large, return the answer modulo 10^9 + 7

## Implementation 2 : Time Limit exceeded
```java
class Solution {
    public int sumSubarrayMins(int[] arr) {
        if(arr == null || arr.length == 0)
            return 0;
        
        int sum = 0;
        int mod = (int) 1e9 + 7;
        for(int i = 0; i < arr.length; i++) {
            for(int j = i; j < arr.length; j++) {
                int[] subarr = subarray(arr, i, j);
                int min = getMin(subarr);
                min = min % mod;
                sum += min;
                sum = sum % mod;
            }
        }
        return sum;
    }
    
    private int[] subarray(int[] arr, int start, int end) {
        int[] num = new int[end-start+1];
        int index = 0;
        for(int i = start; i <= end; i++) {
            num[index++] = arr[i];
        }
        return num;
    }
    
    private int getMin(int[] arr) {
        int min = arr[0];
        for(int i = 1; i < arr.length; i++)
            min = Math.min(min, arr[i]);
        return min;
    }
}
```
