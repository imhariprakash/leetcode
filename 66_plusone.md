# Plus One

## Problem Statement

You are given a large integer represented as an integer array `digits`, where each `digits[i]` is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

## Examples

### Example 1:
```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```

### Example 2:
```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```

### Example 3:
```
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```

## Constraints

- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`
- `digits` does not contain any leading 0's.

## Approach

- If the current digit is **less than 9**, increment it by 1 and return the array.
- If the current digit is **9**, set it to `0` and carry over to the previous digit (towards the most significant digit).
- If all digits are `9`, the number overflows and a new array is created with an additional leading `1`.

## Solutions

### Solution 1: While Loop

```java
class Solution 
{
    public int[] plusOne(int[] digits) 
    {
        boolean isNumberYetToIncrementedByOne = Boolean.TRUE;
        int digitToIncrement = digits.length - 1;
        while(isNumberYetToIncrementedByOne && digitToIncrement > -1)
        {
            boolean isDigitLessThenTen = (digits[digitToIncrement] + 1) < 10;
            if(isDigitLessThenTen)
            {
                ++digits[digitToIncrement];
                return digits;
            }
            digits[digitToIncrement--] = 0;
        }
        int[] sizeIncreasedDigits = new int[digits.length + 1];
        ++sizeIncreasedDigits[0];
        return sizeIncreasedDigits;
    }
}
```

**Performance:**
- Runtime: `0 ms` (Beats 100.00%)
- Test cases: 112/112 passed

### Solution 2: For Loop

```java
class Solution 
{
    public int[] plusOne(int[] digits) 
    {
        boolean isNumberYetToIncrementedByOne = Boolean.TRUE;
        int digitToIncrement = digits.length - 1;
        for(int i = digitToIncrement; i > -1; i--)
        {
            boolean isDigitLessThenNine = (digits[i]) < 9;
            if(isDigitLessThenNine)
            {
                ++digits[i];
                return digits;
            }
            digits[i] = 0;
        }
        int[] sizeIncreasedDigits = new int[digits.length + 1];
        ++sizeIncreasedDigits[0];
        return sizeIncreasedDigits;
    }
}
```

### Solution 3: Optimized (Recommended)

More memory efficient with better readability.

```java
class Solution 
{
    public int[] plusOne(int[] digits) 
    {
        for(int i = digits.length - 1; i > -1; i--)
        {
            if(digits[i] < 9)
            {
                ++digits[i];
                return digits;
            }
            digits[i] = 0;
        }
        int[] sizeIncreasedDigits = new int[digits.length + 1];
        ++sizeIncreasedDigits[0];
        return sizeIncreasedDigits;
    }
}
```

**Performance:**
- Runtime: `0 ms` (Beats 100.00%)
