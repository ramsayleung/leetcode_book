+++
title = "374. Guess Number Higher or Lower"
author = ["Ramsay Leung"]
date = 2022-04-17T13:09:00+08:00
lastmod = 2022-04-17T13:13:01+08:00
draft = false
weight = 374
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/guess-number-higher-or-lower/>

We are playing the Guess Game. The game is as follows:

I pick a number from `1` to `n`. You have to guess which number I picked.

Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.

You call a pre-defined API `int guess(int num)`, which returns three possible results:

-   `-1`: Your guess is higher than the number I picked (i.e. `num > pick`).
-   `1`: Your guess is lower than the number I picked (i.e. `num < pick`).
-   `0`: your guess is equal to the number I picked (i.e. `num == pick`).

Return the number that I picked.

**Example 1**:

```text
Input: n = 10, pick = 6
Output: 6
```

**Example 2**:

```text
Input: n = 1, pick = 1
Output: 1
```

**Example 3**:

```text
Input: n = 2, pick = 1
Output: 1
```

**Constraints**:

-   `1 <= n <= 2^31 - 1`
-   `1 <= pick <= n`


## <span class="section-num">2</span> Solution {#solution}

```C++
/**
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
  int guessNumber(int n) {
    // Time complexity: O(logN)
    // Space complexity: O(1)
    int low = 1;
    int high = n;
    int mid = 0;
    while(low <= high){
      mid = low + (high - low)/2;
      int is_lower = guess(mid);
      if(is_lower > 0){
	low = mid + 1;
      }else if(is_lower < 0){
	high = mid - 1;
      }else{
	return mid;
      }
    }

    return mid;
  }
};
```
