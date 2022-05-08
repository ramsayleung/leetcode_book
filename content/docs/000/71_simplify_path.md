+++
title = "71. Simplify Path"
author = ["Ramsay Leung"]
date = 2022-04-30T08:44:00+08:00
lastmod = 2022-05-08T08:16:34+08:00
draft = false
weight = 71
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/simplify-path/>

Given a string `path`, which is an **absolute path** (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical path** should have the following format:

-   The path starts with a single slash `'/'`.
-   Any two directories are separated by a single slash `'/'`.
-   The path does not end with a trailing `'/'`.
-   The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)

Return the simplified **canonical path**.

**Example 1**:

```text
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

**Example 2**:

```text
Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

**Example 3**:

```text
Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

**Constraints**:

-   1 &lt;= path.length &lt;= 3000
-   `path` consists of English letters, digits, period `'.'`, slash `'/'` or `'_'`.
-   `path` is a valid absolute Unix path.


## <span class="section-num">2</span> Solution {#solution}

```C++
#include <vector>
#include <sstream>
class Solution {
public:
    string simplifyPath(string path) {
	// Space complexity: O(D), D is the depth of path.
	// Time complexity: O(D), D is the depth of path.

	std::istringstream is(path);
	std::string token;
	std::vector<std::string> result{"/"};
	while(std::getline(is, token, '/')){
	    if(token == ""){
		continue;
	    }

	    if(result.back() != "/"){
		result.push_back("/");
	    }

	    if(token == ".."){
		int pop_times = 0;

		while(result.size() > 1 && pop_times < 3){
		    result.pop_back();
		    pop_times++;
		}
	    }else if(token == "."){
		if(result.size() > 1){
		    result.pop_back();
		}
	    }else{
		result.push_back(token);
	    }
	}

	std::stringstream ss;
	for(const auto& path: result){
	    ss << path;
	}
	return ss.str();
    }
};
```
