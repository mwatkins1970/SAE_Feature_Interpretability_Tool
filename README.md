# SAE_Feature_Interpretability_Tool
A tool to assist in the interpretation of learned features in sparse autoencoders (in particular the four SAE's trained by Joseph Bloom on Gemma-2B).

This has two main functions. In both cases, for a given SAE feature, a "feature vector" is constructed from either its encoder or decoder weights (the user's choice), and this is then used to either

* produce "definition trees" for "ghost tokens" based on the feature vector
* produce lists of tokens whose embeddings are close to the feature vector (in a very specific sense)

Functionality 1: Definition trees

blah blah

Functionality 2: Token lists

rhubarb rhubarb


## Overview
This project provides a visual and interactive exploration of Self-Attention Encoder (SAE) feature spaces using a definition tree generation approach. The tool is built to enhance interpretability in AI systems, specifically focusing on feature exploration—a key concern in AI safety research.

## Key Features
- Interactive feature tree generation for SAE layers
- PCA weighting and scaling factor controls for dynamic exploration
- Visual representation of cumulative probabilities
- HuggingFace integration for language model embeddings

## Getting Started

### Prerequisites
- Python 3.x
- Jupyter Notebook or Google Colab
- HuggingFace access token (see [here](https://huggingface.co/docs/hub/security-tokens) for details)

### Installation
1. Clone this repository:
    ```bash
    git clone https://github.com/your-username/SAE_Feature_Interpretability_Tool.git
    ```
2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3. Launch the notebook and explore the SAE features!

### Usage
- Open the `notebooks/SAE_Interpretability_Research.ipynb` file in Colab or Jupyter.
- Follow the instructions in the notebook to load the model, modify feature layers, and generate definition trees.

### Contributions
Contributions are welcome! Please open an issue or submit a pull request.

### License
This project is licensed under the MIT License - see the LICENSE file for details.
