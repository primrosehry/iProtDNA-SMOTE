# iProtDNA-SMOTE
Pytorch implementation of paper 'iProtDNA-SMOTE: Enhancing Protein-DNA Binding Site Prediction through Imbalanced Graph Neural Networks' 

## Dependencies
- python 3.8
- pytorch 1.11.0
- torchvision 0.12.0
- numpy

## Repo for iProtDNA-SMOTE framework
This repo holds the code of iProtDNA-SMOTE framework for protein-ligands binding sites prediction. Five processed datasets are published, including TR646, TR573, TE46, TE129, and TE181.

iProtDNA-SMOTE is primarily dependent on a large-scale pre-trained protein language model ESM2 implemented using PyTorch. Please install the dependencies in advance.

## Files and folders description
### 1. Raw_data
This folder contains raw data. The first line is the protein id (which might not be PDB ID); the second line is the protein sequence, and the third line is the data label indicating binding sites or non-binding sites.

Note: if you wanna find the original data in PDB format, please kindly refer to the following 3 papers: DBPred, GraphBind, and GraphSite.

### 2. Graph_46
This folder contains the graph model for dataset TE46, where each node represents an amino acid residue. The node features are embeddings generated by ESM2. Distances between nodes are determined by the protein's three-dimensional structure, with a spatial distance threshold of 8 angstroms. If the distance between the Cα atoms of two residues is below this threshold, they are connected by an edge in the graph model.

The original pt file was too large, so we split it and you can use follow commands to merge them: 

```
Path\to\your\file>PowerShell -ExecutionPolicy Bypass -File E:\youfile\Graph_46\Merge-Files.ps1
```

### 3. Weights
This folder contains trained weight files. Specifically, 646_46.pt corresponds to the trained model for task TR646, suitable for testing the TE46 dataset. 573_129.pt represents the trained model for task TR573, applicable for testing the TE129 dataset. Lastly, 573_181.pt denotes another trained model for task TR573, intended for testing the TE181 dataset.

## Codes description
The training and implementation of this project are based on PyTorch 1.11.0 and PyTorch-lightning 2.0.3, the higher version might not be compatible. 

### 1. model.py
Implementation of backbone models such as Graphsage, MLP.

### 2. utils.py
Implementation of data preprocessing, GraphSMOTE, and Focal Loss. 

### 3. main.py
Implementation of model training. Here we provide a sample file, and please use iProtDNA-SMOTE as following commands:

```
python main.py --input 646.pt --output 646_46.pt --test.py
```

### 4. test.py
Implementation of independent testing of the model. Here we provide a sample file, and please use iProtDNA-SMOTE as following commands:

```
python test.py --input 646_46.pt, 46.pt --output result
```

## Citation
If any problems occur via running this code, please contact us at 2220641288@qq.com.

Thank you!
