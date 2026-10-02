# 🐱🐶 Cat vs Dog Classifier

A deep learning-based **binary image classification project** that uses a Convolutional Neural Network (CNN) to classify images as either **Cat** or **Dog**.

The project is implemented using **TensorFlow/Keras** and includes both a local Jupyter Notebook and a Google Colab notebook for training and experimentation.

A trained `.h5` model is also included for inference and prediction.

---

## 📌 Project Overview

Classifying images of cats and dogs is a common computer vision problem and a useful introduction to deep learning.

This project builds a custom CNN that learns visual patterns from cat and dog images and predicts the class of a new image.

The complete workflow includes:

```text
Dataset
   ↓
Image Cleaning
   ↓
Image Resizing
   ↓
Train / Validation / Test Split
   ↓
CNN Model
   ↓
Model Training
   ↓
Evaluation
   ↓
Trained Model
   ↓
Cat / Dog Prediction
```

---

## ✨ Features

* 🐱 Cat vs Dog binary image classification
* 🧠 Custom Convolutional Neural Network
* 🖼️ Image preprocessing and resizing
* 📊 Dataset distribution analysis
* 🔀 Training and validation split
* 📈 Training accuracy and loss monitoring
* 💾 Trained model saved in `.h5` format
* 🎥 Real-time webcam-based prediction using OpenCV
* ☁️ Google Colab training support
* ⚡ GPU-compatible Colab workflow

---

## 🛠️ Tech Stack

### Programming Language

* Python

### Deep Learning

* TensorFlow
* Keras
* Convolutional Neural Networks (CNN)

### Data Processing

* NumPy
* Pandas

### Computer Vision

* OpenCV

### Visualization

* Matplotlib

### Machine Learning Utilities

* Scikit-learn

### Development Environment

* Jupyter Notebook
* Google Colab

---

## 📂 Project Structure

```text
Cat-vs-Dog-Classifier/
│
├── cat_dog_classifier.ipynb
├── cat_dog_classifier_colab.ipynb
├── cat_dog_classifier.h5
├── requirements.txt
└── README.md
```

### Files

| File                             | Description                           |
| -------------------------------- | ------------------------------------- |
| `cat_dog_classifier.ipynb`       | Local training and inference notebook |
| `cat_dog_classifier_colab.ipynb` | Google Colab training notebook        |
| `cat_dog_classifier.h5`          | Trained CNN model                     |
| `requirements.txt`               | Python dependencies                   |
| `README.md`                      | Project documentation                 |

---

## 📊 Dataset

The project uses the **Kaggle Cats vs Dogs dataset**.

Dataset source:

`https://www.kaggle.com/datasets/karakaggle/kaggle-cat-vs-dog-dataset`

The Colab notebook downloads the dataset using the Kaggle API and extracts it before training.

### Dataset Statistics

The dataset contains:

* **24,959 images**
* **2 classes**
* **Cat:** 12,490 images
* **Dog:** 12,469 images

The notebook uses an 80/20 split for training and validation. Approximately:

* **19,968 images** → training
* **4,991 images** → validation pool

The validation pool is subsequently divided into validation and test subsets.

---

## 🖼️ Image Processing

Images are resized to:

```text
128 × 128 pixels
```

The model receives RGB image data and the inference pipeline normalizes pixel values to the range:

```text
0 – 1
```

by dividing pixel values by `255.0`.

The same preprocessing approach is used during webcam inference.

---

## 🧠 CNN Architecture

The project uses a custom CNN architecture.

```text
Input Image
128 × 128 × 3
      │
      ▼
Conv2D - 32 filters
      │
MaxPooling2D
      │
      ▼
Conv2D - 64 filters
      │
MaxPooling2D
      │
      ▼
Conv2D - 128 filters
      │
MaxPooling2D
      │
      ▼
Conv2D - 256 filters
      │
MaxPooling2D
      │
      ▼
Flatten
      │
Dense - 128
      │
Dropout - 0.5
      │
Dense - 1
Sigmoid
      │
      ▼
Cat / Dog
```

The model uses four convolutional layers with 32, 64, 128 and 256 filters respectively, followed by a 128-unit dense layer, 50% dropout and a single sigmoid output neuron.

---

## ⚙️ Training Configuration

| Parameter         | Value               |
| ----------------- | ------------------- |
| Image Size        | 128 × 128           |
| Batch Size        | 32                  |
| Epochs            | 20                  |
| Optimizer         | Adam                |
| Loss Function     | Binary Crossentropy |
| Output Activation | Sigmoid             |
| Classes           | 2                   |

The training configuration is directly defined in the Colab notebook.

---

## 📈 Model Performance

The trained model achieved the following recorded test performance:

### Test Accuracy

**88.52%**

```text
Test Accuracy: 0.8851933479309082
```

The final training output also reached approximately **98.43% training accuracy** by epoch 20.

### Training Progress

The recorded training accuracy increased throughout the training process:

```text
Epoch 1  → 61.37%
Epoch 5  → 88.07%
Epoch 10 → ...
Epoch 20 → 98.43%
```

This demonstrates that the CNN successfully learned distinguishing visual features from the training dataset.

---

## 💾 Trained Model

A trained model is included in the repository:

```text
cat_dog_classifier.h5
```

The model is loaded using TensorFlow/Keras:

```python
model = tf.keras.models.load_model("cat_dog_classifier.h5")
```

The trained model can therefore be used for inference without retraining the CNN.

---

## 🎥 Real-Time Webcam Prediction

The project also supports real-time classification using a webcam.

The inference pipeline is:

```text
Webcam Frame
     ↓
Resize to 128 × 128
     ↓
Normalize Pixel Values
     ↓
CNN Model
     ↓
Prediction
     ↓
Cat / Dog
     ↓
Confidence Score
```

The notebook uses OpenCV to capture webcam frames and displays the predicted class and confidence score directly on the video feed.

Press **ESC** to exit the webcam prediction window.

---

## 🚀 Installation

Clone the repository:

```bash
git clone https://github.com/AyushShrivastava2808/Cat-vs-Dog-Classifier.git
```

Navigate into the project:

```bash
cd Cat-vs-Dog-Classifier
```

Create a virtual environment:

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Project

### Option 1 — Local Jupyter Notebook

Start Jupyter:

```bash
jupyter notebook
```

Open:

```text
cat_dog_classifier.ipynb
```

Run the cells sequentially.

The notebook can load the trained model and perform webcam-based inference.

---

### Option 2 — Google Colab

Open:

```text
cat_dog_classifier_colab.ipynb
```

in Google Colab.

The notebook downloads the Kaggle dataset, prepares the images, trains the CNN and evaluates the model.

For faster training, the notebook is configured for a GPU-enabled Colab environment.

---

## 🔍 Prediction

The prediction process uses the following logic:

```python
predictions = model.predict(img_array)

predicted_index = np.argmax(predictions[0])
predicted_label = class_names[predicted_index]
confidence_score = np.max(predictions[0])
```

The model predicts one of:

```text
Cat
Dog
```

along with a confidence score.

---

## 📌 Key Learning Outcomes

This project demonstrates practical implementation of:

* Convolutional Neural Networks
* Binary image classification
* TensorFlow/Keras
* Image preprocessing
* Dataset splitting
* CNN architecture design
* Binary cross-entropy loss
* Sigmoid activation
* Model training
* Model evaluation
* Model saving and loading
* OpenCV webcam inference
* Google Colab GPU training

---

## 🔮 Future Improvements

Possible improvements include:

* Data augmentation
* Batch normalization
* Early stopping
* Learning-rate scheduling
* Transfer learning using pretrained models
* Model optimization
* Streamlit web interface
* Improved error analysis
* Confusion matrix and classification report
* Deployment as a web application

---

## ⚠️ Important Note

The training notebook downloads the dataset through the Kaggle API.

For security, **never commit Kaggle usernames, API keys, passwords, tokens or other credentials to GitHub**.

Use environment variables or Kaggle's local credential configuration instead.

---

## 👨‍💻 Author

**Ayush Shrivastava**

GitHub:

https://github.com/AyushShrivastava2808

---

## ⭐ Project

If you find this project useful, feel free to ⭐ the repository.
