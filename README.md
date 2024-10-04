[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mwatkins1970/SAE_Feature_Interpretability_Tool/blob/main/notebooks/SAE_feature_interpretability_multitool.ipynb)

# Gemma-2B SAE Feature Interpretability Multitool

This assists in the interpretability of sparse autoencoder (SAE) features, specifically [those trained by Joseph Bloom on the Gemma-2B model](https://huggingface.co/jbloom/Gemma-2b-Residual-Stream-SAEs). By visualising and probing the representations learned by these SAEs, the multitool supports a detailed examination of the kinds of patterns and associations captured by individual learned features within large language models (LLMs). 

## Overview

The tool offers two main functionalities that serve as experimental probes into the model's learned representations:

1. **Definition trees for "ghost tokens"**: This functionality uses feature vectors to generate interpretive "definition trees," revealing complex, hierarchical relationships.
2. **Token lists by embedding similarity**: This functionality generates lists of tokens that exhibit embedding similarities to the selected feature vector, shedding light on the kinds of tokens associated with specific model features.

These can potentially aid in the interpretation of learned features in LLMs.

### Functionality 1: Definition trees

This tool constructs a "definition tree" based on a user-selected SAE feature. Users can control various parameters, including:

- **choice of encoder or decoder weights**: For some features, using encoder weights to construct the feature vector – and thereby the "ghost token" to be defined – produces more useful results; for others, decoder weights work better (it's currently unclear why this is) 
- **token centroid offset (Boolean)**: Optionally offsets the feature vector by the token embedding centroid, which seems necessary to get any useful results (again, it's unclear why)
- **scaling**: The default scaling for the feature vector is 3.8, the approximate mean distance-from-centroid for the token embeddings, which leads to a "ghost token" pointing in a direction determined by the feature weights, but lying at a typical (for tokens) distance from centroid. Lower values (around 2.5) seem to produce better results when decoder weights are used (it's currently unclear why) 
- **PCA adjustments**: A linear combination of the feature vector and the first PCA component for the token embeddings can be used. With a default weighting of 0, this has no effect. For some features, some degree of PCA adjustment is crucial to get useful results.

The result is a tree that hierarchically displays the most probable definitions Gemma-2B would produce for the "ghost token" if prompted at temperature 0. In many cases these are clearly related to the types of text samples that most strongly activate the feature in question. And their branching/"multiversal" structure seems to capture nuances beyond what simple linear descriptions can offer.

### Functionality 2: Token lists

This tool identifies the tokens closest to the feature vector according to a customisable cosine distance metric. Because (due to the quirks of high-dimensional geometry) the tokens whose embeddings are cosine-closest to the token embedding centroid are cosine-closest to _everything_, these are here filtered out by dividing the token embedding's **cosine distance to the feature vector** by its **cosine distance to centroid** (which thereby incentivises the former being small and the latter being large).

Key configurable parameters include:

- **numerator exponent**: Adjusts the filtering metric by raising the numerator (cosine distance to feature vector) by a chosen power.
- **PCA component weighting**: Modifies the feature vector with first PCA direction, as in Functionality 1.
- **Centroid offset and scaling**: The same as in Functionality 1.

In many cases the tokens atop the output lists are clearly related to the types of text samples that most strongly activate the feature in question. 

### Potential automation
If passed to appropriately powerful LLMs via API, these token lists and definition tree data could perhaps facilitate concept-based interpretability studies of learned SAE features.

## Getting Started

### Prerequisites
- Python 3.x
- Jupyter Notebook or Google Colab
- HuggingFace access token (see [here](https://huggingface.co/docs/hub/security-tokens) for details)

### Installation
1. Clone this repository:
    ```bash
    git clone https://github.com/mwatkins1970/SAE_Feature_Interpretability_Tool.git
    ```
2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
3. Launch the notebook and explore Gemma-2B SAE features.

### Usage
- Open the `notebooks/SAE_feature_interpretability_multitool.ipynb` file in Colab or Jupyter.
- Follow the instructions in the notebook to load the model, select features, and generate interpretive visualizations.

## Future directions

There is significant scope for enhancing and extending this project. Possible additions include:

- **Adaptation to other models**: The tool could be easily generalised to work with SAEs trained on other LLMs.
- **Improved control integration**: Merging common controls between functionalities for streamlined interaction.
- **Enhanced base prompt customization**: Allowing customization of the base prompt for the "ghost token" definitions (currently, the base prompt is '''A typical definition of "{ghost token}" would be''').
- **Expanded PCA and linear combination capabilities**: Exploring the impacts of multiple PCA components and linear combinations of encoder- and decoder-based feature vectors.
- **API integration for feature interpretation**: Exporting outputs for further interpretation to LLMs via API, enabling automated analysis.
- **Feature taxonomy and parameter analysis**: Classifying features according to the efficacy of these two tools in capturing the types of text samples they activate on, as well as the typical parameter settings needed to produce relevant effective outputs.

I'm most excited about the following, probably the next thing to be explored:
- **Steering vector and clamping applications**: Leveraging feature vectors as "steering vectors" and/or clamping the relevant feature at a high activation in Functionality 1 to direct the interpretive process, almost certainly enhancing the relevance of the generated trees.

## Contributions

Contributions are welcome. Please open an issue or submit a pull request to discuss your ideas or enhancements.

## License

This project is licensed under the GNU General Public License v3.0 - see the LICENSE file for details.

