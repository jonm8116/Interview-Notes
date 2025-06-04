# Neetcode DSA course

## Static Arrays

26. Remove Duplicates from Sorted Array

- <strong>Strategy: Two pointers</strong>
- <strong>Time complexity: O(n)</strong>
- Use one pointer (rightPtr) to check for duplicates in order to check for
  duplicates (compare against the current index and previous index)
- Use second pointer (leftPtr) to assign non duplicate values to the
  same array


```
[1,2,3]

def removeDuplicates(self, nums: List[int]) -> int:
    rightPtr    = 1
    leftPtr     = 1
    
    while(rightPtr < len(nums)):
        if(nums[rightPtr] != nums[rightPtr - 1]):
            nums[leftPtr] = nums[rightPtr]
            leftPtr += 1
        rightPtr += 1
    
    return leftPtr

```

27. Remove Element

- <strong>Strategy: Two pointers</strong>
- <strong>Time complexity: O(n)</strong>
- Following a similar strategy to #26

```
def removeElement(self, nums: List[int], val: int) -> int:
    k = 0
    lenNums = len(nums)

    for curIndex in range(0, lenNums):
        if(nums[curIndex] != val):
            nums[k] = nums[curIndex]
            k += 1

    return k
```

## Dynamic Arrays

1929. Concatenation of Array

- <strong>Strategy: Linear Scan?</strong>
- <strong>Time complexity: O(n)</strong>
- Create list of size 2n where n = length of given list
- Have an index into the original list and store the values at the same index
  in the new list and at an offset of the index + size of the original list

```
def getConcatenation(self, nums: List[int], val: int) -> List[int]:
    len2NumArr = len(nums) * 2
    lenNums = len(nums)
    retArr = [0] * len2NumArr
    list1Counter = 0

    for i in range(0, lenNums):
        retArr[i] = nums[list1Counter]
        retArr[i+lenNums] = nums[list1Counter]
        list1Counter += 1
    return retArr

```

## Stacks

20. Valid Parentheses

- <strong>Strategy: Stacks</strong>
- <strong>Time complexity: O(n)</strong>
- Use a stack (use a list to sim stackk) to push opening (left) parentheses on to the stack
- Pop an item off the stack whenever a closing (right) parentheses is
  found in the string and the top of the stack contains the matching opening
parentheses
- If stack is empty after iterating over the whole string then the string
  contains valid parentheses

```
def isValid(self, s:str) -> bool:
    stack = []
    for i in range(0, len(s)):
        if(len(stack) > 0):
            if (    (stack[-1] == '(' and s[i] == ')') or
                    (stack[-1] == '{' and s[i] == '}') or
                    (stack[-1] == '[' and s[i] == ']')):
                stack.pop()
            else:
                stack.append(s[i])
        else:
            stack.append(s[i])
    
    return len(stack) == 0

```

155. Min Stack

- <strong>Strategy: Stacks</strong>
- <strong>Time Complexity: N/A class design</strong>
- To maintain the min stack we want to keep track of the minimum at each
  level of the stack
- so instead of pushing just the value on to the stack we push a dictionary of
  both the current val and the minimum at that time
- we also need to readjust the minimum whenever we pop

```
class MinStack:

    def __init__(self):
        self.stack = []
        self.curMin = 0

    def push(self, val: int) -> None:
        # if first item set cur min
        if(len(self.stack) == 0):
            self.curMin = val
        else:
            if(val < self.curMin):
                self.curMin = val
        item = {'val': val, 'curMin': self.curMin}
        self.stack.append(item)

    def pop(self) -> None:
        ret = self.stack.pop()
        if(len(self.stack) > 0):
            self.curMin = self.stack[-1]['curMin']
        return ret['val']

    def top(self) -> int:
        return self.stack[-1]['val']

    def getMin(self) -> int:
        return self.stack[-1]['curMin']
```

## Singly Linked Lists

206. Reverse a linked list

- <strong>Strategy: recursion with two pointers</strong>


```
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    return self.reverseListHelper(None, head)

def reverseListHelper(self, prev: Optional[ListNode], current: Optional[ListNode]):
    # iterate to end the of the list
    # we return the prev ptr here because cur ptr will be pointing to null
    # at the end of the list
    if(current == None):
        return prev
    else:
        tmpNext = current.next  # set tmp ref to the next part of list
        current.next = prev     # this is where the reversal will happen but you will lose ref to iterate thru list that's why you keep the tmp ref

        # in the recursive call we will use current as prev
        # and the tmp next ref will be used as next current
        return self.reverseListHelper(current, tmpNext)


```

## Trees

94. Binary Tree Inorder Traversal

- <strong>strategy: Inorder Traversal</strong>
- Need to perform an inorder traversal and pass in an additional list to add the current node to during the traversal
- easy way to remember traversals
    - preorder: root, left, right
    - inorder: left, root, right
    - postorder: left, right, root

```
def inOrderTraversal(self, root: Optional[TreeNode]) -> List[int]:

    retList = []
    self.inOrderTraversalHelper(root, retList)
    return retList

def inOrderTraversalHelper(self, root: Optional[TreeNode], retList: List[TreeNode]) -> List[int]:
    if(root == None):
        return
    if(root.left):
        self.inOrderTraversal(root.left, retList)
    retList.append(root.val)
    if(root.right):
        self.inOrderTraversalHelper(root.right, retList)

```

102. Binary Tree Level Order Traversal

- <strong>strategy: BFS</strong>
- a BFS (at least for trees) requires two queues
- a main queue and temporary queue
- you will enqueue the current level's children into the temp queue and then copy that over to the main queue to start the next level

```
def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
    if(root == None):
        return []

    levels = [[root.val]]
    mainQueue = [root]
    tempQueue = []

    while(len(mainQueue) != 0):
        item = mainQueue.pop(0)
        if(item.left != None):
            tempQueue.append(item.left)
        if(item.right != None):
            tempQueue.append(item.right)

        if(len(mainQueue) == 0):
            if(len(tempQueue) > 0):
                levels.append([n.val for n in tempQueue])
                mainQueue = tempQueue
                tempQueue = []

    return levels
```

199. Binary Tree Right Side View

- <strong>strategy: BFS</strong>
- use BFS but in each level just add the last element
- this equates to the right most element at that level (depending how you traverse the tree)

```
def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
    if(root == None):
        return []

    rightSide = [root.val]
    mainQueue = [root]
    tempQueue = []

    while(len(mainQueue) != 0):
        item = mainQueue.pop(0)
        if(item.left != None):
            tempQueue.append(item.left)
        if(item.right != None):
            tempQueue.append(item.right)
        if( len(mainQueue) == 0 and
            len(tempQueue) > 0):
            rightSide.append(tempQueue[-1].val)
            mainQueue = tempQueue
            tempQueue

    return rightSide
```
