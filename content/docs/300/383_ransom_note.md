+++
title = "383. Ransom Note"
author = ["Ramsay Leung"]
date = 2022-05-08T08:04:00+08:00
lastmod = 2022-05-08T08:09:26+08:00
draft = false
weight = 383
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/ransom-note/>

Given two strings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed from `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1**:

```text
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2**:

```text
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3**:

```text
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

Constraints:

-   `1 <= ransomNote.length, magazine.length <= 10^5`
-   `ransomNote` and `magazine` consist of lowercase English letters.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <unordered_map>
class Solution {
public:
  bool canConstruct(string ransomNote, string magazine) {
    // Time complexity: O(N + M), N is the size of ransomNode, M is the size of
    // magazine Space complexity: O(26) => O(1)

    // table doubling is expensive,so just preallocating the space
    std::unordered_map<char, int> word_freq(26);

    for (int i = 0; i < magazine.size(); i++) {
      auto iter = word_freq.find(magazine[i]);
      if (iter == word_freq.end()) {
	word_freq[magazine[i]] = 1;
      } else {
	iter->second++;
      }
    }

    for (int i = 0; i < ransomNote.size(); i++) {
      auto iter = word_freq.find(ransomNote[i]);
      if (iter == word_freq.end() || iter->second < 1) {
	return false;
      } else {
	iter->second--;
      }
    }

    return true;
  }
};
```
