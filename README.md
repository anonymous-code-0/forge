# Anonymisation of the forge repo. Only use for review purposes.

# Forge
A lightweight tool for managing ML experiments.

Forge makes it easier to configure experiments and allows easier model inspection and evaluation due to smart checkpoints. With Forge, you can configure and build your dataset and model in separate files and load them easily in an experiment script or a jupyter notebook. Once the model is trained, it can be easily restored from a snapshot (with the corresponding dataset) without the access to the original config files.

## Config files and scripts
Dataset and model config files are general (separate) python scripts that define a `load` function. Dataset should return a `dict`, which is passed as keyword arguments to the model config.  

Both config files and any scripts use `forge.flags` for configuration. They are based on an older implementation of [abseil](https://github.com/abseil/abseil-py/tree/master/absl/flags). Forge does not take Tensorflow flags into account, so it's best to use `forge.flags` instead.

## Model Checkpoints
The training script relies on `checkpoint_dir` and `run_name` flags, that specify where model checkpoints should be kept. For every run, a job-specific folder is created under `checkpoint_dir/run_name/#`, where `#` is a number. All config flags and dataset/model config are stored in a job folder, so that the corresponding job can be easily resumed later by passing the `resume` flag.

