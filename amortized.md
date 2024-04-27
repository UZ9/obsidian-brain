## Problem
- We have some operation that is almost always a certain time complexity, e.g. $O(1)$. However, there is a special edge case, e.g. resizing, where it suddenly becomes $O(n)$. How do we represent this without saying $O(n$) always?

## Solution
- The time complexity of an algorithm over time (i.e. not considering that one specific edge case) is considered the **amortized** time complexity. For example, an [[ArrayList]] has an average add to back operation of $O(1)$, but in the special case it has to resize this becomes $O(n)$. Therefore, the time complexity is $O(1)$ amortized.