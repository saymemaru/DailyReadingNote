# Halcon 深度学习参数

详细请参考
 MVTec/DeepLearningTool/doc/deeplearningtool/zh/training_manual  

 [DeepLearningTool 手册](../../../../app/MVTec/DeepLearningTool/doc/deeplearningtool/zh/training_manual/general_train.html)

## 预训练模型

>如果想知道网络模型各参数值，可以使用算子 get_dl_classifier_param 获取

>对于至少有一个全连接层的网络模型，只要图像尺寸变了，就需要重新训练，比如 enhanced 模型；对于没有全连接层的网络，训练好的网络模型可以直接应用在不同尺寸的图像上，但分类精度会降低  
>
>即，请尽量使用同尺寸图像训练推理

### 1. pretrained_dl_classifier_compact.hdl

- 原理：SqueezeNet网络  
- 优点是节省内存以及运行效率高
- 支持``real``图像类型
- 支持改变训练图像尺寸，最小尺寸不能低于 15 x 15。
- 可以应用在不同尺寸的图像上推理，但精度会降低。

### 2. pretrained_dl_classifier_alexnet.hdl

- 第一层卷积核比 compact 更大，更有利于特征提取。

### 3. pretrained_dl_classifier_enhanced.hdl

- 对比 compact 网络，拥有更多的隐含层，因此可以胜任更复杂的分类任务
- 需要更大内存以及更长的训练时间，由于隐含层的增多，计算比上面的网络更复杂
- 所以 batch_size 不能设置太大
- 支持改变训练图像尺寸，最小尺寸不能低于 47 x 47
- 图像尺寸越大，占用内存资源越多
- 更改图像大小将重新初始化全连接层的权重，因此需要重新训练网络
  
### 4. retrained_dl_classifier_resnet50.hdl

- 类似 enhanced 模型，但对更复杂的分类任务表现效果更好
- 网络结构不同于以上两个模型，训练时稳定性以及鲁棒性更好
- 支持改变训练图像尺寸，但是最小尺寸不能低于32 x 32
- 尽管同样是全连接层，图像大小的改变不会导致权重的重新初始化

### 5. retrained_dl_classifier_resnet18.hdl

- 类似 resnet50，但复杂性更低，推理时间更快
- 支持改变训练图像尺寸，但是最小尺寸不能低于32 x 32

### 6. pretrained_dl_classifier_mobilenet_v2.hdl

- 体积小，功耗低，适合移动和嵌入式视觉应用

## 参数设置

### 高级参数设置

#### 图像宽度/高度

- 在预处理过程中，所有图像都会被缩放到图像宽度和图像高度中设置的值，这会改变它们的长宽比。
>
>要检测位置请让输入图片尺寸与预处理尺寸相等

## Halcon程序

读取数据集
>.dict 或 .json 格式数据集

```C++
read_dict(数据集，string,string,句柄DictHandle)
```

读取第三方数据集

```C++
read_dl_dataset_from_coco(数据集,string,string,DLDataset)
```

最小工作流程
```c++
dev_update_off ()
Backbone:='pretrained_dl_classifier_compact.hdl'
NumClasses:=1
ImageWidth:=512
ImageHeight:=320
*压缩后的图像通道数
ImageNumChannels:=1
*设置最小值，最大值，锚数值和锚纵横比等超参数
MinLevel:=2
MaxLevel:=4
AnchorNumSubscales:=3
AnchorAspectRatios:=[1.0,0.5,2.0]
Capacity:='medium'
******创建对象检测模型************
*为泛型参数创建字典并创建对象检测模型
create_dict (DLModelDetectionParam)
set_dict_tuple (DLModelDetectionParam, 'image_width', ImageWidth)
set_dict_tuple (DLModelDetectionParam, 'image_height', ImageHeight)
set_dict_tuple (DLModelDetectionParam, 'image_num_channels', ImageNumChannels)
set_dict_tuple (DLModelDetectionParam, 'min_level', MinLevel)
set_dict_tuple (DLModelDetectionParam, 'max_level', MaxLevel)
set_dict_tuple (DLModelDetectionParam, 'anchor_num_subscales', AnchorNumSubscales)
set_dict_tuple (DLModelDetectionParam, 'anchor_aspect_ratios', AnchorAspectRatios)
set_dict_tuple (DLModelDetectionParam, 'capacity', Capacity)
*创建模型
create_dl_model_detection (Backbone, NumClasses, DLModelDetectionParam, DLModelHandle)
*************数据预处理***************
*输出文件夹
ExampleDataDir:='D:/middle report'
DLModeFileName:=ExampleDataDir+'/pretrained_dl_model_detection.hdl'
DataDirectory:=ExampleDataDir+'/output_data_'+ImageWidth+'x'+ImageHeight
PreprocessParamFileName:=DataDirectory+'/dl_preprocess_param_'+ImageWidth+'x'+ImageHeight+'.hdict'
*用于拆分的数据集,训练集70%，15%验证集，15%测试集
TrainingPercent:=70
ValidationPercent:=15
*设置随机种子
SeedRand:=42
file_exists (ExampleDataDir, FileExists)
if(not FileExists)
    make_dir (ExampleDataDir)
endif
*读取数据库字典
read_dict ('D:/middle report/jiance.hdict', [], [], DictHandle)
*从模型中的数据集中设置类ID
get_dict_tuple (DictHandle, 'class_ids', ClassIDs)
set_dl_model_param (DLModelHandle, 'class_ids', ClassIDs)
*编写初始化的DL对象检测模型 
write_dl_model (DLModelHandle, DLModeFileName)
set_system ('seed_rand', SeedRand)
split_dl_dataset (DictHandle, TrainingPercent, ValidationPercent, [])
*从模型中获取预处理参数
create_dl_preprocess_param_from_model (DLModelHandle, 'false', 'full_domain', [], [], [], DLPreprocessParam)
create_dict (GenParam)
set_dict_tuple (GenParam, 'overwrite_files', true)
*数据预处理部分
preprocess_dl_dataset (DictHandle, DataDirectory, DLPreprocessParam, GenParam, DLDatasetFileName)
write_dict (DLPreprocessParam, PreprocessParamFileName, [], [])
get_dict_tuple (DictHandle, 'samples', DatasetSamples)
find_dl_samples (DatasetSamples, 'split', 'train', 'match', SampleIndices)
tuple_shuffle (SampleIndices, ShuffledIndices)
read_dl_samples (DictHandle, ShuffledIndices[0:9], DLSampleBatchDisplay)
*设置dev_display_dl_数据的参数
create_dict (WindowHandleDict)
create_dict (GenParam)
set_dict_tuple (GenParam, 'scale_windows', 1.2)
*在DLSampleBatchDisplay中显示示例
for Index := 0 to |DLSampleBatchDisplay| - 1 by 1
   *在DLSampleBatchDisplay中循环采样
    dev_display_dl_data (DLSampleBatchDisplay[Index], [], DictHandle, 'bbox_ground_truth', GenParam, WindowHandleDict)
    get_dict_tuple (WindowHandleDict, 'bbox_ground_truth', WindowHandles)
    * 添加解释性文本
    dev_set_window (WindowHandles[0])
    get_dict_object (Image, DLSampleBatchDisplay[Index], 'image')
    get_image_size (Image, ImageWidth, ImageHeight)
    dev_disp_text ('New image size after preprocessing: ' + ImageWidth + ' x ' + ImageHeight, 'window', 'bottom', 'right', 'black', [], [])
    dev_set_window (WindowHandles[1])
    dev_disp_text ('Press Run (F5) to continue', 'window', 'bottom', 'right', 'black', [], [])
    stop ()
endfor
dev_display_dl_data_close_windows (WindowHandleDict)

```

## 参考文章

1. [知乎 - Halcon深度学习(预训练网络模型介绍）- Evian​](https://zhuanlan.zhihu.com/p/432956443)
