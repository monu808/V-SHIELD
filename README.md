# DeepShield: AI Powered Deepfake Detection Tool

DeepShield is a deep learning-based tool designed to detect deepfake images. It preprocesses images to extract faces using MTCNN, trains a classifier using transfer learning with the Xception model, and offers a Flask web application for real-time detection. This project is especially geared toward aiding law enforcement investigations by providing a quick and accessible deepfake detection solution.

## Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Folder Structure](#folder-structure)
- [Usage](#usage)
  - [Data Preprocessing](#data-preprocessing)
  - [Training the Model](#training-the-model)
  - [Evaluating the Model](#evaluating-the-model)
  - [Running the Flask App](#running-the-flask-app)
- [Troubleshooting](#troubleshooting)
- [Future Enhancements](#future-enhancements)
- [License](#license)

## Features
- **Face Detection & Preprocessing:** Uses MTCNN to detect and crop faces from input images.
- **Deepfake Detection:** Utilizes a fine-tuned Xception model for binary classification (Real vs. Deepfake).
- **Web Interface:** A simple Flask-based dashboard for uploading images and viewing prediction results.
- **Forensic Ready:** (Planned) Capability to generate detailed forensic reports for law enforcement.

## Requirements
- Python 3.6+
- TensorFlow & Keras
- OpenCV
- MTCNN
- Flask
- NumPy, Matplotlib, scikit-learn

## Installation

1. **Clone the Repository:**

   ```bash
   git clone <repository_url>
   cd deepshield
Create and Activate a Virtual Environment (Optional but Recommended):

bash
python -m venv deepshield_env
source deepshield_env/bin/activate  # On Windows: deepshield_env\Scripts\activate
Install the Required Packages:

deepshield/
│
├── dataset/
│   ├── real/
│   │   ├── real1.jpg
│   │   └── real2.jpg
│   └── fake/
│       ├── fake1.jpg
│       └── fake2.jpg
│
├── processed_dataset/       # Generated after running preprocess.py
│   ├── real/
│   └── fake/
│
├── templates/
│   └── index.html           # HTML template for the Flask web app
│
├── preprocess.py            # Face detection & cropping script using MTCNN
├── train_model.py           # Script to build and train the deepfake detection model
├── evaluate_model.py        # Script to evaluate the trained model
└── app.py                   # Flask application for real-time image prediction

Usage
Data Preprocessing
Before training, preprocess your images to extract faces:

Place your raw images in the following structure:

sql
dataset/
    real/   (images with real faces)
    fake/   (images with deepfake faces)
Run the preprocessing script:

bash
python preprocess.py
This script uses MTCNN to detect faces and saves the cropped images in a new folder called processed_dataset/.

Training the Model
Train the deepfake detection model using the preprocessed data:

bash
python train_model.py
The script leverages transfer learning with the Xception model.
The best-performing model is saved as deepshield_best.h5.
Training parameters and augmentation options can be adjusted in the script.
Evaluating the Model
After training, you can evaluate the model on a separate test set:

Organize your test dataset (e.g., in a folder named processed_dataset_test/ with the same structure as processed_dataset/).

Run the evaluation script:

bash
python evaluate_model.py
The script will output the test accuracy and loss.

Running the Flask App
Launch the Flask web application to perform real-time deepfake detection:

bash
python app.py
Open your browser and navigate to http://127.0.0.1:5000/.
Use the provided web interface to upload an image.
The app will return a prediction (Real or Deepfake) along with a confidence score.
Troubleshooting
TensorFlow CPU Optimization Message:
You may see a message about CPU instructions (e.g., SSE, AVX) when running the scripts. This is an informational log. To suppress it, set:

bash
export TF_CPP_MIN_LOG_LEVEL=2  # Linux/macOS
set TF_CPP_MIN_LOG_LEVEL=2     # Windows (Command Prompt)
Face Not Detected:
If a face is not detected in an image, ensure that the image contains a clear, front-facing face. The script will notify you if no face is found.

Dependency Issues:
Confirm all required packages are installed and that you are using a compatible Python version.

Future Enhancements
Video Analysis: Extend the tool to analyze videos frame-by-frame.
Forensic Reporting: Automate the generation of detailed forensic reports with annotated evidence.
Adversarial Robustness: Improve model robustness against adversarial attacks.
License
This project is licensed under the MIT License.
