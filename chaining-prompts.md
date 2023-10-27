# Chaining Prompt
Accomplish a task by breaking it into multiple smaller prompts and passing the output of one prompt as the input to the next

## Why Chaining Prompt ?
- Reduce the number of tokens in a prompt
- Skip some chains of the workflow when not needed for the task
- For complex tasks, keep track of state
- Use external tools like databases, internet, and/or calling an API

## Sequential Chains
Sequential chains is another type of chains. The idea is to combine multiple chains where the output of the one chain is the input of the next chain.

### There is two types of sequential chains
- Simple sequential Chain: Single input/output
- Sequential Chain: multiuple input/output

### Router chain
- if/else chain
- Ex. if the input is related to (1, 2, 3) then go to chain1, else go to default chain 
