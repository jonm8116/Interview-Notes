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
