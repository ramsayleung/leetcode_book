+++
title = "93. Restore IP Addresses"
author = ["Ramsay Leung"]
date = 2022-05-14T13:34:00+08:00
lastmod = 2022-05-14T13:38:58+08:00
draft = false
weight = 93
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/restore-ip-addresses/>

A **valid IP address** consists of exactly four integers separated by single dots. Each integer is between `0` and `255` (**inclusive**) and cannot have leading zeros.

-   For example, `"0.1.2.201"` and `"192.168.1.1"` are **valid** IP addresses, but `"0.011.255.245"`, `"192.168.1.312"` and `"192.168@1.1"` are `invalid` IP addresses.

Given a string `s` containing only digits, return all possible valid IP addresses that can be formed by inserting dots into `s`. You are **not** allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in **any** order.

**Example 1**:

```text
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```

**Example 2**:

```text
Input: s = "0000"
Output: ["0.0.0.0"]
```

**Example 3**:

```text
Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

**Constraints**:

-   `1 <= s.length <= 20`
-   `s` consists of digits only.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <vector>
#include <string>
#include <cstdlib>
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
	// Time complexity: O(N!), N is the size of s.
	// Space complexity: O(N!)
	// faster than 100.00% of C++ online submissions for Restore IP Addresses
	std::vector<std::string> result;
	std::vector<std::string> bytes;
	backtrack(s, bytes , result);
	return result;
    }

    void backtrack(const std::string& input, std::vector<std::string>& bytes, std::vector<std::string>& result){
	if(input.empty() && bytes.size() == 4){
	    std::string ip;
	    for(const auto& b: bytes){
		ip = ip + b + ".";
	    }
	    ip.pop_back();
	    result.push_back(ip);
	}

	for(int i = 1; i<= input.size(); i++){
	    std::string substr = input.substr(0, i);
	    if(!is_valid_ip(substr)){
		continue;
	    }

	    // Cut the all invalid branches
	    if(bytes.size() > 4){
		return;
	    }

	    bytes.push_back(substr);
	    backtrack(input.substr(i), bytes, result);
	    bytes.pop_back();
	}
    }

    bool is_valid_ip(const std::string& ip){
	if(ip.size() > 1 && ip[0] == '0'){
	    return false;
	}

	int digit = std::atoi(ip.c_str());
	if(digit < 0 || digit > 255){
	    return false;
	}

	return true;
    }
};
```
