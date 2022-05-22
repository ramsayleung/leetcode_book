+++
title = "131. Palindrome Partitioning"
author = ["Ramsay Leung"]
date = 2022-05-14T13:30:00+08:00
lastmod = 2022-05-14T13:39:02+08:00
draft = false
weight = 131
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/palindrome-partitioning/>

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1**:

```text
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

**Example 2**:

```text
Input: s = "a"
Output: [["a"]]
```

**Constraints**:

-   `1 <= s.length <= 16`
-   `s` contains only lowercase English letters.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
class Solution {
public:
    vector<vector<string>> partition(string s) {
	// Time complexity: O(N!) N is the size of s
	// Space complexity: O(N!)
	std::vector<std::vector<std::string>> result;
	std::vector<std::string> partition_str;
	backtrack(s, result, partition_str);
	return result;
    }

    void backtrack(const std::string& input, std::vector<std::vector<std::string>>& result, std::vector<std::string>&partition){
	if(input.empty()){
	    result.push_back(partition);
	}

	for(int i = 1; i <= input.size(); i++){
	    std::string substr = input.substr(0, i);
	    if(!isPalindrome(substr)){
		continue;
	    }

	    partition.push_back(substr);
	    backtrack(input.substr(i), result, partition);
	    partition.pop_back();
	}
    }

    bool isPalindrome(const std::string& input){
	int size = input.size() ;
	int med = size/2;
	for(int i = 0 ; i < med; i++){
	    if(input[i] != input[size - 1 - i]){
		return false;
	    }
	}
	return true;
    }

};
```
