# Fine-Tuning via Linked Domains: A Closed-Form Dual Alignment Mechanism for Transferring Vision-Language Models
## Approach
![main figure](images/main_figure.png)
> **<p align="justify"> Abstract:** *Adapters and prompt learning methods have become common strategies to fine-tune pre-trained vision-language models, mitigating the high computational cost of fine-tuning the entire model for downstream tasks. However, these strategies primarily focus on aligning the predictions from the fine-tuned model with those from the pre-trained model within a single modality, \textcolor{red}{neglecting the interaction between different modalities}. \textcolor{blue}{However, these strategies primarily focus on aligning the fine-tuned model's predictions with those of the pre-trained model within a single modality or on unidirectional cross-modal alignment, while overlooking the interactions between different modalities.} To address this issue, we propose a closed-form dual alignment mechanism (DAM) that {\it not only ensures the consistency in predictions within a single modality but also achieves the alignment of features across different modalities}. In DAM, all alignments are achieved by ridge regression with closed-form solutions, significantly reducing the computational burden. Experimental results demonstrate that DAM outperforms the state-of-the-art methods on 11 benchmarks over various evaluation metrics.* </p>

## Contributions
- We propose a Dual Alignment Mechanism (DAM) that combines same-modal alignment and cross-modal alignment strategies, enhancing cross-modal information transfer and utilization while preventing overfitting, and addressing the issue of insufficient cross-modal alignment in existing methods.
- We design a robust cross-modal alignment technique that ensures comprehensive feature alignment by calculating Euclidean distances from text to image embeddings and from image to text embeddings.
- We have designed a parameter-efficient intra-modal alignment technique that aligns prompt features with pre-trained features to achieve precise feature matching. Additionally, we introduced an intra-modal alignment loss to ensure the consistency between the fine-tuned model and the pre-trained model.
- We achieve optimal same-modal and cross-modal alignment by solving a ridge regression problem, ensuring stable and effective feature transformation.

## Installation
```bash
# Create a conda environment
conda create -n dam python=3.8

# Activate the environment
conda activate dam

# Install torch (requires version >= 1.8.1) and torchvision
# Please refer to https://pytorch.org/ if you need a different cuda version
pip install torch==1.10.1+cu111 torchvision==0.11.2+cu111 torchaudio==0.10.1 -f https://download.pytorch.org/whl/cu111/torch_stable.html

# Clone this repo
git clone https://github.com/KaiyangZhou/Dassl.pytorch.git
cd Dassl.pytorch/

# Install dependencies
pip install -r requirements.txt

# Install this library (no need to re-build if the source code is modified)
python setup.py develop
cd ..

git clone https://github.com/Peiy-Lu/DAM-main.git

cd DAM-main/

# Install requirements
pip install -r requirements.txt
```

## Datasets
For datasets, please follow the CoOp instructions here: [DATASETS.md](https://github.com/KaiyangZhou/CoOp/blob/main/DATASETS.md).

## How to Run
We have designed execution scripts for each task to help you reproduce the results of our paper.

### Base-to-New Generalization
First, you need to set the DATA variable in the `./scripts/b2n_train.sh` and `./scripts/b2n_test.sh` files to your dataset path.

For convenience, we have included all three seeds for each dataset in a single script file named b2n_all.sh. You can reproduce our results by simply running the following code:
```bash
bash ./scripts/b2n_all.sh
```
If you need to reproduce results for a single dataset, seed, or shot, you can simply run the script as follows:
- Train and Test on Base Classes: `bash scripts/b2n_train.sh dataset seed shot gpu`
- Test on New Classes：`bash scripts/b2n_test.sh dataset seed shot gpu`

### Domain Generalization & Cross-dataset Evaluation
Similarly, we provide a script named `./scripts/xd_all.sh` for Domain Generalization and Cross-dataset Evaluation, which enables the training and testing of all datasets with three seeds in a single run.

If you need to reproduce the performance of a single dataset, you will need to follow the steps below to run the script:
- Training on ImageNet: `bash ./scripts/xd_train.sh gpu`
- Test on New Dataset for Domain Generalization: `bash ./scripts/xd_test_dg.sh dataset seed gpu`
- Test on New Dataset for Cross-dataset Evaluation: `bash ./scripts/xd_test_cde.sh dataset seed gpu`

## Results

