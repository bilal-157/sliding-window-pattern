# sliding-window-pattern

643. Maximum Average Subarray I
Solved
Easy
Topics
Companies
You are given an integer array nums consisting of n elements, and an integer k.

Find a contiguous subarray whose length is equal to k that has the maximum average value and return this value. Any answer with a calculation error less than 10-5 will be accepted.

 

Example 1:

Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation: Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
Example 2:

Input: nums = [5], k = 1
Output: 5.00000

SOLUTION : 

class Solution(object):
    def findMaxAverage(self, nums, k):
        
        # Step 1: we need to variables to store the sum
        max_sum = current_sum = sum(nums[:k])
        
        # Step 2: Sliding window technique will start from here
        for i in range(k, len(nums)):
            # Update the current sum: subtract the element going out, add the element coming in
            current_sum += nums[i] - nums[i - k]
            # Update max_sum if the current_sum is larger
            max_sum = max(max_sum, current_sum)
        
        # Step 3: Return the maximum average
        return max_sum / float(k)

1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold
Solved
Medium
Topics
Companies
Hint
Given an array of integers arr and two integers k and threshold, return the number of sub-arrays of size k and average greater than or equal to threshold.

 

Example 1:

Input: arr = [2,2,2,2,5,5,5,8], k = 3, threshold = 4
Output: 3
Explanation: Sub-arrays [2,5,5],[5,5,5] and [5,5,8] have averages 4, 5 and 6 respectively. All other sub-arrays of size 3 have averages less than 4 (the threshold).
Example 2:

Input: arr = [11,13,17,23,29,31,7,5,2,3], k = 3, threshold = 5
Output: 6
Explanation: The first 6 sub-arrays of size 3 have averages greater than 5. Note that averages are not integers.

SOLUTION : 

class Solution(object):
    def numOfSubarrays(self, arr, k, threshold):
        current_sum = sum(arr[:k])
        result = 0

        if current_sum / k >= threshold:
            result += 1

        for i in range(k, len(arr)):
            current_sum += arr[i] - arr[i - k]

            if current_sum / k >= threshold:
                result += 1

        return result

567. Permutation in String
Solved
Medium
Topics
Companies
Hint
Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

 

Example 1:

Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
Example 2:

Input: s1 = "ab", s2 = "eidboaoo"
Output: false

SOLUTION : 

from collections import Counter

class Solution(object):
    def checkInclusion(self, s1, s2):
        # Step 1: If s1 is longer than s2, return False
        if len(s1) > len(s2):
            return False
        
        # Step 2: Create frequency counters for s1 and the initial window of s2
        count_s1 = Counter(s1)
        count_window = Counter(s2[:len(s1)])  # First window in s2
        
        # Step 3: Check the first window
        if count_s1 == count_window:
            return True
        
        # Step 4: Slide the window over s2
        for i in range(len(s1), len(s2)):
            # Include the new character at the end of the window
            count_window[s2[i]] += 1
            
            # Remove the old character from the start of the window
            count_window[s2[i - len(s1)]] -= 1
            if count_window[s2[i - len(s1)]] == 0:
                del count_window[s2[i - len(s1)]]
            
            # Step 5: Check if the current window is a permutation of s1
            if count_s1 == count_window:
                return True
        
        return False

438. Find All Anagrams in a String
Solved
Medium
Topics
Companies
Given two strings s and p, return an array of all the start indices of p's anagrams in s. You may return the answer in any order.

 

Example 1:

Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

Input: s = "abab", p = "ab"
Output: [0,1,2]
Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

SOLUTION : 

import collections
class Solution:
    def findAnagrams(self, s, p):
        myDictP = collections.Counter(p)
        myDictS = collections.Counter(s[:len(p)])
        result = []
        i = 0
        j = len(p)

        while j <= len(s):  # include the last window too
            if myDictP == myDictS:
                result.append(i)

            myDictS[s[i]] -= 1
            if myDictS[s[i]] <= 0:
                myDictS.pop(s[i])

            if j < len(s):
                myDictS[s[j]] += 1

            i += 1
            j += 1
        
        return result
        
1876. Substrings of Size Three with Distinct Characters
Solved
Easy
Topics
Companies
Hint
A string is good if there are no repeated characters.

Given a string s​​​​​, return the number of good substrings of length three in s​​​​​​.

Note that if there are multiple occurrences of the same substring, every occurrence should be counted.

A substring is a contiguous sequence of characters in a string.

 

Example 1:

Input: s = "xyzzaz"
Output: 1
Explanation: There are 4 substrings of size 3: "xyz", "yzz", "zza", and "zaz". 
The only good substring of length 3 is "xyz".
Example 2:

Input: s = "aababcabc"
Output: 4
Explanation: There are 7 substrings of size 3: "aab", "aba", "bab", "abc", "bca", "cab", and "abc".
The good substrings are "abc", "bca", "cab", and "abc".

SOLUTION : 

class Solution(object):
    def countGoodSubstrings(self, s):
        count = 0

        for i in range(len(s)-2):
            
            window = s[i:i+3]

            if len(set(window))==3:
                count += 1
                
        return count

3. Longest Substring Without Repeating Characters
Solved
Medium
Topics
Companies
Hint
Given a string s, find the length of the longest substring without duplicate characters.

 

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

SOLUTION : 

class Solution(object):
    def lengthOfLongestSubstring(self, s):
        result = set()  # To store unique characters in the current window
        left = 0        # Left pointer of the sliding window
        max_length = 0  # To track the maximum length of the substring

        for right in range(len(s)):  # Iterate over the string with the right pointer
            # If the character at `right` is a duplicate, shrink the window
            while s[right] in result:
                result.remove(s[left])  # Remove the character at the `left` pointer
                left += 1               # Move the `left` pointer to the right

            # Add the current character to the set and calculate the max length
            result.add(s[right])
            max_length = max(max_length, right - left + 1)

        return max_length


209. Minimum Size Subarray Sum
Solved
Medium
Topics
Companies
Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

 

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
Example 2:

Input: target = 4, nums = [1,4,4]
Output: 1
Example 3:

Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0

SOLUTION : 

class Solution(object):
    def minSubArrayLen(self, target, nums):
        left=0
        min_length=float('inf')
        current_sum=0

        for right in range(len(nums)):
            current_sum += nums[right]

            while current_sum>= target:
                min_length = min(min_length, right-left+1)
                current_sum -= nums[left]
                left +=1
        return min_length if min_length != float('inf') else 0

904. Fruit Into Baskets
Solved
Medium
Topics
Companies
You are visiting a farm that has a single row of fruit trees arranged from left to right. The trees are represented by an integer array fruits where fruits[i] is the type of fruit the ith tree produces.

You want to collect as much fruit as possible. However, the owner has some strict rules that you must follow:

You only have two baskets, and each basket can only hold a single type of fruit. There is no limit on the amount of fruit each basket can hold.
Starting from any tree of your choice, you must pick exactly one fruit from every tree (including the start tree) while moving to the right. The picked fruits must fit in one of your baskets.
Once you reach a tree with fruit that cannot fit in your baskets, you must stop.
Given the integer array fruits, return the maximum number of fruits you can pick.

 

Example 1:

Input: fruits = [1,2,1]
Output: 3
Explanation: We can pick from all 3 trees.
Example 2:

Input: fruits = [0,1,2,2]
Output: 3
Explanation: We can pick from trees [1,2,2].
If we had started at the first tree, we would only pick from trees [0,1].
Example 3:

Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: We can pick from trees [2,3,2,2].
If we had started at the first tree, we would only pick from trees [1,2].

SOLUTION : 

class Solution(object):
    def totalFruit(self, fruits):
        basket = {}
        max_fruits = 0
        left = 0

        for right in range(len(fruits)):  # Fixed: removed -1
            basket[fruits[right]] = basket.get(fruits[right], 0) + 1

            while len(basket) > 2:
                basket[fruits[left]] -= 1
                if basket[fruits[left]] == 0:
                    del basket[fruits[left]]
                left += 1
            
            max_fruits = max(max_fruits, right - left + 1)  # Fixed: proper indentation
        
        return max_fruits

1248. Count Number of Nice Subarrays
Solved
Medium
Topics
Companies
Hint
Given an array of integers nums and an integer k. A continuous subarray is called nice if there are k odd numbers on it.

Return the number of nice sub-arrays.

 

Example 1:

Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].
Example 2:

Input: nums = [2,4,6], k = 1
Output: 0
Explanation: There are no odd numbers in the array.
Example 3:

Input: nums = [2,2,2,1,2,2,1,2,2,2], k = 2
Output: 16

SOLUTION : 

class Solution(object):
    def numberOfSubarrays(self, nums, k):
        
        def helper(x):
            if x < 0: return 0

            res = 0
            l,cur = 0,0

            for r in range(len(nums)):
                cur += nums[r] % 2
                while cur > x:
                    cur -= nums[l] % 2
                    l += 1
                
                res += (r-l+1)
            return res
        return helper(k) - helper(k-1)

 713. Subarray Product Less Than K
Solved
Medium
Topics
Companies
Hint
Given an array of integers nums and an integer k, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than k.

 

Example 1:

Input: nums = [10,5,2,6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
Example 2:

Input: nums = [1,2,3], k = 0
Output: 0

 SOLUTION : 

 class Solution(object):
    def numSubarrayProductLessThanK(self, nums, k):
        if k <= 1: return 0  # Special case

        prod = 1
        res = 0
        l = 0

        for r in range(len(nums)):
            prod *= nums[r]
            while prod >= k:
                prod //= nums[l]
                l += 1
            res += (r - l + 1)
        return res

        

        
        
