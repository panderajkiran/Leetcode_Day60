# Leetcode_Day60
# Day 60 — Longest Substring Without Repeating Characters

**LeetCode Problem:** 3. Longest Substring Without Repeating Characters  
**Difficulty:** Medium  
**Language:** Java  
**Topic:** Sliding Window, Hashing / Frequency Array

---

## Problem

Given a string `s`, find the length of the longest substring that contains no repeated characters.

### Example

```text
Input:  s = "abcabcbb"
Output: 3

Explanation:
The longest substring without repeating characters is "abc".
Its length is 3.
Approach

I used the Sliding Window technique with a frequency array.

How it works:
Use two pointers:
left → start of the current window
right → end of the current window
Move right through the string one character at a time.
Store the frequency of each character in an array.
If the current character appears more than once, move left forward and decrease the frequency of the characters being removed.
Once the window contains unique characters again, calculate its length.
Keep updating the maximum length found.
Example

For:

s = "abcabcbb"

The window expands:

a → ab → abc

When another a appears, we shrink the window from the left until a is no longer repeated.

This allows us to maintain a valid substring without repeatedly checking the entire string.

Code
class Solution {
    public int lengthOfLongestSubstring(String s) {

        int[] count = new int[128];
        int left = 0;
        int max = 0;

        for (int right = 0; right < s.length(); right++) {

            count[s.charAt(right)]++;

            while (count[s.charAt(right)] > 1) {
                count[s.charAt(left)]--;
                left++;
            }

            max = Math.max(max, right - left + 1);
        }

        return max;
    }
}
Complexity
Time Complexity

O(n)

Each character is processed at most a few times as the two pointers move forward.

Space Complexity

O(1)

The frequency array has a fixed size of 128 characters.

What I Learned

Today I learned how powerful the Sliding Window technique can be for substring problems.

Instead of starting over whenever I find a duplicate, I can simply adjust the left side of the window and continue.

The important idea is:

Don't throw away the whole solution when a small part becomes invalid. Adjust only what needs to change.

Key Takeaway

Sliding Window is useful when we need to find the longest, shortest, or valid continuous portion of an array or string while maintaining some condition.
