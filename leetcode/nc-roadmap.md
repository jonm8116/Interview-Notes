# Neetcode roadmap

## Stacks

150. Evaluate Reverse Polish Notation

- <strong>Strategy: Stacks</strong>
- Use a stack to push numbers on to the stack as iterating through the list of tokens. When encountering an operator then push the top 2 elements of the stack and push result on to the stack. 
- After iterating through the full list of tokens then pop off the result and return as answer

```
def isOperator(self, char: str) -> bool:
    if( char == '+' or
        char == '-' or
        char == '*' or
        char == '/'):
        return True
    else:
        return False

def evalRPN(self, tokens: List[str]) -> int:
    stack = []
    for i in range(0, len(tokens)):
        if(self.isOperator(tokens[i]) == False):
            stack.append(int(tokens[i]))
        else:
            rightNumber = stack.pop(len(stack)-1)
            leftNumber = stack.pop(len(stack)-1)
            result = -1
            if(tokens[i] == '+'):
                result = leftNumber + rightNumber
            elif(tokens[i] == '-'):
                result = leftNumber - rightNumber
            elif(tokens[i] == '*'):
                result = leftNumber * rightNumber
            elif(tokens[i] == '/'):
                result = leftNumber / rightNumber
            stack.append(result)

    return stack.pop(0)

```
