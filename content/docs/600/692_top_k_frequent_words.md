+++
title = "692. Top K Frequent Words"
author = ["Ramsay Leung"]
date = 2022-04-29T23:25:00+08:00
lastmod = 2022-05-08T08:19:03+08:00
draft = false
weight = 692
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/top-k-frequent-words/>

Given an array of strings `words` and an integer `k`, return the `k` most frequent strings.

Return the answer `sorted` by `the frequency` from highest to lowest. Sort the words with the same frequency by their `lexicographical order`.

**Example 1**:

```text
Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2**:

```text
Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Constraints**:

-   `1 <= words.length <= 500`
-   `1 <= words[i] <= 10`
-   `words[i]` consists of lowercase English letters.
-   `k` is in the range `[1, The number of unique words[i]]`

**Follow-up**: Could you solve it in `O(n log(k))` time and `O(n)` extra space?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <utility>
#include <algorithm>
#include <unordered_map>
class Solution {
public:
  vector<string> topKFrequent(vector<string>& words, int k) {
    // Space complexity: O(M), N is the size of unique words
    // Time complexity: O(N + N*LogN) => O(N*LogN), N is the size of words.
    std::unordered_map<std::string, int> frequency;
    for(const auto& word: words){
      auto iter = frequency.find(word);
      if(iter == frequency.end()){
	frequency[word] = 1;
      }else{
	iter->second += 1;
      }
    }

    auto cmp = [](const std::pair<std::string, int>& a, const std::pair<std::string, int>& b){
      if(a.second == b.second){
	return a.first > b.first;
      }else{
	return a.second < b.second;
      }

    };
    std::vector<std::pair<std::string, int>> heap;
    heap.reserve(frequency.size());
    for(auto iter = frequency.begin(); iter != frequency.end(); iter ++){
      heap.push_back(*iter);
      std::push_heap(heap.begin(), heap.end(), cmp);
    }

    std::vector<std::string> result;
    while(k > 0 && heap.size() > 0){
      std::pop_heap(heap.begin(), heap.end(), cmp);
      result.push_back(heap.back().first);
      heap.pop_back();
      k--;
    }

    return result;
  }
};
```
