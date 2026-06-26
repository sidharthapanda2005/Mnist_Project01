# **MNIST Digit Classification & FastAPI Deployment**

## **Project Overview**
This project demonstrates how to build, train, and deploy an **Artificial Neural Network (ANN)** to classify handwritten digits using the famous **MNIST dataset**. The repository contains two primary components:
1. An exploratory **Jupyter Notebook** (`ANN01.ipynb`) used to experiment with different neural network architectures, activation functions, and optimizers.
2. A **Python API** built with **FastAPI** that serves a trained Keras model, allowing users to upload an image and receive a digit prediction.

## **Key Features**
* **Model Exploration:** Uses **TensorFlow** and **Keras** to build sequential models ranging from simple flattened layers to deep networks with multiple hidden layers.
* **Data Preprocessing:** Handles image normalization (scaling pixel values by **dividing by 255**) and flattening arrays for dense layer compatibility.
* **REST API:** Provides a fully functional backend using **FastAPI** to accept image uploads (**`multipart/form-data`**) and return predictions.

## **Dependencies & Installation**
To run this project locally, ensure you have **Python 3.x** installed. You will need the following core libraries:

* **FastAPI**
* **Uvicorn**
* **python-multipart** (required for FastAPI file uploads)
* **TensorFlow**
* **Pandas**
* **NumPy**
* **Pillow (PIL)**
* **Matplotlib**

You can install the required packages using pip:
**`pip install fastapi uvicorn python-multipart tensorflow pandas numpy pillow matplotlib scikit-learn`**

## **How to Run the API**

**1. Update File Paths:**
Before running the application, ensure that the file paths for **`mnist_train.csv`** and **`mnist_test.csv`** inside the FastAPI script accurately point to the locations on your local machine.

**2. Start the Uvicorn Server:**
Navigate to the directory containing your FastAPI script (e.g., `main.py`) and run the following command in your terminal:
**`uvicorn main:app --host 127.0.0.1 --port 5000`**

**3. Access the API:**
Once the server is running, you can access the application locally at:
**`http://127.0.0.1:5000`**

You can also test the endpoints interactively using FastAPI's built-in Swagger UI documentation by navigating to:
**`http://127.0.0.1:5000/docs`**

## **API Endpoints**

### **`GET /`**
* **Description:** A simple health check/welcome endpoint.
* **Response:** **`{"Deployment": "Hello and Welcome to 5 Minutes Engineering"}`**

### **`POST /predict`**
* **Description:** Accepts an image file, preprocesses it (converts to grayscale, resizes, and normalizes), and predicts the handwritten digit. 
* **Input:** A file upload parameter named **`file`**.
* **Response:** Returns the predicted number as a string word. Example: **`{"Prediction": "seven"}`**

## **Future Improvements & Architecture Notes**
Currently, the FastAPI script is designed to **train the neural network dynamically** every time a request is made to the **`/predict`** endpoint. 

For production-level deployments, the architecture should be refactored to:
1. **Train the model once** in a separate script or notebook.
2. **Save the trained model** to disk (e.g., using **`model.save('mnist_model.h5')`**).
3. **Load the pre-trained model** when the FastAPI server starts, so the `/predict` endpoint only performs inference, drastically reducing response times.
