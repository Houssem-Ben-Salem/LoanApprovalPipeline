# Loan Approval Prediction MLOps Pipeline

This repository implements an end-to-end *MLOps pipeline* for a *Loan Approval Prediction* system. The project automates data fetching, model training, containerization, CI/CD deployment, and model monitoring using tools like Docker, GitHub Actions, Google Cloud Platform (GCP), and Evidently AI.

---

## 🚀 Features

1. *CI/CD Automation*:
   - Automated builds, tests, and deployments using GitHub Actions.
   - Continuous deployment to Google Cloud Run.

2. *Model Development*:
   - Training pipeline with support for hyperparameter tuning.
   - Support for state-of-the-art models like XGBoost and CatBoost.

3. *Monitoring*:
   - Integrated with *Evidently AI* for monitoring data drift and model performance.
   - Logging and metrics tracking using Google Cloud Monitoring.

4. *Containerization*:
   - Dockerized application for scalable deployment.
   - Support for both training and inference containers.

5. *Feedback Loop*:
   - Gradio-based feedback interface to improve model predictions.
   - Automated retraining with user feedback.

---

## 📦 Installation

1. *Clone the Repository*:
   
   git clone https://github.com/yassineboumaiza/LoanApprovalPipeline.git
   cd LoanApprovalPipeline
   

2. *Set Up Python Environment*:
   
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   

3. *Set Up GCP Authentication*:
   - Save the GCP service account key as a base64-encoded secret (GCP_SERVICE_ACCOUNT_KEY) in GitHub.
   - Locally, copy the key to /tmp/key.json:
     
     cp loanapprovalprediction-442813-de39e566af07.json /tmp/key.json
     export GOOGLE_APPLICATION_CREDENTIALS=/tmp/key.json
     

4. *Build and Run the Docker Container Locally*:
   
   docker build -t loan-approval-pipeline .
   docker run -p 8080:8080 loan-approval-pipeline
   

---

## 🚀 Usage

### 1. *Run the Inference Service Locally*:
   
   cd app
   python gradio_inference.py
   
   Access the Gradio app at [http://localhost:8080](http://localhost:8080).

### 2. *Train the Model*:
   Run the training pipeline:
   
   python src/pipeline/run_pipeline.py
   

---

## 🌐 CI/CD Pipeline

### Workflow: **train-pipeline.yml**
This GitHub Actions workflow automates the CI/CD process:
1. Fetches the latest dataset from Google Cloud Storage.
2. Builds and pushes the Docker image to GCP Artifact Registry.
3. Deploys the image to Google Cloud Run.

#### Trigger: Push to main branch.

---

## 🔍 Monitoring

### Data and Concept Drift
- Integrated with *Evidently AI* to detect:
  - Data drift.
  - Target distribution changes.
  - Feature importance changes.

### Access Monitoring Reports:
Reports are generated and stored locally as monitoring_report.html.

---

## 🔄 Feedback Loop

- *Modify Predictions*: Users can review and modify model predictions via the Gradio app.
- *Save Feedback*: Updated records are saved to Google Cloud Storage for retraining.

---

## 🧪 Testing

- *Unit Tests*: Add tests to validate individual components.
- *Integration Tests*: Ensure end-to-end functionality of the pipeline.

Example:
pytest tests/

---

## 🌐 Deployment

1. *Deploy Training Pipeline*:
   
   gcloud run deploy loan-approval-training \
       --image us-central1-docker.pkg.dev/${PROJECT_ID}/loan-approval-repo/loan-approval-pipeline \
       --platform managed \
       --allow-unauthenticated
   

2. *Deploy Inference Service*:
   
   gcloud run deploy loan-approval-inference \
       --image us-central1-docker.pkg.dev/${PROJECT_ID}/loan-approval-repo/inference-service \
       --platform managed \
       --allow-unauthenticated
   

---

## 🔧 Future Enhancements

1. *Add Model Explainability*:
   - Integrate SHAP or LIME to explain model predictions.

2. *Improve Feedback Loop*:
   - Automate retraining based on user feedback.

3. *Add Experiment Tracking*:
   - Integrate tools like [Weights & Biases](https://wandb.ai/) for experiment tracking.

4. *Integrate Alerts*:
   - Set up Google Cloud Monitoring to notify on anomalies.

---

## 🛠️ Built With

- *Google Cloud Platform*:
  - Cloud Storage, Artifact Registry, Cloud Run, Cloud Monitoring.
- *Docker*:
  - Containerized training and inference services.
- *GitHub Actions*:
  - CI/CD pipeline for automated deployment.
- *Evidently AI*:
  - Monitoring for data and model drift.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1. Fork this repository.
2. Create a feature branch:
   
   git checkout -b feature/new-feature
   
3. Push your changes and create a pull request.

---

## 🛡️ License

This project is licensed under the MIT License. See LICENSE for more details.
