### EEND (End-to-End Neural Diarization)
EEND (End-to-End Neural Diarization) is a neural-network-based speaker diarization method.


## Getting started
We recommend to create [anaconda](https://www.anaconda.com/) environment
```bash
conda create -n EEND python=3.6
conda activate EEND
```
Clone the repository
```bash
git clone https://github.com/Sangramsingkayte/End-to-End-Neural-Diarization.git
```
## Install tools
### Requirements
 - NVIDIA CUDA GPU
 - CUDA Toolkit (8.0 <= version <= 10.1)
 - 
### Install kaldi and python environment
```bash
cd tools
make
```
- This command builds kaldi at `tools/kaldi`
  - if you want to use pre-build kaldi
    ```bash
    cd tools
    make KALDI=<existing_kaldi_root>
    ```
    This option make a symlink at `tools/kaldi`
- This command extracts miniconda3 at `tools/miniconda3`, and creates conda envirionment named 'eend'
- Then, installs Chainer and cupy into 'eend' environment
  - use CUDA in `/usr/local/cuda/`
    - if you need to specify your CUDA path
      ```bash
      cd tools
      make CUDA_PATH=/your/path/to/cuda-8.0
      ```
      This command installs cupy-cudaXX according to your CUDA version.
      See https://docs-cupy.chainer.org/en/stable/install.html#install-cupy

## CALLHOME two-speaker experiment
### Configuraition
- Modify `egs/callhome/v1/cmd.sh` according to your job schedular.
If you use your local machine, use "run.pl".
If you use Grid Engine, use "queue.pl"
If you use SLURM, use "slurm.pl".
For more information about cmd.sh see http://kaldi-asr.org/doc/queue.html.
- Modify `egs/callhome/v1/run_prepare_shared.sh` according to storage paths of your corpora.

### Data preparation
```bash
cd egs/callhome/v1
./run_prepare_shared.sh
# If you want to conduct 1-4 speaker experiments, run below.
# You also have to set paths to your corpora properly.
./run_prepare_shared_eda.sh
```
### Self-attention-based model using 2-speaker mixtures
```bash
./run.sh
```
### BLSTM-based model using 2-speaker mixtures
```bash
local/run_blstm.sh
```
### Self-attention-based model with EDA using 1-4-speaker mixtures
```bash
./run_eda.sh
```

## References
- BLSTM EEND (INTERSPEECH 2019)
  - https://www.isca-speech.org/archive/Interspeech_2019/abstracts/2899.html
- Self-attentive EEND (ASRU 2019)
  - https://ieeexplore.ieee.org/abstract/document/9003959/

The EEND extension for various number of speakers is also provided in this repository.
- Self-attentive EEND with encoder-decoder based attractors
  - https://arxiv.org/abs/2005.09921
 
