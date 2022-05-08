+++
title = "56. Merge Intervals"
author = ["Ramsay Leung"]
date = 2020-04-27T22:55:01
lastmod = 2022-05-08T08:17:07+08:00
draft = false
weight = 56
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/merge-intervals/>

Given a collection of intervals, merge all overlapping intervals.

**Example 1**:

```text
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2**:

```text
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**NOTE**: input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.


## <span class="section-num">2</span> Solution {#solution}

```python
from typing import List
# time complexity: O(nlogn), time to sort intervals.
# space complexity: O(1)
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
	size = len(intervals)
	if size <=1:
	    return intervals
	# sorted
	merged = []
	intervals.sort(key = lambda x: x[0])
	for interval in intervals:
	    if not merged or merged[-1][1]<interval[0]:
		merged.append(interval)
	    else:
		merged[-1][1] = max(merged[-1][1], interval[1])
	return merged

```

```C++
#include <algorithm>
class Solution {
public:
  vector<vector<int>> merge(vector<vector<int>>& intervals) {
    std::sort(intervals.begin(), intervals.end());

    std::vector<std::vector<int>> merged;
    for(const auto& interval: intervals){
      if(merged.empty() || merged.back()[1] < interval[0]){
	merged.push_back(interval);
      }else{
	// there is an overlap
	merged.back()[1] = std::max(merged.back()[1], interval[1]);
      }
    }

    return merged;
  }
};
```
