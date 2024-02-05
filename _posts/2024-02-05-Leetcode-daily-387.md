---
title: Leetcode Daily - 5th Feb 2024 (First Unique Character in a String)
date: 2024-02-05 22:00:00 +0530
categories: [Leetcode]
tags: [daily, string, stl, hashing]     # TAG names should always be lowercase
---

# Introduction

**Title**: First Unique Character in a String

**Short Problem description**: Find index of first non-repeating character in String.


**Prerequisites**: Map STL, String, Hashing

**Problem Link**: [Link](https://leetcode.com/problems/first-unique-character-in-a-string/description/?envType=daily-question&envId=2024-02-05)

## Solution
Consider having two maps.
1. Stores the count of each character
2. Stores the last location in which a character occured

For a character to be not repeating, it should have a count of 1 in our first map. So therefore, for every character that has a count of 1, we take the minimum value of their positions from the second map.

Note that the order of the characters present doesn't matter, therefore we can use unordered_map to reduce the time complexity to O(n).

## Key points to note.
1. Using map instead of unordered_map can increase the time complexity to O(nlogn) because of their underlying implementations.
2. Map can be replaced with Array for this problem as there are only 26 different alphabets. Each array access can be made as ```array[s[i] - 'a']``` to get their indices between the range 0 to 25. This still has the complexity as O(n), but can slightly improve the memory overhead.

## Code for solution

```cpp
int firstUniqChar(string s) {
    unordered_map <char,int> count, position;

    int ans = INT_MAX;
    for (int i = 0;i < s.length();i++) {
        count[s[i]]++;
        position[s[i]] = i;
    }

    for (auto itr: count) {
        // when parsing through an iterator, we get an iterator that has the key in its .first location and value in it's .second location
        // Here for every value that is 1 (count of character is 1), we take the last seen location of the corresponding key in the second map.
        // Minimum of all these gives us the answer
        if(itr.second == 1)ans = min(ans,position[itr.first]);
    }

    return ans == INT_MAX ? -1 : ans;
}
```