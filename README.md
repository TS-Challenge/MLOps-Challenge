# MLOps Playground Challenge: Customer Churn Prediction (40 Points)

## Objective

In this challenge, you are tasked with deploying a pre-trained machine learning model that predicts customer churn using the Bank Customer Churn Dataset. The pre-trained model will be provided as a pickle file (`churn_model.pkl`). You will build a pipeline for loading the model, accepting inputs, and making predictions. The focus will be on the deployment of the model using Docker, testing the pipeline, and automating the process with CI/CD (GitHub Actions).

---

## Task Breakdown

### Task 1: Load the Pre-Trained Model (5 Points)

- Write a Python script (`load_model.py`) that loads the pre-trained model using `pickle`.
- The script should load the model from the `models/` directory, where the pre-trained model (`churn_model.pkl`) is located.

---

### Task 2: Interactive Prediction (10 Points)

- Write a Python script (`run_model.py`) that prompts the user for customer data (credit score, age, balance, number of products, etc.) and returns a prediction on whether the customer will churn.
- Use the pre-trained model to make predictions based on user inputs.

---

### Task 3: Dockerize the Application (10 Points)

- Create a `Dockerfile` that:
  1. Uses a **Python 3.8** image.
  2. Copies the necessary files (model, scripts, etc.) into the container.
  3. Installs the dependencies listed in `requirements.txt`.
  4. Runs the `run_model.py` script inside the container.

---

### Task 4: Set Up CI/CD Pipeline with GitHub Actions (10 Points)

- Write a **GitHub Actions workflow** that:
  1. Installs the dependencies.
  2. Builds the Docker image.
  3. Runs the container to execute the `run_model.py` script.
- The workflow should run every time code is pushed to the `main` branch.
  
#### Example `deploy.yml` (for GitHub Actions):
```yaml
name: Build and Run Model

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'

    - name: Install dependencies
      run: |
        pip install -r requirements.txt

    - name: Build Docker image
      run: |
        docker build -t churn_model .

    - name: Run Docker container
      run: |
        docker run churn_model
