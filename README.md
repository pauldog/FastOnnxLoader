# FastOnnxLoader 🚀👩‍🚀
Loads in onnx files with less RAM. (Not necessarily faster -but nearly) Useful for loading very large ONNX files onto the GPU with limited RAM.

This script is a test to load an ONNX file in OnnxRuntime with less RAM by first loading in an ONNX with no embedded weights, then sequentially loading in the weight files one by one.

Workflow
===
1. export the torch model using `torch.onnx.export()` which gives you your basic model.onnx file
2. Use `python separate.py` on model.onnx to separate weights and also rename bad weight names.
3. Use `python clear.py` on this new model.onnx file to create a model_without_weights.onnx
4. Use the C# code to load in the `model_without_weights.onnx` and sequentially load in the weight files.

separate.py
===
This takes an onnx file and separates it into separate weight files. It makes sure to rename weights with illegal characters such as ":". One thing to not is that it doesn't separate weight with less than about 650 bytes. (The exact number is not documented)

clear.py
===
If you already have an onnx file with separated weights (for example it might be a >2GB onnx). Then you can just use clear.py to create a **model_without_weights.onnx** file.



Issues
===
No issues at the moment


See also
===
https://github.com/microsoft/onnxruntime/issues/15429


![image](https://user-images.githubusercontent.com/33497043/230762304-1123df5c-e374-4614-8a5e-8ddc28452def.png)

----
Decompression
===
I am also working on a utility that decompressed quantized onnx files so they can be run faster in float16. This is useful to save space on the hard drive.

getoffsets.py
===
This is a helper file that extracts all the scales and zero_points from a quantized onnx files and writes them to a json file. 


