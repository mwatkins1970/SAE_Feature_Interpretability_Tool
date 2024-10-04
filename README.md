[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mwatkins1970/SAE_Feature_Interpretability_Tool/blob/main/notebooks/SAE_feature_interpretability_multitool.ipynb)

# Gemma-2B SAE Feature Interpretability Multitool

This tool assists in the interpretability of sparse autoencoder (SAE) features, specifically those trained by Joseph Bloom on the Gemma-2B model. By visualizing and probing the representations learned by these SAEs, the multitool supports a detailed examination of latent features and their interactions within large language models (LLMs). 

## Overview

The tool offers two main functionalities that serve as experimental probes into the model's learned representations:

1. **Definition Trees for Ghost Tokens**: This functionality uses feature vectors to generate interpretive "definition trees," revealing complex, hierarchical token relationships.
2. **Token Lists by Embedding Similarity**: This function generates lists of tokens that exhibit embedding similarities to the selected feature vector, shedding light on the kinds of token meanings associated with specific model features.

These tools can potentially aid in studying model alignment issues, such as interpretability, the impact of post-training adjustments, and persona stability within SAEs. 

### Functionality 1: Definition Trees

This function constructs a "definition tree" based on a user-selected SAE feature vector. Users can control the construction parameters, including:

- **SAE Layer**: Choice of encoder or decoder feature weights at layers 0, 6, 10, or 12.
- **Token Centroid Offset**: Optionally offsets the feature vector by the token embedding centroid, shifting the "ghost token" toward a central token embedding.
- **Scaling and PCA Adjustments**: Fine-tune feature influence through scaling and PCA weighting.

The result is a tree that maps relationships between tokens based on their cumulative probability in a rollout process, providing a visualized hierarchy that aids in interpretability.

### Functionality 2: Token Lists

This function identifies the top tokens closest to the feature vector according to a customizable cosine distance metric. Key configurable parameters include:

- **Numerator Exponent**: Adjusts the distance metric by scaling the cosine distance.
- **PCA Component Weighting**: Modifies the feature vector with principal component directions for exploratory analysis.
- **Centroid Offset and Scaling**: Controls vector scaling and adjusts the feature vector origin, allowing for comparative studies of token proximity.

These token lists can facilitate concept-based interpretability studies and offer empirical insights into the emergent behaviors that may arise as a consequence of feature activation.

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

## Future Directions

There is significant scope for enhancing and extending this tool. Possible additions include:

- **Adaptation to Other Models**: The tool could be generalized to work with SAEs trained on other LLMs.
- **Improved Control Integration**: Merging common controls between functionalities for streamlined interaction.
- **Enhanced Base Prompt Customization**: Allowing user-defined prompts for the "ghost token" definitions.
- **Expanded PCA and Linear Combination Capabilities**: Exploring the impacts of multiple PCA components and combinations of encoder and decoder features.
- **API Integration for Feature Interpretation**: Exporting outputs for further interpretation using LLMs like ChatGPT-4 or Claude, enabling automated analysis.
- **Steering Vector Applications**: Leveraging feature vectors as "steering vectors" to direct the interpretive process, potentially enhancing the clarity and relevance of the generated trees.

## Contributions

Contributions are welcome. Please open an issue or submit a pull request to discuss your ideas or enhancements.

## License

This project is licensed under the GNU General Public License v3.0 - see the LICENSE file for details.

