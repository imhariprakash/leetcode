## 13. Roman to Integer

Roman numerals use seven symbols:

| Symbol | Value |
|---|---:|
| I | 1 |
| V | 5 |
| X | 10 |
| L | 50 |
| C | 100 |
| D | 500 |
| M | 1000 |

### Examples
- `2` is written as `II` (two ones).
- `12` is written as `XII` (`X + II`).
- `27` is written as `XXVII` (`XX + V + II`).

### Writing rules
Roman numerals are typically written from left to right in descending order. However, subtraction is used in specific cases:
- `I` can be placed before `V` (5) and `X` (10) to form `4` and `9`.
- `X` can be placed before `L` (50) and `C` (100) to form `40` and `90`.
- `C` can be placed before `D` (500) and `M` (1000) to form `400` and `900`.

Given a Roman numeral string, convert it to an integer.

### Sample inputs/outputs

**Example 1**
- Input: `s = "III"`
- Output: `3`
- Explanation: `III = 3`

**Example 2**
- Input: `s = "LVIII"`
- Output: `58`
- Explanation: `L = 50`, `V = 5`, `III = 3`

**Example 3**
- Input: `s = "MCMXCIV"`
- Output: `1994`
- Explanation: `M = 1000`, `CM = 900`, `XC = 90`, `IV = 4`

### Constraints
- `1 <= s.length <= 15`
- `s` contains only `I`, `V`, `X`, `L`, `C`, `D`, `M`
- `s` is guaranteed to be a valid Roman numeral in the range `[1, 3999]`

---

## Approach 1: Map-based conversion (Roman → Integer)

- Check a 2-character token first (e.g., `IV`, `IX`); if it matches, add its value and skip the next character (`i++`).
- Otherwise, fall back to a 1-character token and continue.
- Note (LeetCode): this approach can be slower due to repeated `substring` calls.

### Solution
```java
import static java.util.Map.entry;
class Solution 
{
    public int romanToInt(String s) 
    {
        Map<String, Integer> romanToNumber = Map.ofEntries(
            entry("I", 1),
            entry("V", 5),
            entry("X", 10),
            entry("L", 50),
            entry("C", 100),
            entry("D", 500),
            entry("M", 1000),
            entry("IV", 4),
            entry("IX", 9),
            entry("XL", 40),
            entry("XC", 90),
            entry("CD", 400),
            entry("CM", 900)
        );
        int result = 0;
        
        for(int i = 0; i < s.length(); i++)
        {
            int endIndex = s.length() > (i + 2) ? (i + 2) : s.length();
            String substring = s.substring(i, endIndex);
            if(romanToNumber.containsKey(substring))
            {
                result += romanToNumber.get(substring);
                i++;
            }
            else
            {
                substring = s.substring(i, i + 1);
                result += romanToNumber.get(substring);
            }
        }
        return result;
    }
}
```

### Result
- Runtime: `8 ms`
- Beats: `6.48%`
