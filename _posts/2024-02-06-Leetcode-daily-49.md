---
title: Leetcode Daily - 6th Feb 2024 (Group Anagrams)
date: 2024-02-06 14:00:00 +0530
categories: [Leetcode]
tags: [daily, string, stl, hashing]     # TAG names should always be lowercase
---

# Introduction

**Title**: Group Anagrams

**Short Problem description**: Group all strings that are anagrams of each other.


**Prerequisites**: Map STL, String, Hashing

**Problem Link**: [Link](https://leetcode.com/problems/first-unique-character-in-a-string/description/?envType=daily-question&envId=2024-02-05)


## Intuition

Two strings are anagrams of each other if we get the same strings upon sorting them. So we sort each string, and map them to their sorted version.

## Solution

We declare a datastructure to store the sorted string and map them to the required answer. This shall be of the format ```map <string,vector <string> > anagrams```.

![Desktop View](/assets/img/feb6th.jpeg){: width="500" height="500" }_Diagram explaining the grouping logic_

For each string s, we first sort it to obtain string t, and store s for our key t in our map. At the end of the doing this for each string, we simply traverse across our map and aggregate each value position (present as the second component of map) with help of a vector and that gives us the answer.

## Code for solution

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    map <string,vector <string> > anagrams;

    for(int i = 0;i < strs.size();i++) {
        string t = strs[i];
        sort(t.begin(),t.end());
        anagrams[t].push_back(strs[i]);
    }

    vector <vector<string>> ans;
    for(auto x: anagrams){
        ans.push_back(x.second);
    }

    return ans;
}
```

## Alternate solution

1. We could hash the string to the count of characters present in them. For example, the string "apple" would be converted to "a1 e1 l1 p2" (without space). This would remove the logarithmic time sort. But note that the complexity would still be O(nlogn) because we still have t use map.
