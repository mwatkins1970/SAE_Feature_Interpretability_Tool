# Gemma-2B SAE feature interpretability multitool
A tool to assist in the interpretation of learned features in sparse autoencoders (in particular the four SAE's trained by Joseph Bloom on Gemma-2B).

## Overview
This tool two main functions. For both, given a choice of SAE feature, a "feature vector" is constructed from either its encoder or decoder weights (also the user's choice), and this is then used to either

* produce "definition trees" for "ghost tokens" based on the feature vector
* produce lists of tokens whose embeddings are close to the feature vector (in a very specific sense)

### Functionality 1: Definition trees

choose various parameters
cumulative probability cutoff
top-5 logits
trimming tree 
(could add functionality to export tree structure (JSON dictionary) or visualisation (PNG image)

token centroid offset seems crucial to get anything to work (but is included as optional)


### Functionality 2: Token lists

controls include an exponent which controls tradeoff between closeness-to-feature-vector and farness-from-centroid

token centroid offset seems crucial to get anything to work (but is included as optional)

General:
While focussing on Gemma-2B and JB's SAE, could be easily adapted to other SAEs trained on other models.
Could be extended to include linear combinations of multiple PCA components (not just scalings of the first)
Linear combination of encoder- and decoder-based feature vectors
Use of steering vectors to enhance the effect?


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
3. Launch the notebook and explore Gemma-2B SAE features

### Usage
- Open the `notebooks/SAE_Interpretability_Research.ipynb` file in Colab or Jupyter.
- Follow the instructions in the notebook to load the model, modify feature layers, and generate definition trees.

### Contributions
Contributions are welcome. Please open an issue or submit a pull request.

### License
This project is licensed under the GNU General Public License v3.0 - see the LICENSE file for details.
