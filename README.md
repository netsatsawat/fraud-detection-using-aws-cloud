# Fraud Detection using AWS Cloud
This repository outlines various solutions using AWS Cloud's AIML services to detect fraud faster.

### Table of contents
- [Introduction](https://github.com/netsatsawat/fraud-detection-using-aws-cloud#Introduction)
- [Solutions using AWS services](https://github.com/netsatsawat/fraud-detection-using-aws-cloud#Solutions-using-AWS-services)
  
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/90ef058e3c3c8b37bc9b5777e9e2476998c4ee8d/img/fraud-detector-AI.jpg" width=400>

## Introduction

**Fraud detection** is the process of identifying fraudulent activities, such as identity theft, financial fraud, and claim fraud. This can be applied in broad range of industries, as such it is crucial for organizations to have effective fraud detection systems in place. Fraud detection is a critical process for organizations across sectors to limit financial losses, comply with industry regulations, maintain their reputations, and deter fraudsters. Investing in fraud detection capabilities delivers major benefits and protects companies from potentially significant risks and damages.

## Solutions using AWS services
In AWS Cloud, there are many solution for data scientists and data analysts to build, train, and deploy the fraud detection model. Also this repository contains the Python code as notebook to run on Amazon SageMaker to replicate the solutions.

There are 2 main serivces that I would like to focus on;
- **[Amazon Fraud Detector](https://aws.amazon.com/fraud-detector/)**
- **[Amazon SageMaker](https://aws.amazon.com/sagemaker/)**

Let's quickly look at each service below, however, I encourage the readers to go to the website and read its documentation.

### Amazon Fraud Detector

Amazon Fraud Detector is a fully managed service enabling customers to identify potentially fraudulent activities with just a few clicks and without any prior ML experience. Amazon Fraud Detector can be used to define business rules to detect or specify each action to the activities (i.e., you can specify **fraud**, **to investigate**, and **legit** based on the model score).

<img src="https://d1.awsstatic.com/fraud-detector/Product-Page-Diagram_Amazon-Fraud-Detector.1d59515b4eab27cdb9e253245682459c3c765b82.png" width=1200 height=350>

### Amazon SageMaker

Amazon SageMaker Studio is an integrated development environment (IDE) that provides a single web-based visual interface where you can access purpose-built tools to perform all machine learning (ML) development steps, from preparing data to building, training, and deploying your ML models, improving data science team productivity by up to 10x. You can quickly upload data, create new notebooks, train and tune models, move back and forth between steps to adjust experiments, collaborate seamlessly within your organization, and deploy models to production without leaving SageMaker Studio.

<img src="https://d1.awsstatic.com/sagemaker/Amazon-SageMaker-Studio%402x.aa0572ebf4ea9237571644c7f853c914c1d0c985.png" width=1000>


## Things not include in this tutorial
- How to set up AWS account, please refer to this [documentation](https://docs.aws.amazon.com/accounts/latest/reference/welcome-first-time-user.html).
- How to create IAM users or roles, please refer to this [IAM documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

## Remark
Everything I wrote here is my opinion and not involve with my employers.
