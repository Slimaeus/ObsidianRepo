# 1️⃣What is Two pointers?
With the Two Pointer technique, we use two pointers to traverse a list/array/string and perform search operations within a loop on the data structure. It consists of two variants:

1. Opposite-Directional: Each pointer is placed at opposite ends of the array, and they move towards each other until they meet or satisfy a certain condition.
2. Equi-Directional: Each pointer starts at the beginning of the array. One pointer moves slower while the other pointer moves faster, both in the same direction, until they meet a certain specified condition.
# 2️⃣Why use the Two Pointer technique?

The most important reason for using this technique is to reduce the time complexity of a problem from O(n^3) or O(n^2) to O(n) or O(nlogn), depending on whether the array is sorted or not.

# 3️⃣How to use the Two Pointer technique?

Let's understand this technique by looking at the following example:

Problem: Given an array of integers, "numbers," sorted in ascending order, find two numbers such that their sum is equal to a target number. The result should be an array that stores the positions of these two numbers.

Conditions: 1 <= answer[0] < answer[1] <= number.length.

Example:

Input: numbers = [2,7,11,15], target = 9

Output: [1,2]

Explanation: Since 2 + 7 = 9, and 2 is at position 1 while 7 is at position 2, the result is [1,2].

In this problem, we are given a sorted array and a target number. We need to iterate through the array and determine the positions of two numbers that add up to the given number, and then return the positions of those numbers. Now, let's talk about the possible approaches that can be used to solve this problem:

Brute Force with Time Complexity: O(n^2)

Two Pointer with Time Complexity: O(n)