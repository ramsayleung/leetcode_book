+++
title = "278. First Bad Version"
author = ["Ramsay Leung"]
date = 2022-04-16T21:05:00+08:00
lastmod = 2022-04-16T21:08:03+08:00
draft = false
weight = 278
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/first-bad-version/>

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example 1**:

```text
Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```

**Example 2**:

```text
Input: n = 1, bad = 1
Output: 1
```

**Constraints**:

-   `1 <= bad <= n <= 2 ^ 31 - 1`


## <span class="section-num">2</span> Solution {#solution}

```C++
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
	// it's similar with `git bisect` command
	// time complexity: O(log N)
	// space complexity: O(1)
	int high = n;
	int low = 1;
	int first = 0;
	while(low <= high){
	    int mid = low + (high - low) / 2;
	    bool bad = isBadVersion(mid);
	    if(bad){
		first = mid;
		high = mid - 1;
	    }else{
		low = mid + 1;
	    }
	}

	return first;
    }
};
```
