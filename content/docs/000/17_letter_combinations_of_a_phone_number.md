+++
title = "17. Letter Combinations of a Phone Number"
author = ["Ramsay Leung"]
date = 2020-04-25T21:08:17
lastmod = 2022-05-13T22:23:34+08:00
draft = false
weight = 17
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/letter-combinations-of-a-phone-number/>

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

{{< figure src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png" >}}

Example:

```text
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note**:

Although the above answer is in lexicographical order, your answer could be in any order you want.


## <span class="section-num">2</span> Solution {#solution}

```python
from typing import List


# Runtime: 28 ms, faster than 70.44% of Python3 online submissions for Letter Combinations of a Phone Number.
# time complexity: O(4^n), because "7" and "9" have four letters.
# space complexity: O(4^n)
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
	mapping = {}
	mapping["2"] = ["a", "b", "c"]
	mapping["3"] = ["d", "e", "f"]
	mapping["4"] = ["g", "h", "i"]
	mapping["5"] = ["j", "k", "l"]
	mapping["6"] = ["m", "n", "o"]
	mapping["7"] = ["p", "q", "r", "s"]
	mapping["8"] = ["t", "u", "v"]
	mapping["9"] = ["w", "x", "y", "z"]

	def backtracking(combination: str, digits: str, output: List[str]) -> None:
	    if len(digits) == 0:
		output.append(combination)
		return
	    for letter in mapping[digits[0]]:
		backtracking(combination+letter, digits[1:], output)
		output = []
	if len(digits) > 0:
	    backtracking("", digits, output)
	return output

```

```C++
#include <unordered_map>
#include <vector>
class Solution {
public:
    vector<string> letterCombinations(string digits) {
	// Time complexity: O(3 ^ N), N is the size of digits
	// Space complexity: O(3 ^ N)
	// faster than 100.00% of C++ online submissions for Letter Combinations of a Phone Number.
	std::vector<std::string> result;
	std::vector<std::string> comb;
	backtrack(digits, 0, 0, result, comb);
	return result;
    }

    void backtrack(const std::string& digits, int digit_start, int letter_start, std::vector<std::string>& result, std::vector<std::string>& comb){
	static std::unordered_map<char, std::vector<std::string>> letter_map{
	    {'2', {"a", "b","c"}},
	    {'3', {"d", "e", "f"}},
	    {'4', {"g", "h", "i"}},
	    {'5', {"j", "k", "l"}},
	    {'6', {"m", "n", "o"}},
	    {'7', {"p", "q", "r", "s"}},
	    {'8', {"t", "u", "v"}},
	    {'9', {"w", "x", "y", "z"}}

	};

	if(!digits.empty() && comb.size() == digits.size()){
	    result.push_back(vec2str(comb));
	}

	for(int i = digit_start; i< digits.size(); i++){
	    char c = digits.c_str()[i];
	    for(int j = 0; j < letter_map[c].size(); j++){
		comb.push_back(letter_map[c][j]);
		backtrack(digits, i + 1, j, result, comb);
		comb.pop_back();
	    }
	}
    }

    std::string vec2str(const std::vector<std::string>& comb){
	std::string result;
	for(const auto& s: comb){
	    result += s;
	}
	return result;
    }
};
```
