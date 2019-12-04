---
title: "The Moment I Realized The Importance Of Data Structures & Algorithms"
date: "2019-12-04"
featuredImage: './image.jpg'
---

Data Structures and Algorithms is a topic that inevitably comes up when learning how to program. When I was first introduced to this subject, I knew it was something that needed to be understood but I couldn't quite figure out how to explain its relevance. It was too abstract and I didn't have enough experience to truly appreciate its importance.

However, recently, I ran into a situation where I could understand its relevance in clearer terms. I wanted to share this example in this post where I realized the importance of choosing the correct data structure for the problem you're trying to solve.

I've been working through some LeetCode problems in preparation for future whiteboarding challenges. Python is my go-to for these types of problems because the syntax is clear and easy to understand. Whenever I solve one of these problems, I sometimes will bring up the problem and solution to my girlfriend who also can write some Python.

Here's the LeetCode problem that inspired this post.

### Contains Duplicate - [Leetcode Link](https://leetcode.com/problems/contains-duplicate/)

__Problem Statement__: Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

#### My Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        tracker = {}

        for i in nums:
            if i not in tracker:
                tracker[i] = 1
            else:
                return True

        return False
```

The above code in plain english:

1. Create an empty dictionary which will be used to look up values
2. Loop through the list of integers that are passed into the function
3. If the element in the list of integers is not in the dictionary, set that element in the list as a key in the dictionary with the value of 1
4. If the element is already in the dictionary, return True as per the problem description because that means that element appeared twice
5. Continue doing #3 and #4 until we find a duplicate or we loop over the entire input
6. After going through the whole list of integers, if True was never returned, return False because none of the integers were duplicates

My solution passed 18/18 of the test cases on LeetCode.

When I shared my solution with my girlfriend, she asked me to explain why I used a dictionary instead of using a list as storage. I couldn't explain why so she refactored my algorithm and that's when we both learned something new. 

Let's take a look at her solution.

#### Girlfriend's Solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        tracker = []

        for i in nums:
            if i not in tracker:
                tracker.append(i)
            else:
                return True

        return False
```

The above code in plain english:

1. Create an empty list called "tracker" which will be used to lookup values
2. Loop through the list of integers that are passed into the function
3. If the element in the list is not in tracker, add that element into tracker
4. If the element is already in tracker, return True as per the problem description because that means that element appeared twice
5. Continue doing #3 and #4 until we find a duplicate or we loop over the entire input
6. After going through the whole list of integers, if True was never returned, return False because none of the integers were duplicates

This solution worked for 17/18 test cases on LeetCode but on the 18th one, the Time Limit was Exceeded and the problem was considered unsolved. We looked at each other with confused expressions when we saw that result. Her logic was practically the same but the algorithm took too long to process?

We examined the list that was used in the 18th test case and saw that it was a list of numbers starting at -24500 incrementing by +1. We knew that the logic "works" because 17/18 test cases were passed so we concluded that the size of the input was the problem. Something about this algorithm was handling a list of 24,500 integers too slowly.

So this is when it clicked for me. I learned that the underlying data structure behind a Python dictionary is a hash table. After googling around I came across the following.

> If you could choose to store things that you’d want to look up later in a Python dictionary or in a Python list, which would you choose?
>It turns out that looking up items in a Python dictionary is much faster than looking up items in a Python list. If you search for a fixed number of keys, if you grow your haystack size (i.e. the size of the collection you’re searching through) by 10,000x from 1k entries to 10M entries, using a dict is over 5000x faster than using a list! (Source: Fluent Python by Luciano Ramalho) 

[Source: Jessica Yung's Blog](http://www.jessicayung.com/how-python-implements-dictionaries/)

After it's all said and done, if I ever get asked why I used a dictionary to help with lookup values, I'll be able to give an explanation. Even with the same logic, using the optimum data structure for the problem you're trying to solve can result in better performance and time saved. This concept seems to be especially important when dealing with large amounts of data.

If it wasn't for my girlfriend asking me to explain my thought process, I wouldn't have learned this topic and this post would not have been created as I had luckily implemented a fast solution but couldn't explain why it worked. Creating a solution that works but you can't explain why it does is just as bad as developing a solution that doesn't work at all, in my opinion.

Thank you for reading this far.