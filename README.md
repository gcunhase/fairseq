# Introduction <img src="fairseq_logo.png" width="50"> 

Fairseq(-py) is a sequence modeling toolkit that allows researchers and
developers to train custom models for translation, summarization, language
modeling and other text generation tasks. It provides reference implementations
of various sequence-to-sequence models, including:
- **Convolutional Neural Networks (CNN)**
  - [Dauphin et al. (2017): Language Modeling with Gated Convolutional Networks](https://arxiv.org/abs/1612.08083)
  - [Gehring et al. (2017): Convolutional Sequence to Sequence Learning](https://arxiv.org/abs/1705.03122)
  - [Edunov et al. (2018): Classical Structured Prediction Losses for Sequence to Sequence Learning](https://arxiv.org/abs/1711.04956)
  - [Fan et al. (2018): Hierarchical Neural Story Generation](https://arxiv.org/abs/1805.04833)
- **LightConv and DynamicConv models**
  - **_New_** [Wu et al. (2019): Pay Less Attention with Lightweight and Dynamic Convolutions](https://openreview.net/pdf?id=SkVhlh09tX)
- **Long Short-Term Memory (LSTM) networks**
  - [Luong et al. (2015): Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025)
  - [Wiseman and Rush (2016): Sequence-to-Sequence Learning as Beam-Search Optimization](https://arxiv.org/abs/1606.02960)
- **Transformer (self-attention) networks**
  - [Vaswani et al. (2017): Attention Is All You Need](https://arxiv.org/abs/1706.03762)
  - [Ott et al. (2018): Scaling Neural Machine Translation](https://arxiv.org/abs/1806.00187)
  - [Edunov et al. (2018): Understanding Back-Translation at Scale](https://arxiv.org/abs/1808.09381)

Fairseq features:
- multi-GPU (distributed) training on one machine or across multiple machines
- fast generation on both CPU and GPU with multiple search algorithms implemented:
  - beam search
  - Diverse Beam Search ([Vijayakumar et al., 2016](https://arxiv.org/abs/1610.02424))
  - sampling (unconstrained and top-k)
- large mini-batch training even on a single GPU via delayed updates
- fast half-precision floating point (FP16) training
- extensible: easily register new models, criterions, tasks, optimizers and learning rate schedulers

We also provide [pre-trained models](#pre-trained-models-and-examples) for several benchmark
translation and language modeling datasets.

![Model](fairseq.gif)

# Requirements and Installation
* A [PyTorch installation](http://pytorch.org/)
* For training new models, you'll also need an NVIDIA GPU and [NCCL](https://github.com/NVIDIA/nccl)
  * For CUDA 9.0, [download NCCL](https://developer.nvidia.com/nccl/nccl2-download-survey) and follow [link](https://docs.nvidia.com/deeplearning/sdk/nccl-install-guide/index.html)
  ```
  sudo dpkg -i nccl-repo-<version>.deb
  sudo apt update
  sudo apt install libnccl2 libnccl-dev
  ```
  * Else:
  ```
  sudo apt install libnccl2=2.0.0-1+cuda8.0 libnccl-dev=2.0.0-1+cuda8.0
  ```
* Python version 3.6
  ```
  apt-get install software-properties-common python-software-properties
  add-apt-repository ppa:jonathonf/python-3.6
  apt-get update
  apt-get install python3.6
  python3.6 -V
  ```
Currently fairseq requires PyTorch version >= 1.0.0.
Please follow the instructions here: https://github.com/pytorch/pytorch#installation.

If you use Docker make sure to increase the shared memory size either with
`--ipc=host` or `--shm-size` as command line options to `nvidia-docker run`.

After PyTorch is installed, you can install fairseq with:
```
pip install -r requirements.txt
python setup.py build develop
```

# Getting Started

The [full documentation](https://fairseq.readthedocs.io/) contains instructions
for getting started, training new models and extending fairseq with new model
types and tasks.

# Pre-trained models and examples

We provide pre-trained models and pre-processed, binarized test sets for several tasks listed below,
as well as example training and evaluation commands.

- [Translation](examples/translation/README.md): convolutional and transformer models are available
- [Language Modeling](examples/language_model/README.md): convolutional models are available

We also have more detailed READMEs to reproduce results from specific papers:
- [Wu et al. (2019): Pay Less Attention with Lightweight and Dynamic Convolutions](examples/pay_less_attention_paper/README.md)
- [Edunov et al. (2018): Classical Structured Prediction Losses for Sequence to Sequence Learning](https://github.com/pytorch/fairseq/tree/classic_seqlevel)
- [Fan et al. (2018): Hierarchical Neural Story Generation](examples/stories/README.md)
- [Ott et al. (2018): Scaling Neural Machine Translation](examples/scaling_nmt/README.md)
- [Gehring et al. (2017): Convolutional Sequence to Sequence Learning](examples/conv_seq2seq/README.md)
- [Dauphin et al. (2017): Language Modeling with Gated Convolutional Networks](examples/conv_lm/README.md)

# Join the fairseq community

* Facebook page: https://www.facebook.com/groups/fairseq.users
* Google group: https://groups.google.com/forum/#!forum/fairseq-users

# License
fairseq(-py) is BSD-licensed.
The license applies to the pre-trained models as well.
We also provide an additional patent grant.

# Credits
This is a PyTorch version of
[fairseq](https://github.com/facebookresearch/fairseq), a sequence-to-sequence
learning toolkit from Facebook AI Research. The original authors of this
reimplementation are (in no particular order) Sergey Edunov, Myle Ott, and Sam
Gross.
