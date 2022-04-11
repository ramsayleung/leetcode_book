+++
title = "190. Reverse Bits"
author = ["Ramsay Leung"]
date = 2022-04-10T20:45:00+08:00
lastmod = 2022-04-11T22:27:54+08:00
draft = false
weight = 190
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/reverse-bits/>

Reverse bits of a given 32 bits unsigned integer.

**Note**:

-   Note that in some languages, such as Java, there is no unsigned integer type. In this case, both input and output will be given as a signed integer type. They should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
-   In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in **Example 2** above, the input represents the signed integer -3 and the output represents the signed integer `-1073741825`.

**Example 1**:

```text
Input: n = 00000010100101000001111010011100
Output:    964176192 (00111001011110000010100101000000)
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.
```

**Example 2**:

```text
Input: n = 11111111111111111111111111111101
Output:   3221225471 (10111111111111111111111111111111)
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
```

**Constraints**:

-   The input must be a **binary string** of length `32`

**Follow up**: If this function is called many times, how would you optimize it?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <bitset>
#include <sstream>
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
	std::string bin_str = std::bitset<32>(n).to_string();
	std::stringstream ss;
	for(int i = bin_str.size() -1 ; i >= 0; i--){
	    ss << bin_str[i];
	}
	std::bitset<32> result{ss.str()};
	return result.to_ulong();
    }
};
```
