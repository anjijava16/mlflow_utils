# Python Function (python_function)

The python_function model flavor serves as a default model interface for MLflow Python models. Any MLflow Python model is expected to be loadable as a python_function model. This enables other MLflow tools to work with any python model regardless of which persistence module or framework was used to produce the model. This interoperability is very powerful because it allows any Python model to be productionized in a variety of environments.

In addition, the python_function model flavor defines a generic filesystem model format for Python models and provides utilities for saving and loading models to and from this format. The format is self-contained in the sense that it includes all the information necessary to load and use a model. Dependencies are stored either directly with the model or referenced via conda environment. This model format allows other tools to integrate their models with MLflow.

# How To Save Model As Python Function
1. Most python_function models are saved as part of other model flavors - for example, all mlflow built-in flavors include the python_function flavor in the exported models. In addition, the mlflow.pyfunc module defines functions for creating python_function models explicitly. This module also includes utilities for creating custom Python models, which is a convenient way of adding custom python code to ML models. For more information, see the custom Python models documentation.

# How To Load And Score Python Function Models
1. You can load python_function models in Python by calling the mlflow.pyfunc.load_model() function. Note that the load_model function assumes that all dependencies are already available and will not check nor install any dependencies ( see model deployment section for tools to deploy models with automatic dependency management).

Once loaded, you can score the model by calling the predict method, which has the following signature:


## predict(model_input: [pandas.DataFrame, numpy.ndarray, Dict[str, np.ndarray]]) -> [numpy.ndarray | pandas.(Series | DataFrame)]

All PyFunc models will support pandas.DataFrame as an input. In addition to pandas.DataFrame, DL PyFunc models will also support tensor inputs in the form of numpy.ndarrays. To verify whether a model flavor supports tensor inputs, please check the flavor’s documentation.


For models with a column-based schema, inputs are typically provided in the form of a pandas.DataFrame. If a dictionary mapping column name to values is provided as input for schemas with named columns or if a python List or a numpy.ndarray is provided as input for schemas with unnamed columns, MLflow will cast the input to a DataFrame. Schema enforcement and casting with respect to the expected data types is performed against the DataFrame.


For models with a tensor-based schema, inputs are typically provided in the form of a numpy.ndarray or a dictionary mapping the tensor name to its np.ndarray value. Schema enforcement will check the provided input’s shape and type against the shape and type specified in the model’s schema and throw an error if they do not match.


For models where no schema is defined, no changes to the model inputs and outputs are made. MLflow will propagate any errors raised by the model if the model does not accept the provided input type.


The python environment that a PyFunc model is loaded into for prediction or inference may differ from the environment in which it was trained. In the case of an environment mismatch, a warning message will be printed when calling mlflow.pyfunc.load_model(). This warning statement will identify the packages that have a version mismatch between those used during training and the current environment. In order to get the full dependencies of the environment in which the model was trained, you can call mlflow.pyfunc.get_model_dependencies(). Furthermore, if you want to run model inference in the same environment used in model training, you can call mlflow.pyfunc.spark_udf() with the env_manager argument set as “conda”. This will generate the environment from the conda.yaml file, ensuring that the python UDF will execute with the exact package versions that were used during training.

