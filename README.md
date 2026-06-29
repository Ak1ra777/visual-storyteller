# The Visual Storyteller

Image captioning final project for Deep Learning.

The goal of this project is to build a neural network that takes an image as input and generates a natural language caption describing the image.

## Project Overview

This project uses a CNN + LSTM architecture:

* **Encoder:** pretrained ResNet50 used as an image feature extractor
* **Decoder:** LSTM language model that generates captions word by word
* **Dataset:** approximately 8,000 images, each with 5 human-written captions
* **Task:** image input → generated text caption output

The project was trained and tested in Google Colab using GPU.

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

## Notebooks

### `data_and_training.ipynb`

This notebook contains:

* dataset loading
* caption preprocessing
* train/validation/test split by image
* vocabulary creation
* PyTorch Dataset and DataLoader
* ResNet50 encoder + LSTM decoder model
* training loop
* validation loss tracking
* model artifact saving

Best validation loss:

```text
2.7126
```

The best model was saved after epoch 4.

### `inference.ipynb`

This notebook contains:

* loading trained model artifacts
* recreating the model architecture
* image preprocessing
* greedy decoding
* required caption generation function:

```python
def generate_caption(image_path: str, model: any) -> str:
    """
    Takes a path to an image and returns a generated caption string.
    """
```

It also demonstrates the model on unseen test images and includes both successful examples and failure cases.

## Dataset

The dataset file is not included in this repository because it is large.

Expected dataset structure after extraction:

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

The trained model artifacts are not committed to GitHub because they are large.

Saved artifacts:

```text
best_model.pt
vocab.pkl
config.json
training_history.json
```

In Colab, these were saved to:

```text
/content/drive/MyDrive/deep_learning_final/artifacts
```

## Training Details

Main hyperparameters:

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

The ResNet50 encoder was frozen, and only the decoder layers were trained.

## Results

The model learned to generate simple captions for unseen images. It performs best on common scenes involving people, dogs, children, outdoor activities, and simple actions.

Some generated captions are successful because they correctly identify the main subject or action. However, some captions are generic or incorrect, especially for complex images with multiple objects or unusual scenes.

Possible improvements:

* train for more epochs
* add beam search decoding
* fine-tune the CNN encoder
* add attention mechanism
* use a transformer-based decoder

## How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Run training notebook

Open and run:

```text
notebooks/data_and_training.ipynb
```

This notebook trains the model and saves artifacts.

### 3. Run inference notebook

Open and run:

```text
notebooks/inference.ipynb
```

This notebook loads the saved model and generates captions for unseen test images.

## Notes

This project was developed using a hybrid workflow:

* Google Colab for GPU training and inference
* Google Drive for dataset and model artifacts
* GitHub for notebooks, documentation, and project structure
