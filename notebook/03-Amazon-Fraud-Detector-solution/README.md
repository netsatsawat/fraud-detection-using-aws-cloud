# Detect fraud activities using Amazon Fraud Detector

Build, deploy, and manage fraud detection models **without previous machine learning (ML) experience**.

## How it works
Amazon Fraud Detector is a **fully managed service** enabling customers to identify potentially fraudulent activities and catch more online fraud faster.

<img src="https://d1.awsstatic.com/fraud-detector/Product-Page-Diagram_Amazon-Fraud-Detector.1d59515b4eab27cdb9e253245682459c3c765b82.png">

## Demonstration
In this demonstration, I use `boto3` SDK to build Fraud detector utilizing Amazon Fraud Detector service. You can opt to build either on console or code.

When using Amazon Fraud Detector, there will be few terms and terminologies you need to understand. Let's imagine the transaction or claim scenario:
1. The **entities** (i.e., can be person, hospital, merchant) make an activities, or **events** (this can be transaction, claim, account registration).
2. This event will consists of data points, or **variable**, which represents the transaction type, amount, etc.
3. This event will result in an **outcome**, or **labels**, which either can be fraud or legit transaction.

Below image demonstrates the overall process with the terms.
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/824e633d5509c7fc68ef691326536a0afd68d31e/img/afd-key-terms1.png">

Now, to detect fraud, usually there are 2 options:
- Domain users have predefine logics or **rules** to filter the events or transactions
- Data scientists have built ML **model** to score or predict each event or transaction

**Amazon Fraud Detector** has the capabilities to combine these 2 methods, known as **Detector**, to buld the ML models using AutoML and define the business **logic** and each logic produce a different **outcome**. For example:
- model score >= 800, outcome is `fraud`
- model score > 500 and model score < 800, outcome is `investigate`
- model score <= 500, outcome is `legit`

You can define various logics and outcomes based on your business objectives.
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/b07cebdf793cffd1050fe959307233bc0c4f06b3/img/afd-key-terms2.png">

To conclude, **Amazon Fraud Detector** consists of processes below.
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/b07cebdf793cffd1050fe959307233bc0c4f06b3/img/afd-how-it-works.png">
