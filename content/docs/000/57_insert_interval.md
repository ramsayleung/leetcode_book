+++
title = "57. Insert Interval"
author = ["Ramsay Leung"]
date = 2022-04-30T08:36:00+08:00
lastmod = 2022-05-08T08:16:55+08:00
draft = false
weight = 57
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/insert-interval/>

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

**Example 1**:

```text
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

**Example 2**:

```text
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

**Constraints**:

-   `0 <= intervals.length <= 10^4`
-   `intervals[i].length == 2`
-   `0 <= starti <= endi <= 10^5`
-   intervals is sorted by `starti` in **ascending** order.
-   `newInterval.length == 2`
-   `0 <= start <= end <= 10^5`


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <algorithm>
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
      // Space complexity: O(N), N is the size of intervals
      // Time complexity: O(N)
	std::vector<std::vector<int>> merged;
	for(auto iter = intervals.begin(); iter != intervals.end(); iter++){
	    auto interval = *iter;
	    //  the newInterval is less than the current interval, since the intervals is in ascending order, therefore there is no chance to have overlapping any more, just return
	    if(newInterval[1] < interval[0]){
		merged.push_back(newInterval);
		std::copy(iter, intervals.end(), std::back_inserter(merged));
		return merged;
	    }else if(interval[1] < newInterval[0]){
	    // There is no overlapping here since the left value of newInterval is greater than the right value of interval.
		merged.push_back(interval);
	    }else{
		// Create a new `newInterval` with maximium range.
		newInterval = {std::min(newInterval[0], interval[0]), std::max(newInterval[1], interval[1])};
	    }
	}

	merged.push_back(newInterval);

	return merged;
    }
};
```
