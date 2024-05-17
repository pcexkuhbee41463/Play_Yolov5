## Yolov5目标检测模型的pytorch精简实现




## 安装环境
torch==1.2.0

## 文件下载

VOC数据集下载地址如下，里面已经包括了训练集、测试集、验证集（与测试集一样），无需再次划分。
链接：https://pan.baidu.com/s/1xHNrhdJIRh5vVVK8OT3bDg 
提取码：kcmd 

训练所需的权值下载地址如下。
链接：https://pan.baidu.com/s/1PFJFyDeLRMNw-HQvnclgTg 
提取码：scsd 


## 训练步骤
### a、训练VOC07+12数据集
1. 数据集的准备   
使用VOC格式进行训练，训练前需要下载好VOC07+12的数据集，解压后放在根目录。

2. 数据集的处理   
修改voc_annotation.py里面的annotation_mode=2，运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，直接运行train.py即可开始训练。   

4. 训练结果预测   
训练结果预测需要用到两个文件，分别是yolo.py和predict.py。首先需要去yolo.py里面修改model_path以及classes_path，这两个参数必须要修改。   
model_path指向训练好的权值文件，在logs文件夹里； classes_path指向检测类别所对应的txt。 
完成修改后就可以运行predict.py进行检测，运行后输入图片路径即可检测。   

### b、训练自己的数据集
1. 数据集的准备   
训练前将标签文件放在VOCdevkit文件夹下的VOC2007文件夹下的Annotation中。   
训练前将图片文件放在VOCdevkit文件夹下的VOC2007文件夹下的JPEGImages中。   

2. 数据集的处理  
在完成数据集的摆放后，需要利用voc_annotation.py获得训练用的2007_train.txt和2007_val.txt。   
修改voc_annotation.py里面的参数。第一次训练可以仅修改classes_path，classes_path用于指向检测类别所对应的txt。   
训练自己的数据集时，可以自己建立一个cls_classes.txt，里面写自己所需要区分的类别。   
修改voc_annotation.py中的classes_path，使其对应cls_classes.txt，并运行voc_annotation.py。  

3. 开始网络训练  
classes_path用于指向检测类别所对应的txt，这个txt和voc_annotation.py里面的txt一样，训练自己的数据集必须要修改。 
修改完classes_path后就可以运行train.py开始训练了，在训练多个epoch后，权值会生成在logs文件夹中。  

4. 训练结果预测  
训练结果预测需要用到两个文件，分别是yolo.py和predict.py。在yolo.py里面修改model_path以及classes_path。  
model_path指向训练好的权值文件，在logs文件夹里；classes_path指向检测类别所对应的txt。
完成修改后就可以运行predict.py进行检测，运行后输入图片路径即可检测。  

## 预测步骤
### a、使用预训练权重
1. 下载完库后解压，在百度网盘下载权值，放入model_data，运行predict.py，输入  
```python
img/street.jpg
```
2. 在predict.py里面进行设置可以进行fps测试和video视频检测。  
### b、使用自己训练的权重
1. 按照训练步骤训练。  
2. 在yolo.py文件里面，按照对应注释修改model_path和classes_path使其对应训练好的文件。
3. 运行predict.py，输入  
```python
img/street.jpg
```
4. 在predict.py里面进行设置可以进行fps测试和video视频检测。  


## Reference
https://github.com/ultralytics/yolov5   
