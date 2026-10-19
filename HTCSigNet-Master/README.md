# HTCSigNet
# Usage

## Data preprocessing

The functions in this package expect training data to be provided in a single .npz file, with the following components[1] :

* ```x```: Signature images (numpy array of size N x 1 x H x W)
* ```y```: The user that produced the signature (numpy array of size N )
* ```yforg```: Whether the signature is a forgery (1) or genuine (0) (numpy array of size N )

We provide functions to process some commonly used datasets in the script ```htcsignet.datasets.process_dataset```. 

```bash
python -m htcsignet.preprocessing.process_dataset --dataset gpds \
 --path gpds/path --save-path gods_256_256.npz
```

During training a random crop of size 256x256 is taken for each iteration. During test we use the center 224x224 crop.

## Training 

Training HTCSigNet with lambda=0.95:

```
python -m htcsignet.featurelearning.htcsignet_train_train --model htcsignet --dataset-path  <data.npz> --users [first last]\
--epochs 100 --forg --lamb 0.95 --logdir ../../htcsignet_lr_0.95  
```

## Training WD classifiers and evaluating the result

For training and testing the WD classifiers, use the ```htcsignet.wd.test``` script. Example:

```bash
python -m htcsignet.wd.htcsignet_wd_test -m htcsignet --model-path <path/to/trained_model> \
    --data-path <path/to/data>  --exp-users 0 300 --dev-users 0 300 --gen-for-train 12
```

## Update-2026.10.19！！！
## Weight Sharing
I've shared the file htcsignet.pth with you via Quark Cloud Drive. Open the Quark APP by tapping the link or copying the full content below to access it.
/~f38b3bZCEe~:/
Link: https://pan.quark.cn/s/f973a6bb5495?pwd=wp87
Extraction code: wp87


## Reference
[1] Hafemann, Luiz G., Robert Sabourin, and Luiz S. Oliveira. "Learning Features for Offline Handwritten Signature Verification using Deep Convolutional Neural Networks" http://dx.doi.org/10.1016/j.patcog.2017.05.012 ([preprint](https://arxiv.org/abs/1705.05787))

## Acknowledgments
The implementation of featurelearning and WD-based verification is based on https://github.com/luizgh/sigver
