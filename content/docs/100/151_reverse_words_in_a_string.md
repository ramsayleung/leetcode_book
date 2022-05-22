+++
title = "151. Reverse Words in a String"
author = ["Ramsay Leung"]
date = 2022-05-18T22:23:00+08:00
lastmod = 2022-05-18T22:28:09+08:00
draft = false
weight = 151
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/reverse-words-in-a-string/>

Given an input string `s`, reverse the order of the `words`.

A `word` is defined as a sequence of non-space characters. The `words` in `s` will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

`Note` that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1**:

```text
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2**:

```text
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3**:

```text
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

**Constraints**:

-   `1 <= s.length <= 10^4`
-   `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
-   There is `at least one` word in `s`.

**Follow-up**: If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <sstream>
class Solution {
public:
  string reverseWords(string s) {
    // Time complexity: O(N), N is the size of s
    // Space complexity: O(N)
    int last_index = s.size() - 1;

    std::string result;
    std::string word;
    while(last_index >= 0){
      if(s[last_index] == ' '){
	if(!word.empty()){
	  result = result.empty() ? word : result + " " + word;
	}
	word = "";
      }else{
	word = s[last_index] + word;
      }
      last_index--;
    }

    if(!word.empty()){
      result = result.empty() ? word : result + " " + word;
    }

    return result;
  }
};
```
