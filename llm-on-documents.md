# LLMs on documents
We want to use an LLm and combine it with our documents, but LLMs can only inspect a few thousends of words at aq time. This is where embeddings and vector stores come into play.

## First, Embeddings
- Numerical representation of pieces of text, this numeric representation captures the semantic meaning of the piece of text
- Text with simillar content will have simillar vectors

## Second, Vector Database
- A vector database is a way to store these vector representations that we created in the previous step
- We pupulate it with chunks of text, comming from incomming documants
- When we get a big incomming document, we first going to break it into chunks, which is useful, because we may not be able to pass the whole document to the model
  -   if the document small, then you don't need to create any chunk 
- Then we create an embidding for each of these chunks, then we store those vectors in a vector database

## Third, Scenario
- When a query comes in, we first create an embidding for it
- Compare it to all the vectors in the vector database, and then we pick the most N simillar vectors
- Then pass all those vectors to the language model to get the final answer
