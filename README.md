# TorchServe Instruction
- An introduction to TorchServe, a performant, flexible and easy to use tool for serving PyTorch models in production.
- An easy-to-understand instruction: [Link](https://viblo.asia/p/torchserve-cong-cu-ho-tro-trien-khai-mo-hinh-pytorch-vyDZOqwO5wj)


## 1. Setting
```
git clone https://github.com/pytorch/serve
cd serve
```
```
python ./ts_scripts/install_dependencies.py
```
```
pip install torchserve torch-model-archiver
```

## 2. Save model by TorchServe
```
mkdir model_store
```
```
wget https://download.pytorch.org/models/densenet161-8d451a50.pth
```
```
torch-model-archiver \
--model-name densenet161 \
--version 1.0 \
--model-file ./examples/image_classifier/densenet_161/model.py \
--serialized-file densenet161-8d451a50.pth \
--export-path model_store \
--extra-files ./examples/image_classifier/index_to_name.json \
--handler image_classifier
```

**Result**: model_store/densenet161.mar (from _--model-name densenet161_)

## 3. Run TorchServe
```
torchserve \
--start --ncs \
--model-store model_store \
--models densenet161.mar
```

