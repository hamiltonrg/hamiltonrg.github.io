# Large Language Models (LLMs)
This is my basic understanding, I may be off here or there.


## Basics how they work

 - Tokenizer
    - Text is seperated into 1 or more tokens by a tokenizer.  There a different ones used by different models.
    -  Example: sandwich becomes 2 tokens, ["sand", "wich"].
    -  URL: https://platform.openai.com/tokenizer
 - Vectorize
   - An pretrained embedding model converts the tokens to a vector.  The embedding model captures the meaning of the word, as part of the training.  
     - See https://vectors.nlpl.eu/explore/embeddings/en/# for a somewhat of an example.
 - Inference
   - After all the text is converted to tokens and then converted to vectors, the vectors are fed into the language model.  
     - How this works depends on how the model is designed, normally called its "architecture".  Different operations are run against varying combinations of vectors and those resulting values progress through "layers" of other calculations until they reach a final layer that calculates the probability of each possible token being the next token.
     - The probabilities of each token are returned to the inference application which then uses various parameters to determine what set of tokens to consider, other parameters and then randomly selecting from the final pruned set.  This is why running the same text through the same LLM multiple times will result in different answers.
 - Loop
   - When text is sent through the above process and the next token is generated, all of that resulting data is fed back through continually until an end of text token is generated or a preconfigured maximum amount of tokens is generated.
 