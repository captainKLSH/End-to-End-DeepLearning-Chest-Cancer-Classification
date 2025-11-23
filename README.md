# End-to-End MLOps Pipeline for Chest Cancer Detection 
### From Raw Data to Cloud Deployment: A full-lifecycle Deep Learning system.

Medical image classification requires high accuracy, but distinct operational challenges exist in reproducibility and deployment. The goal was to build a standardized, modular pipeline to detect Chest Cancer from CT scan images, moving beyond ad-hoc scripts to a production-grade system.

I engineered a modular MLOps pipeline using Python and Deep Learning:

- **Structured Ingestion:** Designed a robust data pipeline with custom ConfigurationManagers and YAML-based config handling to ensure reproducible data ingestion and preprocessing.

- **Transfer Learning:** Leveraged the pre-trained VGG16 architecture , fine-tuning it for the specific domain of chest cancer detection. This approach maximized performance (78% accuracy) despite limited medical data.

- **Experiment Tracking:** Integrated MLflow to log metrics, visualize loss curves, and manage hyperparameter tuning experiments, ensuring the best model version was selected for production.

The Deployment (CI/CD) The final model wasn't just saved locally; it was containerized and shipped to the cloud:

- **Containerization:** Built a Docker image of the source code and dependencies.

- **Cloud Infrastructure:** Pushed the image to AWS ECR (Elastic Container Registry) and deployed it to a production environment using AWS EC2, making the inference API accessible globally.

**MLflow**

- Its Production Grade
- Trace all of your expriements
- Logging & taging your model

**DVC** 

- Its very lite weight for POC only
- lite weight expriements tracker
- It can perform Orchestration (Creating Pipelines)

# ⚙️ Usage

## AWS-CICD-Deployment-with-Github-Actions

### 1. Login to AWS console.

### 2. Create IAM user for deployment
```bash
    #with specific access
	1. EC2 access : It is virtual machine
	2. ECR: Elastic Container registry to save your docker image in aws
	#Description: About the deployment
	1. Build docker image of the source code
	2. Push your docker image to ECR
	3. Launch Your EC2 
	4. Pull Your image from ECR in EC2
	5. Lauch your docker image in EC2
	#Policy:
	1. AmazonEC2ContainerRegistryFullAccess
	2. AmazonEC2FullAccess
```
	
## 3. Create ECR repo to store/save docker image
```- Save the URI: 566373416292.dkr.ecr.us-east-1.amazonaws.com/<file>```

	
## 4. Create EC2 machine (Ubuntu) 

## 5. Open EC2 and Install docker in EC2 Machine:
```bash
	#optinal
	sudo apt-get update -y
	sudo apt-get upgrade
	#required
	curl -fsSL https://get.docker.com -o get-docker.sh
	sudo sh get-docker.sh
	sudo usermod -aG docker ubuntu
	newgrp docker
```
# 6. Configure EC2 as self-hosted runner:
```setting>actions>runner>new self hosted runner> choose os>``` then run command one by one


# 7. Setup github secrets:
```bash
    AWS_ACCESS_KEY_ID=
    AWS_SECRET_ACCESS_KEY=
    AWS_REGION = us-east-1
    AWS_ECR_LOGIN_URI = demo>>  
```