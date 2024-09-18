
In this work we introduce new sparse dynamic transformers for graph data, and use them in the [GraphGPS](https://github.com/rampasek/GraphGPS) framework. Our sparse transformer has three components: actual edges, expander graphs, and universal connectors or virtual nodes. We combine these components into a single sparse attention mechanism.


### Python environment setup with Conda

```bash
conda create -n exphormer python=3.9
conda activate exphormer

conda install pytorch=1.10 torchvision torchaudio -c pytorch -c nvidia
conda install pyg=2.0.4 -c pyg -c conda-forge

# RDKit is required for OGB-LSC PCQM4Mv2 and datasets derived from it.  
conda install openbabel fsspec rdkit -c conda-forge

pip install torchmetrics
pip install performer-pytorch
pip install ogb
pip install tensorboardX
pip install wandb

conda clean --all
```


### Running 
```bash
conda activate exphormer

# Running Exphormer for LRGB Datasets
python main.py --cfg configs/Exphormer_LRGB/peptides-struct-EX.yaml  wandb.use False

# Running Exphormer for Cifar10
python main.py --cfg configs/Exphormer/cifar10.yaml  wandb.use False
```
You can also set your wandb settings and use wandb.

### Guide on configs files

Most of the configs are shared with [GraphGPS](https://github.com/rampasek/GraphGPS) code. You can change the following parameters in the config files for different parameters and variants of the Exphormer:
```
prep:
  exp: True  # Set True for using expander graphs, set False otherwise. 
    # Alternatively you can set use_exp_edges to False.
    # In this case expander graphs will be calculated but not used in the Exphormer. 
  exp_deg: 5 # Set the degree of the expander graph.
    # Please note that if you set this to d, the algorithm will use d permutations 
    # or d Hamiltonian cycles, so the actual degree of the expander graph will be 2d
  exp_algorithm: 'Random-d' # Options are ['Random-d', 'Random-d2', 'Hamiltonian].
    # Default value is 'Random-d'
  add_edge_index: True # Set True if you want to add real edges beside expander edges
  num_virt_node: 1 # Set 0 for not using virtual nodes 
    # otherwise set the number of virtual nodes you want to use.
```

