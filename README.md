# The Visual Storyteller

Image captioning final project for Deep Learning.

This project builds a neural network that takes an image as input and generates a natural language caption describing the image.

## Overview

The project uses a CNN + LSTM image captioning architecture:

* **Encoder:** pretrained ResNet50 image feature extractor
* **Decoder:** LSTM caption generator
* **Dataset:** approximately 8,000 images with 5 human-written captions per image
* **Task:** image input → generated text caption

Training and inference were done in Google Colab using GPU.

## Repository Structure

```text
visual-storyteller/
├── notebooks/
│   ├── data_and_training.ipynb
│   └── inference.ipynb
├── artifacts/
│   └── .gitkeep
├── data/
│   └── .gitkeep
├── requirements.txt
├── .gitignore
└── README.md
```

The `data/` and `artifacts/` folders are placeholders. Large dataset files and trained model files are not committed to GitHub.

## Notebooks

### `data_and_training.ipynb`

Contains the full training pipeline:

* dataset loading
* caption cleaning and preprocessing
* train/validation/test split by image
* vocabulary creation
* PyTorch Dataset and DataLoader
* ResNet50 encoder + LSTM decoder model
* training and validation loops
* loss tracking
* saving trained model artifacts

Best validation loss:

```text
2.7126
```

The best model checkpoint was saved after epoch 4.

### `inference.ipynb`

Contains the inference pipeline:

* loading saved model artifacts
* recreating the trained model architecture
* image preprocessing
* greedy decoding
* caption generation for unseen test images
* success examples and failure cases

The notebook includes the required function:

```python
def generate_caption(image_path: str, model: any) -> str:
    """
    Takes a path to an image and returns a generated caption string.
    """
```

## Dataset

The dataset is not included in this repository because of file size.

Expected structure after extraction:

```text
/content/data/
├── captions.txt
└── Images/
```

In Colab, the dataset was stored in Google Drive as:

```text
/content/drive/MyDrive/caption_data.zip
```

and extracted into:

```text
/content/data
```

## Model Artifacts

The trained model artifacts are not committed to GitHub because of file size.

Saved artifacts:

```text
best_model.pt
vocab.pkl
config.json
training_history.json
```

In Colab, they were saved to:

```text
/content/drive/MyDrive/deep_learning_final/artifacts
```

## Training Details

Main configuration:

```text
Encoder: ResNet50
Decoder: LSTM
Embedding dimension: 256
Hidden dimension: 512
Batch size: 64
Max caption length: 40
Optimizer: Adam
Learning rate: 1e-3
Loss: CrossEntropyLoss with padding ignored
Epochs trained: 5
```

The ResNet50 encoder was frozen, and the LSTM decoder was trained on the captioning task.

## Results

The model can generate simple captions for unseen test images. It works best on common scenes involving people, children, dogs, outdoor activities, and simple actions.

Some captions correctly identify the main subject or action. Other captions are generic or incorrect, especially for complex images with multiple objects or unusual scenes.

Possible improvements:

* train for more epochs
* add beam search decoding
* fine-tune the CNN encoder
* add an attention mechanism
* use a transformer-based decoder

## How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run training

Open and run:

```text
notebooks/data_and_training.ipynb
```

This notebook trains the model and saves the artifacts.

### 3. Run inference

Open and run:

```text
notebooks/inference.ipynb
```

This notebook loads the saved model artifacts and generates captions for unseen test images.

## Notes

This project used a hybrid workflow:

* Google Colab for GPU training and inference
* Google Drive for dataset and trained artifacts
* GitHub for notebooks, documentation, and project structure
