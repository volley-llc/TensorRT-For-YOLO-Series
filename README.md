# YOLO Series TensorRT Python/C++ 

# Conversion

## FP16 TRT model
- If you use TRT 8.2 or lower you have to set `nms_fp32` param to True
- If you use TRT 8.4 or higher you can set `nms_fp32` param to False
```
python3 export.py -o yolov7_e2e.onnx -e yolov7_e2e_fp16.trt -p fp16 --nms_fp32 True
```
## INT8 TRT model
### Model with integrated pre-processing
- Input of model with integrated pre-processing not requires any-preprocessing of raw image, it all done in computation graph
- Logic of `nms_fp32` is the same as described aboce
```
python3 export.py -o yolov7_e2e.onnx -e yolov7_e2e_int8.trt -p int8 --nms_fp32 True --calib_input ./images
```
### Model without integrated pre-processing
- Model without integrated pre-processing requires input normalization
```
python3 export.py -o yolov7_nms.onnx -e yolov7_nms_int8.trt -p int8 --nms_fp32 True --calib_norm_input True --calib_input ./images
```

##  Prepare TRT Env 
`Python`
```
pip install --upgrade setuptools pip --user
pip install nvidia-pyindex
pip install --upgrade nvidia-tensorrt
pip install pycuda
```