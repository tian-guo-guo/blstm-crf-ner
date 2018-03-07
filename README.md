# blstm-crf-ner

A NER model (B-LSTM + CRF + word embeddings) implemented using *Tensorflow* which is used to tag **Turkish noisy data** (tweets specifically!) without using any hand-crafted features or rules. 

The model is very similar to [Lample et al.](https://arxiv.org/abs/1603.01360), [Gungor, Onur et al.](https://arxiv.org/pdf/1706.00506.pdf) and [Ma and Hovy](https://arxiv.org/pdf/1603.01354.pdf). As a consequence, the source code is also heavily influenced by Guillaume Genthial's [sequence_tagging](https://github.com/guillaumegenthial/sequence_tagging) and Guillaume Lample's [tagger](https://github.com/glample/tagger) projects. 

## Getting started

1. Download the GloVe vectors with

```
make glove
```

Alternatively, you can download them manually [here](https://nlp.stanford.edu/projects/glove/) and update the `glove_filename` entry in `config.py`. You can also choose not to load pretrained word vectors by changing the entry `use_pretrained` to `False` in `model/config.py`.

2. Build the training data, train and evaluate the model with
```
make run
```

## Details

Here is the breakdown of the commands executed in `make run`:

1. Build vocab from the data and extract trimmed glove vectors according to the config in `model/config.py`.

```
python build_data.py
```

2. Train the model with

```
python train.py
```


3. Evaluate and interact with the model with

```
python evaluate.py
```

Data iterators and utils are in `model/data_utils.py` and the model with training/test procedures is in `model/ner_model.py`

## Training Data

The training data must be in the following format (identical to the CoNLL2003 dataset).

A default test file is provided to help you getting started.

```
John B-PER
lives O
in O
New B-LOC
York I-LOC
. O

This O
is O
another O
sentence
```

Once you have produced your data files, change the parameters in `config.py` like

```
# dataset
filename_dev = "data/tr.testa.iobes"
filename_test = "data/tr.testb.iobes"
filename_train = "data/tr.train.iobes"
```

## License

This project is licensed under the terms of the apache 2.0 license (as Tensorflow and derivatives). If used for research, citation would be appreciated.

