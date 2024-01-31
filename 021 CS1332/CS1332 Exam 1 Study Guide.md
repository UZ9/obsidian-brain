# Big-O Chart

## Lists
|  | ArrayList | Singular Linked List (w/ tail) | Singular Linked List (w/o tail) | Circular Singly Linked List | Doubly Linked List w/ tail  | Doubly Linked List w/o Tail |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| addToFront | $O(n)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ |
| addAtIndex | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ |
| addToBack | $O(1)*$ | $O(1)$ | $O(n)$ | $O(1)$ | $O(1)$ | $O(n)$ |
| removeFromFront | $O(n)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ |
| removeAtIndex | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ |
| removeFromBack | $O(1)$ | $O(n)*$ | $O(n)$ | $O(n)$ | $O(1)$ | $O(n)$ |
| traverseFront | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ | $O(1)$ |
| traverseMiddle | $O(1)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ | $O(n)$ |
| traverseBack | $O(1)$ | $O(1)$ | $O(n)$ | $O(n)$ | $O(1)$ | $O(n)$ |
## Stacks
|  | Singly Linked List Stack | Array Stack |
| ---- | ---- | ---- |
| Push | $O(1)$ | $O(1)*$ |
| Pop | $O(1)$ | $O(1)$ |
| Peek | $O(1)$ | $O(1)$ |
| isEmpty | $O(1)$ | $O(1)$ |
| size | $O(1)$ | $O(1)$ |
| clear | $O(1)$ | Depends |
| resize | $O(1) | $O(n)$ |
## Trees
|  | BST |
| ---- | ---- |
| Average add | $O(\log n)*$ |
| Average remove | $O(\log n)*$ |
| Average access | $O(\log n)*$ |
| Average height | $O(n)$ |
| Average traversal | $O(n)$ |
| Worst case add | $O(n)$ |
| Worse case remove | $O(n)$ |
| Worse case height | $O(n)$ |
| Worst case traversal | $O(n)$ |
## Queues
|  | Singly Linked List Queue | Array Queue |
| ---- | ---- | ---- |
| enqueue | $O(1)$ | $O(1)*$ |
| dequeue | $O(1)$ | $O(1)$ |
| peek | $O(1) | $O(1)$ |

Worst case space complexity for all of these data structures: $O(n)$