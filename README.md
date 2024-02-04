# Swin-UMamba: Mamba-based UNet with ImageNet-based pretraining

Official repository for: *Swin-UMamba: Mamba-based UNet with ImageNet-based pretraining*

![network](https://github.com/JiarunLiu/Swin-UMamba/blob/main/assets/swin-umamba.png)

## Installation

**Step-1:** Create a new conda environment & install requirements

```shell
conda create -n swin_umamba python=3.10
conda activate swin_umamba

pip install torch==2.0.1 torchvision==0.15.2
pip install causal-conv1d==1.1.1
pip install mamba-ssm
pip install torchinfo timm
```

**Step-2:** Install Swin-UMamba

```shell
git clone https://github.com/JiarunLiu/Swin-UMamba
cd Swin-UMamba/swin_umamba
pip install -e .
```

## Prepare data

**Dataset:**  We use the same data & processing strategy following U-Mamba. Download dataset from [U-Mamba](https://github.com/bowang-lab/U-Mamba) and put them into the data folder. Then preprocess the dataset with following command:

```shell
nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
```

**ImageNet pretrained model:** We use the pretrained VMamba-Tiny model from [here](https://drive.google.com/file/d/1ml7nZM-YPYbQurHiodf4dpXHw88dXFfP/view?usp=sharing). You need to put the model checkpoint into `data/pretrained/vmamba/vmamba_tiny_e292.pth`

## Training

Using the following command to train & evaluate Swin-UMamba

```shell
# AbdomenMR dataset
bash scripts/train_AbdomenMR.sh MODEL_NAME
# Endoscopy dataset
bash scripts/train_Endoscopy.sh MODEL_NAME
# Microscopy dataset 
bash scripts/train_Microscopy.sh MODEL_NAME
```

Here  `MODEL_NAME` can be:

- `nnUNetTrainerSwinUMamba`: Swin-UMamba model with ImageNet pretraining
- `nnUNetTrainerSwinUMambaD`: Swin-UMamba$\dagger$  model with ImageNet pretraining
- `nnUNetTrainerSwinUMambaScratch`: Swin-UMamba model without ImageNet pretraining
- `nnUNetTrainerSwinUMambaDScratch`: Swin-UMamba$\dagger$  model without ImageNet pretraining

We will release our models later.

## Acknowledgements

We thank the authors of [nnU-Net](https://github.com/MIC-DKFZ/nnUNet), [Mamba](https://github.com/state-spaces/mamba), [UMamba](https://github.com/bowang-lab/U-Mamba), and [VMamba](https://github.com/MzeroMiko/VMamba) for making their valuable code & data publicly available.