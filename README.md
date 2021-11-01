# Sum of subarray minimums
## https://leetcode.com/problems/sum-of-subarray-minimums

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
