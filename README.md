There are 4 files taken from https://patentsview.org/download/data-download-tables
Tried to use the API but the documentation on the website () is quite bad and I kept being denied permission even with the API key.
https://patentsview.org/apis/purpose
https://search.patentsview.org/swagger-ui/

The files include:
- General patent information
- 2014 image description text
- 2014 claims
- 2014 brief summary

Some things you may need to install:
- numpy
- pandas
- re
- tensorflow
- tensorflow_hub
- clip
- requests
- nltk
- sklearn

Code setup:
the first chunk of the code is handling the data given and combining 3 files into one table and having a separate table for the drawing descriptions. The tables were filtered so that only common patents between the four files are used

The second part under "Image Description Model" implements the CLIP model where it is fed the image description text as a basis and then an image is taken from "data" folder. Originally tried to have the user upload the image themselves so it could be easily changed each time, but had troubles with a tuple. A similarity is calculated, but it is quite bad right now. The text image "flowchart" is an image directly from a patent, but the model does not fit it with the proper description right now since the CLIP model isn't trained on sketches and diagrams. The image text is also too long right now for CLIP and is being truncated which could cause problems.

The last part under "NLP Model" takes in the user's description of their product, and computes the cosine similarity to the existing claims. It then returns information on the patent and the similarity percentage of the top 10 patents in order. Only the first 1000 claims are used since the dataset is soooo large.

TODO:
- add biases for image vs text similarity
- user interface
- scaling to handle the data (word2vec or doc2vec?)
- fix truncated CLIP image description text
- determine threshold for what constitutes "infringement" 
