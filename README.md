# KGRA

![ ](KGRA.jpg)

**This is the data and code for our paper** `KGRA: a knowledge graph relational attention model for drug repurposing`.

The development of new drugs is costly and time-consuming. Drug repurposing has gained popularity as an efficient and low-risk approach to find new therapeutic options by using drugs that have already been broadened to treat new diseases. Recently, knowledge graph-based methods have been used for drug repurposing. These models predict new drug-disease relations by learning low-dimensional embeddings of entities and relationships. Among them, the graph attention network (GAT) and graph convolutional network (GCN) can generate richer and more expressive feature embeddings, so they performs well in relation prediction. However, most graph neural networks ignore relationship information and complex relationship combination information, so they are not suitable for direct use in knowledge graphs. Moreover, the presence of noise during the training process of knowledge graph embedding will have an impact on the optimization of model parameters. In our work, we propose a knowledge graph relational multi-head attention network with denoising for drug repurposing, called KGRA. Firstly, the knowledge graph relational multi-head attention network (KGRMA) is proposed to combine the attention scores of context triples and aggregated messages. The KGRMA fully learns the semantic information of neighboring entities and relations, enhancing the representation ability of entity embedding. Then, the InteractE module is used as the decoder to obtain heterogeneous feature interactions in entity and relation representations. Finally, knowledge weighted loss is introduced to reduce the impact of noise on model training. Experiments on three datasets show that the model is superior to the existing knowledge graph embedding (KGE) and graph neural network methods.

## Prerequirements
* `Python(version >= 3.6)`
* `pytorch(version>=1.4.0)`
*  `ordered_set(version>=3.1)`
* `pytorch>=1.7.1 & <=1.9`
* `numpy(version>=1.16.2)`
* `torch_scatter(version>=2.0.4)`
* `scikit_learn(version>=0.21.1)`
* `torch-geometric`
  
We highly recommend you to use conda for package management.

## Datastes

We provide the dataset in the [data](data/) folder.

- [GP-KG](data/GP-KG/)
- [OpenBioLink](data/OpenBioLink/)
- [Biokg](data/Biokg/)

## Repository structure

The current repository is structured in the following way:
```
|-- KGRA.jpg
|-- README.md
|-- main.py
|-- test.py
|-- config
|   |-- log_config.json
|-- data (Data folder)
|   |-- GP-KG
|   |-- OpenBiolink
|   `-- Biokg
`-- model
    |-- KGRMA.py
    |-- data_loader.py
    |-- message_passing.py
    |-- predict.py
    |-- tool.py
```

## Model

The basic structure of our model an be found in [model](model/) folder.
The model can be divided into 4 parts, data loading, KGRMA module, KWL module and InteractE decoder. They can be used in file [`data_loader.py`](model/data_loader.py), [`KGRMA.py`](model/KGRMA.py) and [`predict.py`](model/predict.py).

Training:
Training-related utilities can be found in [`main.py`](main.py). They accept `Iterator`'s that yield batched data,
identical to the output of a `torch.utils.data.DataLoader`. Use the following command to train the model, the model will be named as "test_model" and saved in the directory "model_saved".
  python main.py -data test_data -gpu 1 -name test_model -epoch 500


Drug-Disease Predicting:
Test-related utilities can be found in [`test.py`](test.py). Create a test file named as "drug_pre.txt" and moved the file to the folder "test_data". Run the following command, predicting results will be saved in the file "results.txt".
```
             python test.py -data test_data -gpu 1 -name test_model -save_result drug_pre.txt -test_data result.txt
```

Parameter Note:
-data the directory of training and testing data
-gpu the GPU to use
-name the name of the model snapshot (used for storing model parameters)
-epoch the number of epochs
-save_result the filename that is used to store test results
-test_file the name of testing file


