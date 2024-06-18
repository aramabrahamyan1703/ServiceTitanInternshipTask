# Overview

First of all we need to extract the text from the PDF file, and then store it in a vector database as embedded vectors.
Afterwards, when the user will input their prompt the matching chunks will be directed to the LLM and the response will be generated.

# 1.PDF Processor

First, we need to extract text from our PDF file. The best choice would be to use Python's PyMuPDF library


### Pros: 
Fast and easy to implement.\
No big errors.

### Cons:
The text on the images will not be extracted, which is a big con but not for this specific project, as we almost do not have such cases.

# 2.Embedder

Choosing an embedder may be a hard problem. A good idea will be to choose a dense embedder to capture the context. We can use a pre-trained model, say, Google’s BERT.


### Pros:
Capturing context and not hallucinating on synonyms.

### Cons:
Complex to implement and requires large storage

# 3.Vector DataBase

For this step, we need to choose a database to store our embedded vectors. There are many such databases, but I think Qdrant is an optimal solution.


### Pros:
Opensource\ 
Many features\

### Cons:
As it is relatively new, there may be some bugs and week documentation

# 4.Retrival Mechanism

We can use Qdrant with a Cosine Similarity Search algorithm for Retrival Mechanism, meaning finding the matching part of our user manual.

        
### Pros:
Easy to implement\
Efficient Retrival

### Cons:
Cons of Qdrant
        

# 5.LLM response

For LLM Response Generation, we can take, say, OpenAI’s API.


### Pros:
Good response generation

Cons:
Not free\
Reliance on external parties

# Challenges:

1.Using BERT embedding we will have high dimensionality(768); however we can use PCA(Principal Component Analysis) to reduce the dimensions without affecting the context.
2.Using PyMuPDF we will not get text on the images; however we can use Pytesseract can be used to overcome this challenge.
3.LLM response generation with OpenAI's API will be financially hard to implement, as an alternative we can use on of many models from Hugging Face.

## Examples of complex questions that the chatbot will be able to answer:

1."Where to install the Indoor Unit?"\
2."How to remove the front panel?"\
3."Give hints on wiring"\
4."Can we use taped wires?"\
5."Can the conditioner be installed near gas leak?"

This all information is present in our database, that is why the chatbot will be able to find answers.

## Examples of questions that the chatbot will fail to answer.

1."Why my conditioner is not working now?"\
2."Tell the history of this company."\
3."Which brand is better, yours or others?"\
4."What is wrong with my conditioner, identify the issues from photo."\
5."Are there any legal regulations on installing conditioners in my area?"

The questions are real-time, too specific, or too subjective require photo analysis that is why our model will not be able to answer them. 



