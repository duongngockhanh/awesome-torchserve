# ResNet-18 by TorchServe
Demo an spicific model, ResNet-18 by TorchServe

- Create model_store
```
mkdir model_store
```

- Download pretrained resnet-18
```
wget https://download.pytorch.org/models/resnet18-f37072fd.pth
```

- Create resnet-18.mar
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

- Run
```
torchserve \
--start --ncs \
--model-store model_store \
--models resnet-18.mar
```

- Stop
```
torchserve --stop
```

- Check models
```
curl http://0.0.0.0:8081/models/
```

- config.properties
```
inference_address=http://0.0.0.0:8080
management_address=http://0.0.0.0:8081
metrics_address=http://0.0.0.0:8082

# load_models=all
install_py_dep_per_model=true
model_store=model-store
max_request_size=26214400
max_response_size=26214400
grpc_inference_port=6060
grpc_management_port=6061
models={\
  "VehicleDetection": {\
    "1.0": {\
        "defaultVersion": true,\
        "marName": "VehicleDetection.mar",\
        "minWorkers": 1,\
        "maxWorkers": 8,\
        "batchSize": 40,\
        "maxBatchDelay": 500,\
        "responseTimeout": 50\
    }\
  },\
  "LaneDetection": {\
    "1.0": {\
        "defaultVersion": true,\
        "marName": "LaneDetection.mar",\
        "minWorkers": 1,\
        "maxWorkers": 8,\
        "batchSize": 40,\
        "maxBatchDelay": 500,\
        "responseTimeout": 50\
    }\
  }\
```
