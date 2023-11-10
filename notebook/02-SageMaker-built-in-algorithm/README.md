# Using SageMaker Built-in Algorithm

The **Amazon SageMaker Python SDK** provides framework estimators and generic estimators to train your model while orchestrating the machine learning (ML) lifecycle accessing SageMaker features for training and the AWS infrastructures, such as *Amazon Elastic Container Registry (Amazon ECR)*, *Amazon Elastic Compute Cloud (Amazon EC2)*, and *Amazon Simple Storage Service (Amazon S3)*. 

I would recommend to read the full documentation and how SageMaker workflow acts [here](https://docs.aws.amazon.com/sagemaker/latest/dg/train-model.html).

## Built-in Algorithm: XGBoost 

You can use the new release of the XGBoost algorithm either as a Amazon SageMaker built-in algorithm or as a framework to run training scripts in your local environments. This implementation has a smaller memory footprint, better logging, improved hyperparameter validation, and an expanded set of metrics than the original versions. It provides an XGBoost estimator that executes a training script in a managed XGBoost environment. For more guidelines, please visit the [documentation](https://sagemaker.readthedocs.io/en/stable/algorithms/tabular/xgboost.html).

Below screenshots highlighted some differences from traditional method.  

- Define estimator by getting XGBoost container, defining training instances, S3 location for input, validation, and test datasets.
- Define model hyperparameters and then call `fit()` method.
  
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/0c22ee19a2499c56f0176a2eb43a367a893bafb5/img/xgb-built-in-algorithm-training.png" height=600>

- Model deployment (in this example, I use **real-time inference** as deployment method), you can specify different instance types based on your workload comming in to your API endpoint.

<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/0c22ee19a2499c56f0176a2eb43a367a893bafb5/img/xgb-built-in-algorithm-deployment.png" width=800>


## Scikit-Learn Estimator

To train a **Scikit-learn** model by using SageMaker Python SDK:
- Prepare a training script
- Create a `sagemaker.sklearn.SKLearn` Estimator
- Call the estimator’s fit method

For this specific demonstration, below is the training script. The reason we need to prepare the **training** script is there are multiple algorithms within Scikit-learn.

```{python3}
from __future__ import print_function

import argparse
import joblib
import os
import pandas as pd
from sklearn.ensemble import RandomForestClassifier


if __name__ == '__main__':
    parser = argparse.ArgumentParser()
    
    # Hyperparameters section for RandomForestClassifier algorithm
    parser.add_argument('--n_estimators', type=int, default=100)
    parser.add_argument('--max_depth', type=int, default=4)
    parser.add_argument('--verbose', type=int, default=0)
    parser.add_argument('--random_state', type=int, default=42)
    

    # Sagemaker specific arguments. Defaults are set in the environment variables.
    parser.add_argument('--output-data-dir', type=str, default=os.environ['SM_OUTPUT_DATA_DIR'])
    parser.add_argument('--model-dir', type=str, default=os.environ['SM_MODEL_DIR'])
    parser.add_argument('--train', type=str, default=os.environ['SM_CHANNEL_TRAIN'])

    args = parser.parse_args()

    # Take the set of files and read them all into a single pandas dataframe
    input_files = [os.path.join(args.train, file) for file in os.listdir(args.train)]
    if len(input_files) == 0:
        raise ValueError(('There are no files in {}.\n' +
                          'This usually indicates that the channel ({}) was incorrectly specified,\n' +
                          'the data specification in S3 was incorrectly specified or the role specified\n' +
                          'does not have permission to access the data.').format(args.train, "train"))
        
    # based on our save dataset, we have header, and target column name = 'is_fraud'
    raw_data = [pd.read_csv(file, header=0, engine="python") for file in input_files]
    train_data = pd.concat(raw_data)
    target_col = 'is_fraud'
    X_train = train_data.drop([target_col], axis=1)
    y_train = train_data.loc[:, target_col]

    # get the hyperparameters passing through the script
    n_estimators = args.n_estimators
    max_depth = args.max_depth
    verbose = args.verbose
    random_state = args.random_state
    n_jobs = -1
    
    clf = RandomForestClassifier(
        n_estimators=n_estimators,
        max_depth=max_depth,
        verbose=verbose,
        random_state=random_state,
        n_jobs=n_jobs
    )
    clf = clf.fit(X_train, y_train)

    # Print the coefficients of the trained classifier, and save the coefficients
    joblib.dump(clf, os.path.join(args.model_dir, "model.joblib"))


def model_fn(model_dir):
    """Deserialized and return fitted model

    Note that this should have the same name as the serialized model in the main method
    """
    clf = joblib.load(os.path.join(model_dir, "model.joblib"))
    return clf
```

Setting up `SKLearn` estimator and train the model
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/acfe84aef0b8168eed8ce1a53f35ece4edd47cac/img/skl-estimator-train.png" height=400>

Model deployment - this is similar with **XGBoost** step
<img src="https://github.com/netsatsawat/fraud-detection-using-aws-cloud/blob/acfe84aef0b8168eed8ce1a53f35ece4edd47cac/img/skl-estimator-deploy.png" width=800>
