## Quickstart

### Step 1: Install the data package in your DISPATCHES environment using pip

```sh
conda activate dispatches-dev  # or the name of your DISPATCHES dev environment
pip install git+https://github.com/gmlc-dispatches/steady-state-sweep-data
```

### Step 2: Access the contents of the data package in your code using `dispatches_data.api`

Using `dispatches_data.api.path()`:

```py
from dispatches_data.api import path

# path_to_data_package is a standard pathlib.Path object
path_to_data_package = path("steady_state_sweep")

# subdirectories and files can be accessed using the pathlib.Path API
inputs_path = path_to_data_package / "prescient_generator_inputs.h5"
assert inputs_path.is_file()

# alternatively, if the file is located directly under the data package directory (i.e. not in a subdirectory):
# this will raise an exception if the file does not exist so we don't need to check explicitly
inputs_path = path("steady_state_sweep", "prescient_generator_inputs.h5")

# if the path must be passed to a function that only accepts `str` objects, it can be converted using `str()`
inputs_path_as_str = str(inputs_path)
```

Using `dispatches_data.api.files()`:

```py
from dispatches_data.api import files

# `h5_files_paths` will be a list of pathlib.Path objects for each file matching the specified `pattern`
h5_files_paths = files("steady_state_sweep", pattern="**/*.h5")
# check that the list of found files is not empty
assert h5_files_paths

# `dispatches_data.api.files()` always returns a list, even if only one file matches
outputs_file_path = files("steady_state_sweep", pattern="**/*_outputs.h5")[0]
```

## Examples

Check the other data packages repositories for additional examples and other resources:

- [gmlc-dispatches/data-packages](https://github.com/gmlc-dispatches/data-packages)
- The [dispatches-data-package](https://github.com/topics/dispatches-data-package) topic on GitHub
