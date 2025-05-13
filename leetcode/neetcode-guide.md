# Neetcode DSA course

## Static Arrays

26. Remove Duplicates from Sorted Array

- <strong>Strategy: Two pointers</strong>
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
