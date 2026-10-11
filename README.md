# 🍅 Plant Disease Classification using Deep Learning

> Classify tomato leaf diseases from photos, and see **why a CNN beats traditional models on image data**.

![Python](https://img.shields.io/badge/Python-3.12-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📖 Project in One Minute

| Question | Answer |
|---|---|
| **What does it do?** | Takes a photo of a tomato leaf and predicts which disease it has |
| **Why?** | Plant diseases reduce crop yield. Early detection helps farmers save crops |
| **How?** | Trains and compares 4 models on the same leaf images |
| **Main finding** | CNN models understand leaf patterns (spots, edges, colour changes) far better than models that treat an image as a flat list of numbers |

---

## 🗂️ Dataset

- **Source:** PlantVillage (available on Kaggle)
- **Classes used (5):**
  1. Tomato Bacterial Spot
  2. Tomato Early Blight
  3. Tomato Late Blight
  4. Tomato Leaf Mold
  5. Tomato Septoria Leaf Spot
- **Split:** the dataset already comes divided into `train`, `val` and `test` folders
- **Image size:** resized to 64 x 64 pixels (RGB). Can be increased for better accuracy
- **Samples per class:** adjustable in the notebook (`TRAIN_PER_CLASS`, `VAL_PER_CLASS`, `TEST_PER_CLASS`)

> Download it from Kaggle (search "PlantVillage") and place it inside the `data/` folder.

---

## 🔄 Project Flow

```
Load images  ->  Check data  ->  Normalize  ->  Train 4 models  ->  Compare results
```

1. **Load data** from the `train`, `val` and `test` folders and resize every image
2. **Check data** quality: shapes, pixel range, missing values, sample images, class balance
3. **Normalize** pixel values from 0-255 to 0-1
4. **Flatten** images for the two non-CNN models
5. **Train models** (explained below)
6. **Evaluate** every model on unseen test images using accuracy, confusion matrix and classification report
7. **Compare** all models in one table

---

## 🤖 Models Used

| # | Model | Purpose | How it sees the image |
|---|---|---|---|
| 1 | **Logistic Regression** | **Baseline** (simple starting point to compare against) | A flat list of 12,288 numbers |
| 2 | **Simple Neural Network** | Slightly stronger model with Dense layers | A flat list of numbers |
| 3 | **CNN** | Image-focused model | Looks at the image directly, detects local patterns |
| 4 | **Improved CNN** | Final model | Same as CNN plus the improvements below |

### What makes the Improved CNN better?
- **Data augmentation:** random flips, rotations and zoom, so the model learns from more varied views of a leaf
- **Batch Normalization:** makes training more stable and faster
- **Dropout:** reduces overfitting (memorising the training images)
- **Early Stopping:** stops training when validation stops improving
- **Learning rate scheduler:** lowers the learning rate automatically when progress slows

---

## 📊 Results

Models

Logistic Regression is the baseline. Every image is flattened into one long list of pixel values, and the model learns a simple decision boundary from that.

Neural Network is a small fully connected network, also trained on flattened images.

CNN uses convolution and pooling layers, so it works on the image directly instead of a flattened list. This lets it pick up local patterns like spots, edges and colour changes on the leaf.

Results

Accuracy on the test set:

Model	Test Accuracy (%)
Logistic Regression	62.6
Neural Network	65.0
CNN	86.2

### How to read the results
- **Accuracy:** out of all test images, the percentage predicted correctly
- **Confusion matrix:** shows which diseases get mixed up with each other
- **Training graph:** if the training line is much higher than the validation line, the model is overfitting

### Key takeaway
Logistic Regression and the simple Neural Network lose the spatial structure of the image when it is flattened. CNNs keep it, so they pick up disease spots and texture much better. This is why accuracy improves from the baseline to the CNN models.

---

## 📁 Project Structure

```
D.L. Project/
├── data/                      # dataset (not uploaded to GitHub)
│   ├── train/                 # one sub-folder per disease class
│   ├── val/
│   └── test/
├── notebooks/
│   └── plant_disease.ipynb    # complete project code
├── requirements.txt           # libraries needed
├── .gitignore                 # files Git should ignore
└── README.md                  # this file
```

---

## ▶️ How to Run

**1. Clone the repository**
```bash
git clone <your-repo-link>
cd "D.L. Project"
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv312
venv312\Scripts\activate          # Windows
# source venv312/bin/activate     # Mac / Linux
```

**3. Install the libraries**
```bash
pip install -r requirements.txt
```

**4. Add the dataset**
Download PlantVillage and arrange it like this:
```
data/train/<class_name>/*.jpg
data/val/<class_name>/*.jpg
data/test/<class_name>/*.jpg
```

**5. Open the notebook**
Open `notebooks/plant_disease.ipynb` in VS Code, select the `venv312` kernel and click **Run All**.

> If your data is in a different location, change `TRAIN_DIR`, `VAL_DIR` and `TEST_DIR` in the settings cell.
> From inside the `notebooks` folder, relative paths like `../data/train` work on any computer.

---

## 🛠️ Tech Stack

- Python 3.12
- TensorFlow / Keras
- scikit-learn
- NumPy and Pandas
- Matplotlib
- Pillow

---

## 💡 What I Learned

- How to prepare and validate an image dataset
- Why a baseline model is important for comparison
- Why CNNs work better than flattened-image models
- How data augmentation and callbacks reduce overfitting
- How to read confusion matrices and training curves

---

## 🚀 Future Improvements

- Train on all PlantVillage classes (38 classes, multiple crops)
- Use transfer learning (MobileNet, ResNet)
- Build a web app where a user uploads a leaf photo and gets the disease name
- Add disease treatment suggestions

---

## 👤 Author

**Yash Trivedi**
GitHub: [Yash958035](https://github.com/Yash958035)