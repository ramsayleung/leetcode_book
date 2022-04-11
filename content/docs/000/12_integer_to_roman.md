+++
title = "12. Integer to Roman"
author = ["Ramsay Leung"]
date = 2022-04-10T15:12:00+08:00
lastmod = 2022-04-11T22:27:29+08:00
draft = false
weight = 12
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/integer-to-roman/>

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```text
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

-   `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
-   `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
-   `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.

**Example 1**:

```text
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
```

**Example 2**:

```text
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

**Example 3**:

```text
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

**Constraints**:

-   `1 <= num <= 3999`


## <span class="section-num">2</span> Solution {#solution}

```c++
#include <sstream>
#include <utility>
#include <vector>
class Solution {
public:
    string intToRoman(int num) {
	// Runtime complexity: O(n), n is time to divide num.
	// Space complexity: O(n)
	static std::vector<std::pair<std::string, int>> rimap{
	    {"M", 1000},
	    {"CM", 900},
	    {"D", 500},
	    {"CD", 400},
	    {"C", 100},
	    {"XC", 90},
	    {"L", 50},
	    {"XL", 40},
	    {"X", 10},
	    {"IX", 9},
	    {"V", 5},
	    {"IV", 4},
	    {"I", 1}
	};

	std::stringstream result;
	while(num > 0){
	    for(auto iter = rimap.begin(); iter != rimap.end(); iter++){
		if(num >= iter->second){
		    int times = num / iter-> second;
		    repeat(times, iter->first, result);
		    num = num % iter->second;
		}
	    }
	}
	return result.str();
    }

    void repeat(int times, const std::string& source, std::stringstream& stream){
	while(times > 0){
	    stream << source;
	    times --;
	}
    }
};
```
