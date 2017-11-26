# Leetcode Problem Sheet

## 1. Two Sum

1. O(N^2) is easy
2. O(N) use hash. The map in C++ is quite convenient. 

## 2. Add Two Numbers

O(N) approach. High precision addition method.

Faults:

1. **[WA]** Ingored the carry from the largest bit.
2. **[WA]** `len1(1)` the wrong initialization.

## 3. Longest Substring Without Repeating Characters

O(N) approach, should be the best. Use one array prev[char] to record the latest appeared position of each character. Use one var to record the started position of the current string. Move this var to the new character if such char has appeared in this string.

Faults:

1. **[RE]** The characters are in ASCII range, not only letters.
2. **[RE]** The same as above.

## 4. Median of Two Sorted Arrays  

O(log(2N)) approach. This question is quite complicated. Firstly use dichotomy on one set, enumerate one integer. Secondly use dichotomy on the other set to see how many integers are there larger or smaller than it.

Faults:

1. If the median is not an integer?
2. Or if it is an integer but never appeared in the sets?
3. What if empty array appears in the processing


## 5. Longest Palindromic Substring

O(N^2) approach. Emunerate the middle position of the substring. Notice than the substring's length could be even or odd.

## 6. ZigZag Conversion

Two approaches:

1. Give each letter one serial number. Print them according to the number. Which is time consuming.
2. Find which letter to be printed next. Which will be much faster.

## 7. Reverse Integer

Tips:

1. Leetcode uses windows environment. `long long` could be used here to make this problem easier.
2. `INT_MIN` and `INT_MAX` could be used to indicate the range of int.

Faults:

1. **[WA]** Forgot to initialize the var in class


## 8. String to Integer (atoi)

Things to be noticed:

1. If it is an empty string 
2. The first non-whitespace character
3. If the string only contains whitespace
4. An optional plus or minus sign
5. Stop if invalid character appears
6. Out of range

Faults:

1. **[WA]** Even `long long` is not enough to store this number, so out of range problem should be processed during the transferring.
2. **[CE]** When you check whether the result is smaller than `INT_MIN`, `result > INT_MAX + 1` should be used. But the `INT_MAX + 1` here will exceed integer range, so use `result - 1 > INT_MAX` instead.

## 9. Palindrome Number

Noticed that the problem regards that a negative number could not be palindrome.

## 10. Regular Expression Matching

Try to transfer string p into a more standard form. Then use DP to solve this problem. The "*" condition maybe a little tricky.

Faults:

1. **[WA]** Forget to set bool var to `false` out of the `if` sentences.

## 11. Container With Most Water

My first thought was a O(Nlog(N)) approach. Maintain a increasing sequence, both forward and backward. When we try to find the answer for one bar, use binary search to find the minimum one larger than it. So is backwardly.

The best answer is the O(N) approach. Starting from the two ends, move the two ends to the middle until a new minimum height is reached.

## 12. Integer to Roman

Simple question.

## 13. Roman to Integer

First split the string into four parts. Then use multiple `if` sentence to translate them. What a pity `switch()` could not be used here.

## 14. Longest Common Prefix

Mine is O(NMlog(M)) approach. Select the shortest as the standard, and use dichotomy to enumerate the length of common prefix. Check if such a prefix is right.

## 15. 3Sum

This problem is quite complicated. My first thought was a O(N * N) approach with hash map. But it seems that the negative number couldn't be processed properly. Also, the time is not guranteed.

Then I found another approach. Sort the array, enumerate one number, and use the increasing property to find the other two. 

I try to enumerate the middle one at first, but duplicates could not be avoided. So it is better to enumerate the first one of the triplet.

Faults:

1. **[RE]** when you use "minus" after a `vector.size()`, if the vector is empty, the minus opteration will cause overflow, because the return value of `vector.size()` is unsigned type.

## 16. 3Sum Closet

This question is even simpler than the previous one. Only some little modifications are need here, like duplicates avoiding is uncessary.

Faults:

1. **[TLE]** Ignored the condition that the `tmp` just equalts to the `target`.

## 17. Letter Combiantions of a Phone Number

Build an alphabet and use DFS.


## 18. 4Sum

The same as "3Sum", but instead of enumerate only the begininng of quadruplets, enumerate the beginning and ending at the same time. When you enumerate, be sure that the ending is coming backwards. Otherwise, when you processing the duplicates, some conditions will be neglected.

Faults:

1. **[WA]** Enumerate the ending forwards.

## 19. Remove Nth Node From End of List

Simple to solve, but hard to do it in one pass.

Faults:

1. **[WA]** Think about if you have multiple elements in this link list but you want to delete the first one.

## 20. Valid Parentheses

Stack. Mind `"["` and `"]"` these two conditions.

## 21. Merge Two Sorted List

Just like merge sort, use two pointer.

## 22. Generate Parentheses

Enumerate all the conditions, at the same time, check if it is illegal.

How to check whether it is illegal? I make a silly here to use a stack. You just make sure that left brackets you have here are more than right backets.

## 23. Generate Parentheses

Easy to pass, but learn a lot. Solve with the assistance of priority queue. Learnt the construction function of struct and the override of priority queue's compare function.

    struct Node {
      int val;
      int from;
      Node(int x, int y) : val(x), from(y) {}
    };
    
    struct NodeCmp{
        bool operator()(const Node &a, const Node &b){
            return a.val > b.val;
        }
    };

**[Warning]** The first element poped out should be the last element sorted by your compare function.

## 24. Swap Nodes in Pairs

The same as #25;

## 25. Reverse Nodes in k-Group

Use a vector to record every k elements. Be careful when k equals 1.

## 26. Remove Duplicates from Sorted Array

Just as the title says.

## 27. Remove Element

Naive.

## 28. Implement strStr()

KMP.

## 29. Divede Two Integers

This is quite a good question! You will learn bit manipulation and run into lots of traps.

    const long long one = 1;
    long long c, k, result = 0;
    while (divid >= divis) {
        bool finished = false;
        for (c = divis, k = 0; divid >= c; c <<= 1, k ++) {
            if (divid - c < divis) {
                result = result + (one << k);
                finished = true;
                break;
            }
        }
        if (finished) break;
        divid -= c >> 1;
        result += 1 << (k - 1);
    }

Faults:

1. **[1-2 WA]** The numbers could also be negative. Use a `bool` type sign to solve.
2. **[3-4 WA]** Mind the overflow. Even though every input is `int` type, `-2147483648 / -1` may have a result out of range.
3. **[5-6 WA]** Even though the result is in `int` range, the variables during processing will have value out of range. `long long` will be need here.
4. **[7 WA]** `1 << k` will also causes overflow. Use:

        const long long one = 1;

## 30. Substring with Concatenation of All Words
Learned a special for sentence and the usage of unordered_map.

	for (string word : words)
		counts[word] ++;

	if (counts.find(word) != counts.end()) {
		xxxx
	} else break;

Faults:

1. **[RE]** What if there is no solution? (The length of s is not enough.)

## 31. Next Permutation

Scan elements one-by-one backwards. Stop until at some position, the element before it (a) is larger than itself (b). Then, find the minimum scaned number larger than a. Swap there position, and sort all the elements that have been scaned.

Find the minimum larger one and sort could be implemented in O(log(N)) and O(N), but O(N) and O(log(N)) approached are much easier to write: `sort()`.

Faults:

1. **[WA]** Recalled a wrong algorithm but didn't challenge it. Swaped a and b instead.

## 32. Longest Valid Parentheses

There are several solutions for this problem (A and B stands for two valid parentheses):

1. O(N^3) `bool f[i,j]` means whether i~j is valid or not. A valid parentheses can be built from `(A)` or `AB`. Another O(N) is need to enumerate `AB` condition. (Actually meaningless.)
2. O(N^2) Enumerate the beginning or ending of the parentheses, use one stack to check how long the valid parentheses could be.
3. O(N) `int f[i]` stands for the length of the longest parentheses take s[i] as ending. That could be built in following two forms: `A(B)` and `A()`.

Faults:

1. **[TLE]** Only come up with the O(N^3) approach.
2. **[WA]** Only think of the `(B)` condition but not the `A(B)` one.
3. **[WA]** No initialization for the variable `int tmp`.

## 33. Search in Rotated Sorted Array

1. O(N) scan.
2. O(log(N)) Firstly use one binary search to locate the break point. Then binary the target in left half or right half.

Faults:

1. **[1-2 WA]** When there are only two elements, and the binary stops at the second element, you don't know whether this means there is a break point or not. So the best solution here would be push another `INT_MIN` into the vector. When there is no break point at all, the pointer will stop at `INT_MIN`.

## 34. Search for a Range

Use one binary for the starting of the range, and another for the ending.

## 35. Search Insert Position

Binary search.

## 36. Valid Sudoku

Use arrays to check duplicates.

Faults:

1. **[WA]** Forget the cpp initializing.
2. **[WA]** Translate rows and columns into boxes.
3. **[WA]** Not clear about the input format.

## 37. Sudoku Solver

DFS.

## 38. Count and Say

Simulation.

## 39. Combination Sum

DFS.

Sort the candidates so that you can stop the search if there is no solutions for the smaller ones.

## 40. Combination Sum II

Comparing to the question above, there are duplicates in the candidates but no duplicates in the results.

So you should enumerate how many pieces of one element are selected.

## 41. First Missing Positive

Swap every element to its supposed position, and then the first missed placed number is the answer.

Mind that the swap may mess up the array, so research the array until there is no change any more.

Faults:

1. **[WA]** There are duplicates in the input!

## 42. Trapping Rain Water

For each bar, find the highest bar on its left side and right side, then you know how much water you could store at this position. Add them up and you will get the answer.


## 43. Multiply Strings

High precision multiply.

Faults:

1. **[WA]** The result may be zero.

## 44. Wildcard Matching

Dynamic programming program.

Three conditions for matching process:

1. Two letters.
2. One question mark.
3. One star mark.

Match one string with empty string at first.

You can add one sign at the first of each string to facilitate the processing.

## 45. Jump Game II

Lemma: If you jump to Position A with a least n steps, then you must jump to positions after A within steps no less than n.

Thus we use a queue to store the farthest we can reach within the steps. We pop out the front element if we went out of that range. We push one new element in if it has a farther range than the end.

## 46. Permutations

Start from the end, find the first continous A and B such that A < B. Then find the smallest number after A
 but larger than A. Swap their position. Reverse the whole sequence start from B.

Repeat this process until no A and B
 could be found.

## 47. Permutations II

Same as above.

## 48. Rotate Image

First reverse the matrix up to down, then swap the symmetry.

## 49. Group Anagrams

Use unordered_map and multiset:

     unordered_map<string, multiset<string>> um;

Better way to write a for sentence:

    for (auto m : um) {}

A new way to construct vector:

    vector<string> anagram(m.second.begin(), m.second.end());

## 50. Pow(x, n)

Fast Exponentiation Method.


Faults:

1. **[TLE]** Store values to reduce the times to reference functions.

## 51. N-Queens

DFS + bitwise operations.

## 52. N-Queens II

Same as above.

Faults:

1. **[WA]** Forget the initialization.

## 53. Maximum Subarray

Maintain a sum array.


Faults:

1. **[WA]** The first number may be negative.

## 54. Spiral Matrix

For Sentences.


Faults:

1. **[WA]** The input is a matrix, not square.
2. **[RE]** The input maybe empty.

## 55. Jump Game

The same as `#45 Jump Game II`

## 56. Merge Intervals

Use a sort and go through them.


Faults:

1. **[WA]** The input maybe empty.

## 57. Insert Interval

The same as above.

## 58. Length of Last Word

The true problem here is complicated cases.


Faults:

1. **[WA]** "a ".

## 59. Spiral Matrix II

The same as #54.

## 60. Permutation Sequence

The same as #46 & #47.

## 61. Rotate List

Linked list Manipulation.

Faults:

1. **[WA]** k may be non-zero even though the list is empty.

## 62. Unique Paths

The easiest dp.

## 63. Unique Paths II

The same as #62.

## 64. Minimum Path Sum

The same as #63.

## 65.

## 66. Plus One

High precision addition with only one special conditon that all the digits are "9".

Test programming in Java. Learned how to define one array in Java.

## 67. Add Binary

Binary version high precision addition.

Learned a lot about Java string operation.

    class Solution {
        public String addBinary(String a, String b) {
            // StringBuilder
            StringBuilder sb = new StringBuilder();
            int i = a.length() - 1, j = b.length() - 1, carry = 0;
            while (i > -1 || j > -1) {
                int sum = carry;
                // String.charAt(pos) function
                if (i > -1) sum += a.charAt(i --) - '0';
                if (j > -1) sum += b.charAt(j --) - '0';
                // append(int i)
                // Appends the string representation of the int argument to this sequence.
                // float, boolean are the same.
                sb.append(sum % 2);
                carry = sum / 2;
            }
            // int in java could not be trated like boolean
            if (carry != 0) sb.append(carry);
            // StringBuilder.reverse() StringBuilder.toString()
            return sb.reverse().toString();
        }
    }

## 68.

## 69. Sqrt(x)

Good problem!

Use eps and binary search. The output could be tricky.

Faults:
1. **[TLE]** Not clear about the output. Actually you could just use floor() here and then try whether (result + 1) also possible.
2. **[TLE]** Same as above.
3. **[WA]** Same as above.
4. **[TLE]** Not clear about the precision of float(6) and double(15). Double should be used here.
5. **[WA]** When try (result + 1), its sqr maybe out of integer. You should convert type at this step.

## 70. Climbing Stairs

One simple dp problem.

Stair N could be reached from (N - 1) or (N - 2), so the transfer equation is :

    f[i] = f[i - 1] + f[i - 2];

## 71.

## 72.

## 73.

## 74.

## 75.

## 76.

## 77.

## 78.

## 79.

## 80.

## 81.

## 82.

## 83. Remove Duplicates from Sorted List

Use one pointer to record the last distinct node. Update it until you find a distinct one.

## 84.

## 85.

## 86.

## 87.

## 88. Merge Sorted Array

Merge sort. As long as the space is prepared for you in array 1, you could just merge 2 into 1. In order to avoid conflicts, the operations should be done backwards.

## 89.

## 90.

## 91.

## 92.

## 93. 

## 94.

## 95.

## 96.

## 97.

## 98.

## 99.

## 100. Same Tree

DFS.

Faults:

1. **[WA]** The input maybe `null`. "Given two binary trees ..." so `null` is also a binary tree ???
2. **[RE]** Same as above.

## 101. Symmetric Tree

1. Recursive solution: Build another function `mirror(l, r)` to test whether TreeNode l and r and symmetric, and do this recursively.

2. Iterative solution: Put the inorder traversal in a List or a stack, check if this list/stack is palindrome.

## 101.

## 102.

## 103.

## 104. Maximum Depth of Binary Tree

DFS.


## 105.

## 106.

## 107. Binary Tree Level Order Traversal II

DFS.

Learned how to new 2-dimensional array in Java.

## 108. 