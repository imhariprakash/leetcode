# 961. N-Repeated Element in Size 2N Array

You are given an integer array `nums` with the following properties:

- `nums.length == 2 * n`
- `nums` contains `n + 1` unique elements
- Exactly one element of `nums` is repeated `n` times

Return the element that is repeated `n` times.

## Examples

### Example 1
- **Input:** `nums = [1,2,3,3]`  
- **Output:** `3`

### Example 2
- **Input:** `nums = [2,1,2,5,3,2]`  
- **Output:** `2`

### Example 3
- **Input:** `nums = [5,1,5,2,5,3,5,4]`  
- **Output:** `5`

## Constraints

- `2 <= n <= 5000`
- `nums.length == 2 * n`
- `0 <= nums[i] <= 10^4`
- `nums` contains `n + 1` unique elements and one of them is repeated exactly `n` times.

## Brute solution

```java
class Solution 
{
    public int repeatedNTimes(int[] nums) 
    {
        for(int i = 0; i < nums.length; i++)
        {
            for(int j = i + 1; j < nums.length; j++)
            {
                if(nums[i] == nums[j])
                {
                    return nums[i];
                }
            }
        }
        return -1;
    }
}
```

## Runtime (**Best:** `0ms`)

- `2 ms`  
- Beats `54.01%`

## Optimal Solution 1 (1 ms) — Using HashSet

**Approach:**
- Use a `HashSet` to keep track of already visited elements.
- Traverse the array:
  - If the current element is already present in the set, it is the repeated element — return it.
  - Otherwise, add the element to the set.
- Since exactly one element is repeated `N` times, the duplicate is guaranteed to be found.

**Code:**
```
class Solution 
{
    public int repeatedNTimes(int[] nums) 
    {
        Set<Integer> visitedElements = new HashSet<>();
        for(int i = 0; i < nums.length; i++)
        {
            if(visitedElements.contains(nums[i]))
            {
                return nums[i];
            }
            visitedElements.add(nums[i]);
        }
        return -1;
    }
}

//Using standard for loop: (won't make a difference)
class Solution 
{
    public int repeatedNTimes(int[] nums) 
    {
        Set<Integer> visitedElements = new HashSet<>();
        for(int num : nums)
        {
            if(!visitedElements.add(num))
            {
                return num;
            }
        }
        return -1;
    }
}
