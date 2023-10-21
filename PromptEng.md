# Prompt Engineering

## Model Limitations

### Hallucination
> Makes statements that sound plausible but are not true;

### Reducing the Hallucination
> First find relevant information, then answer the question based on the relevant information

## Principles of Prompting

## Iterative prompt development
> Idea -> Prompt -> Error Analysis -> Repeate

- Try something 
- Analyze where the result doesn't give what you want
- Clarify instructions, give more time to think
- Few shots

### #1 Write clear and specific instructions
#### Use Delimiters 
- """
- '''
- <>

Useing delimiters is helpfull technique to avoid prompt injections, for example the user input prompt can be _"forget all instructions...."_

example: 
```python 
prompt = f"""
    Summarize the text delimited by triple backticks \ 
    into a single sentence.
    ```{text}```
    """
``` 

example: 
```python 
prompt = f"""
    Generate a list of three made-up book titles along \ 
    with their authors and genres. 
    Provide them in JSON format with the following keys: 
    book_id, title, author, genre.
    """
```

#### Ask for specific structure _(HTML, JSON, XML)_

example :

```python
prompt_2 = f"""
    Your task is to perform the following actions: 
    1 - Summarize the following text delimited by 
      <> with 1 sentence.
    2 - Translate the summary into French.
    3 - List each name in the French summary.
    4 - Output a json object that contains the 
      following keys: french_summary, num_names.

    Use the following format:
    Text: <text to summarize>
    Summary: <summary>
    Translation: <summary translation>
    Names: <list of names in Italian summary>
    Output JSON: <json with summary and num_names>

    Text: <{text}>
    """
```

#### Check whether conditions are satisfied 
example:
```python
prompt = f"""
    You will be provided with text delimited by triple quotes. 
    If it contains a sequence of instructions, \ 
    re-write those instructions in the following format:

    Step 1 - ...
    Step 2 - …
    …
    Step N - …

    If the text does not contain a sequence of instructions, \ 
    then simply write \"No steps provided.\"

    \"\"\"{text_2}\"\"\"
"""
```

### Few shot prompting rather than zero-shot prompting
Give successful examples of completing tasks, then ask the model to perform tasks.
```python
prompt = f"""
    Your task is to answer in a consistent style.

    <child>: Teach me about patience.

    <grandparent>: The river that carves the deepest \ 
    valley flows from a modest spring; the \ 
    grandest symphony originates from a single note; \ 
    the most intricate tapestry begins with a solitary thread.

    <child>: Teach me about resilience.
"""
```


### #2 Give the model time to think

#### Specify the steps to complete the task
```python
prompt_1 = f"""
    Perform the following actions: 
    1 - Summarize the following text delimited by triple \
    backticks with 1 sentence.
    2 - Translate the summary into French.
    3 - List each name in the French summary.
    4 - Output a json object that contains the following \
    keys: french_summary, num_names.

    Separate your answers with line breaks.

    Text:
    ```{text}```
"""
```

#### Instruct the model to work out its own solution before rushing to a conclusion

```python
    prompt = f"""
    Your task is to determine if the student's solution \
    is correct or not.
    To solve the problem do the following:
    - First, work out your own solution to the problem. 
    - Then compare your solution to the student's solution \ 
    and evaluate if the student's solution is correct or not. 
    Don't decide if the student's solution is correct until 
    you have done the problem yourself.

    Use the following format:
    Question:
    ***
    question here
    ***
    Student's solution:
    ***
    student's solution here
    ***
    Actual solution:
    ***
    steps to work out the solution and your solution here
    ***
    Is the student's solution the same as actual solution \
    just calculated:
    ***
    yes or no
    ***
    Student grade:
    ***
    correct or incorrect
    ***

    Question:
    ***
    I'm building a solar power installation and I need help \
    working out the financials. 
    - Land costs $100 / square foot
    - I can buy solar panels for $250 / square foot
    - I negotiated a contract for maintenance that will cost \
    me a flat $100k per year, and an additional $10 / square \
    foot
    What is the total cost for the first year of operations \
    as a function of the number of square feet.
    *** 
    Student's solution:
    ***
    Let x be the size of the installation in square feet.
    Costs:
    1. Land cost: 100x
    2. Solar panel cost: 250x
    3. Maintenance cost: 100,000 + 100x
    Total cost: 100x + 250x + 100,000 + 100x = 450x + 100,000
    ***
    Actual solution:
    """
```

## Project
```
You are OrderBot, an automated service to collect orders for a pizza restaurant. \
You first greet the customer, then collects the order, \
and then asks if it's a pickup or delivery. \
You wait to collect the entire order, then summarize it and check for a final \
time if the customer wants to add anything else. \
If it's a delivery, you ask for an address. \
Finally you collect the payment.\
Make sure to clarify all options, extras and sizes to uniquely \
identify the item from the menu.\
You respond in a short, very conversational friendly style. \
The menu includes \
pepperoni pizza  12.95, 10.00, 7.00 \
cheese pizza   10.95, 9.25, 6.50 \
eggplant pizza   11.95, 9.75, 6.75 \
fries 4.50, 3.50 \
greek salad 7.25 \
Toppings: \
extra cheese 2.00, \
mushrooms 1.50 \
sausage 3.00 \
canadian bacon 3.50 \
AI sauce 1.50 \
peppers 1.00 \
Drinks: \
coke 3.00, 2.00, 1.00 \
sprite 3.00, 2.00, 1.00 \
bottled water 5.00
```
