
<p align="center">
  <img src="https://github.com/HKQiu/DataAugmentation4SmallData/assets/73220956/d7a243ed-6cd8-42e2-92c3-56a33f4d3c84" width="50%">
</p>



# DAGNN for PIs
This is the 2nd part of project PPP-Prediction Properties of Polymers from Sun's AI4P Workshop.
**All data and code** about model training and polyScreen software are in this repository.
The data used to train the models mentioned in this work can be found at /model, and the weights of the optimal model can also be found. 
In addition, the related code and the toolkit – **polyScreen2** are also open source at /polyScreen2.


# *polyScreen2*

## Hard requirements
These packages must be available to use polyScreen2:
```
  	python=3.9
  	numpy=1.24.3=pypi_0
  	pandas=2.0.1=pypi_0
  	deepchem=2.6.1=pypi_0
  	tensorflow=2.10.0=pypi_0
  	tensorflow-estimator=2.10.0=pypi_0
  	scikit-learn=1.2.2=pypi_0
  	joblib=1.2.0=pypi_0
```

## Tutorials
An example of property prediction by calling the model is given here: (Don't want to code? Just skip this part and read the following part.)
```python
import glob,os
import pandas as pd
import deepchem as dc
import numpy as np
from rdkit import Chem
from rdkit.Chem import AllChem
from rdkit.Chem import Draw, PyMol, rdFMCS
from rdkit.Chem.Draw import IPythonConsole
from rdkit import rdBase
from deepchem import metrics
from IPython.display import Image, display
from rdkit.Chem.Draw import SimilarityMaps
import tensorflow as tf

Val_DATASET_FILE = 'Path/2/your/file.csv'			# .csv
Restore_MODEL_DIR = ' Path/2/model'
#####Featurizerization#######
featurizer = dc.feat.ConvMolFeaturizer()
loader = dc.data.CSVLoader(tasks=[], feature_field="Smiles", featurizer=featurizer)
testset = loader.create_dataset(Val_DATASET_FILE, shard_size=10000)
###########Model##############
model = dc.models.GraphConvModel(1, mode="regression", model_dir=Restore_MODEL_DIR)
model.restore()
############Predict#############
val_pred = model.predict(testset)
```

It is <span style="color:blue">convenient</span> to make predictions and conduct structure design directly using <span style="color:red">polyScreen2</span> by simply downloading this repository and:

```
cd DataAugmentation4SmallData/polyScreen2
python polyScreen2.py
```
The GUI of polyScreen2 is now in your display as follows. One can find the .gif demo at our repo. to help for the usage.

<p align="center">
  <img src="https://github.com/HKQiu/DataAugmentation4SmallData/assets/73220956/bbfc3326-f71c-457b-b189-159943c3e34d" width="30%">
</p>

Any issue on the usage of **polyScreen2**, please email [hkqiu@ciac.ac.cn](hkqiu@ciac.ac.cn).
