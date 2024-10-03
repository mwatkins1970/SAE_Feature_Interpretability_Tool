# SAE_Feature_Interpretability_Tool
A tool to assist in the interpretation of learned features in sparse autoencoders (in particular the four SAE's trained by Joseph Bloom on Gemma-2B).

This has two main functions. In both cases, for a given SAE feature, a "feature vector" is constructed from either its encoder or decoder weights (the user's choice), and this is then used to either

* produce "definition trees" for "ghost tokens" based on the feature vector
* produce lists of tokens whose embeddings are close to the feature vector (in a very specific sense)

Functionality 1: Definition trees

blah blah

Functionality 2: Token lists

rhubarb rhubarb
