---
title: Leetcode Daily - 7th Feb 2024 (Sort Characters By Frequency)
date: 2024-02-07 22:00:00 +0530
categories: [Leetcode]
tags: [daily, string, stl, sorting, hashing]     # TAG names should always be lowercase
---

# Introduction

**Title**: Sort Characters By Frequency

**Short Problem description**: Sort the characters of a string such that the ones which have a larger frequency of occurence within the string, come first.


**Prerequisites**: Map STL, String, Sorting, Hashing

**Problem Link**: [Link](https://leetcode.com/problems/sort-characters-by-frequency/description/?envType=daily-question&envId=2024-02-01)

## Solution

We start off by storing counts of each character occurence using a map. We need to sort these counts somehow, for which we utilize a vector made with pair STL datastructure. This looks like ```vector <pair<int,char>>```, where we store count in the int parameter, and the actual character as the second parameter.

Note that this works because sorting of pairs first gives importance to the first parameter and only in cases where the first parameters are equal, then proceeds to sort based on the second parameter. Here, the only thing that matters to us is the count. So we use STL sort to obtain an increasing order, then we use STL reverse to get a descending order of count.

Finally we reduce each counts from the pair to get our final result.

## Key points to note.
1. Using map instead of unordered_map can increase the time complexity to O(nlogn) because of their underlying implementations.

## Code for solution

```cpp
string frequencySort(string s) {
    map <char,int> frequency;
    for(auto itr: s)frequency[itr]++;
    vector <pair<int,char>> accumulator;
    for(auto itr: frequency)accumulator.push_back({itr.second,itr.first});
        
    sort(accumulator.begin(),accumulator.end());
    reverse(accumulator.begin(),accumulator.end());

    string ans = "";
    for(auto itr: accumulator) {
        for(int i = 0;i < itr.first;i++)ans += itr.second;
    } 

    return ans;
}
```

