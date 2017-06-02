# dedupe-dcp

This is an experiment in using the dedupe package to flag duplicate records in data managed by the Capital Planning team. For more information on the package, [view the docs](https://dedupe.io/developers/library/en/latest/) or the [package repo](https://github.com/dedupeio/dedupe). There is also a repo with [usage examples](https://github.com/dedupeio/dedupe-examples). These examples were modified and tested on the Facilities Database.

### Setup

Initial tests to use the package using Python 2.7x failed. The deduping script ran successfully in a Python 3.5 environment. If using Anaconda, check out https://conda.io/docs/using/envs.html for info on how to use different Python environments.

If working in a new Python 3.5 environment, you may be prompted to install several dependencies (e.g. Numpy).

#### Defining fields for comparison

The fields to be used in the deduping algorithm are defined as a list of dictionaries. A list of available field comparator types is [here](https://dedupe.io/documentation/types-of-field-comparators.html). Full details on these types and how to define them are [here](https://dedupe.io/developers/library/en/latest/Variable-definition.html).

These field are defined in the main deduping script (e.g. `dedupe_csv.py` for CSV data).

### For CSV files

_Note: Comments in the example code claim that the script will run very quickly on datasets up to 10K rows. However, in testing, errors were being generated on data larger than ~4K rows. This number could be even smaller depending on the number of fields that are defined for comparison. It is also specific to the machine being used._

Use the `dedupe_csv.py` script in the `/csv` folder. Modify the input and output variables as necessary. When in the `/csv` directory, run the script using 

`python dedupe_csv.py`

If the `learned_settings` file does not exist, then you will be prompted to create a small training dataset via the command line. This training data is then used to run the deduping algorithm on a subset of the full dataset, and a `learned_settings` file is generated. If the file already exists, then the script jumps directly to labeling each record in the dataset with a Cluster ID. If records have the same Cluster ID, dedupe thinks they are duplicates. The output file also includes a confidence score column containing the relative likelihood that a record identified as a duplicate is actually a duplicate.

### For PostrgreSQL databases (larger data)

