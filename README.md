# radMLBench

This is a large collection of radiomic datasets, accessible via Python.


## Installing radMLBench

Install it via pip:

```
pip install radMLBench
```


## Datasets

All data sets are stored in a common format:

* First row is the column names
* Each following row corresponds to one row of the data
* The ID column is named `ID` (in case the original data did not supply IDs, these are simple numbers)
* The target column is named `Target`, always binary (=0,1)
* All files are compressed with `gzip` to conserve space


The complete list of datasets is

<!-- dataset table:start -->

| Dataset                     |   Year | Modality   |   #Instances |   #Features |   Dimensionality |   ClassBalance | DOI                                          |
|:----------------------------|-------:|:-----------|-------------:|------------:|-----------------:|---------------:|:---------------------------------------------|
| LGG-1p19qDeletion           |   2017 | MRI        |          159 |        2030 |            12.78 |             64 | https://doi.org/10.1007/s10278-017-9984-3    |
| UPENN-GBM                   |   2022 | MRI        |          187 |       11165 |            59.72 |             42 | https://doi.org/10.1038/s41597-022-01560-7   |
| WORC-GIST                   |   2021 | CT         |          245 |        1015 |             4.15 |             51 | https://doi.org/10.48550/arXiv.2108.08618    |
<!-- dataset table:end -->


## Python wrapper

For easy access to the benchmark data sets, we have provided a Python wrapper named `radMLBench`. The wrapper can be installed on Python via `pip`:

```
pip install radMLBench
```

and used in Python scripts as follows:

```python
from radMLBench import listDatasets, getMetaData, loadData

for dataset in radMLBench.listDatasets():
  print (f"Loading {dataset}")
  data = radMLBench.loadData(dataset)
  print (data.shape)
```

There is a simple example on how to use it in combination with a random forest
classifier in `./examples/simpleTest.py`.

Ideally, one should download the data to a local directory so that
downloading from the internet is minimized for speed reaons. To do so,
just use the `local_cache_dir` variable:

``` data = radMLBench.loadData("Wang2024", local_cache_dir="~/radMLBench.repo") ```

In case you want to load the data not as a dataframe (where ID and Target columns
exist), but as a ready-to-use numpy dataset, just add the parameter `return_X_y`.
This will convert the pandas dataframe into two numpy arrays X, and y. X will
contain the data and y the labels.

``` data = radMLBench.loadData("Wang2024", local_cache_dir="~/radMLBench.repo", return_X_y = True) ```



## Experiments

The decorrelation example can be found in `examples/decorrelation`,
to execute it, start `./examples/decorrelation/decorrelation.py`.

**NOTE**: Due to size problems, it is not possible to upload the .csv result files to github for the time being. Thus, to recreate the results, please rerun the experiment.
 

The other example, TabFPN, can be found in `examples/tebpfn`.
However, before executing this, one must install TabFPN (which in turn
will install things like torch). One must also execute TabFPN once
before  executing the script, since TabFPN must first download the model--
but this will not work if multiple TabFPN instances try it at the same time.
Therefore, one must first (with a single CPU core) execute TabFPN.
One can achieve this by setting downloadFirst to True in the script.
After executing the script (which will just download and exit), one can
put downloadFirst to False again to execute the experiment.



## Citing radMLBench

If you use radMLBench in a scientific publication, please consider citing the paper:

Aydin Demircioglu.  
[radMLBench: A radiomics dataset collection for benchmarking in radiomics](https://doi.org/10.1016/j.compbiomed.2024.109140).  
_Computers in Biology and Medicine_, Volume 182, 2024, 109140.  
ISSN 0010-4825.
