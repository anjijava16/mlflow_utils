# mlflow_utils

# MLFlow 

1. https://www.databricks.com/product/managed-mlflow
2. https://mlserver.readthedocs.io/en/latest/index.html#
3. https://mlflow.org/docs/latest/models.html#input-example


# How to run MlFLow

pip install mlflow

mlflow ui

http://127.0.0.1:5000/#/


# Model API
You can save and load MLflow Models in multiple ways. First, MLflow includes integrations with several common libraries. For example, mlflow.sklearn contains save_model, log_model, and load_model functions for scikit-learn models. Second, you can use the mlflow.models.Model class to create and write models. This class has four key functions:

add_flavor to add a flavor to the model. Each flavor has a string name and a dictionary of key-value attributes, where the values can be any object that can be serialized to YAML.

1. save to save the model to a local directory.

2. log to log the model as an artifact in the current run using MLflow Tracking.

3. load to load a model from a local directory or from an artifact in a previous run.




Examples¶
To see MLServer in action, check out our full list of examples. You can find below a few selected examples showcasing how you can leverage MLServer to start serving your machine learning models.

Serving a scikit-learn model

Serving a xgboost model

Serving a lightgbm model

Serving a tempo pipeline

Serving a custom model

Serving an alibi-detect model

Serving a HuggingFace model

Multi-Model Serving with multiple frameworks

Loading / unloading models from a model repository

https://mlserver.readthedocs.io/en/latest/index.html#examples
