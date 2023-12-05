# Resnet-18 by TorchServe

### Create model_store
```
mkdir model_store
```

### Download pretrained resnet-18
```
wget https://download.pytorch.org/models/resnet18-f37072fd.pth
```

### Create resnet-18.mar
```
torch-model-archiver \
--model-name resnet-18 \
--version 1.0 \
--model-file model.py \
--export-path model_store \
--serialized-file resnet18-f37072fd.pth \
--extra-files index_to_name.json \
--handler image_classifier
```

### Run
```
torchserve \
--start --ncs \
--model-store model_store \
--models resnet-18.mar
```

### Stop
```
torchserve --stop
```
