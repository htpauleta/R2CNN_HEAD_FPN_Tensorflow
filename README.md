# R2CNN_HEAD: Rotational Region CNN for Orientation Robust Scene Detection with Head Direction

A Tensorflow implementation of FPN or R2CNN detection framework based on [FPN](https://github.com/yangxue0827/FPN_Tensorflow).  
You can refer to the papers [R2CNN Rotational Region CNN for Orientation Robust Scene Text Detection](https://arxiv.org/abs/1706.09579) or [Feature Pyramid Networks for Object Detection](https://arxiv.org/abs/1612.03144)    
Other rotation detection method reference [R-DFPN](https://github.com/yangxue0827/R-DFPN_FPN_Tensorflow) and [R2CNN](https://github.com/yangxue0827/R2CNN_FPN_Tensorflow) 
If useful to you, please star to support my work. Thanks.    

# Configuration Environment
ubuntu(Encoding problems may occur on windows) + python2 + tensorflow1.2 + cv2 + cuda8.0 + GeForce GTX 1080     
If you want to use cpu, you need to modify the parameters of NMS and IOU functions use_gpu = False  in cfgs.py     
You can also use docker environment, command: docker push yangxue2docker/tensorflow3_gpu_cv2_sshd:v1.0    

# Installation      
  Clone the repository    
  ```Shell    
  git clone https://github.com/yangxue0827/R2CNN_HEAD_FPN_Tensorflow.git    
  ```     

# Make tfrecord   
The image name is best in English.       
The data is VOC format, reference [here](sample.xml)     
data path format  ($R2CNN_HEAD_ROOT/data/io/divide_data.py)    
VOCdevkit  
>VOCdevkit_train  
>>Annotation  
>>JPEGImages   

>VOCdevkit_test   
>>Annotation   
>>JPEGImages   

Clone the repository    
  ```Shell    
  cd $R2CNN_HEAD_ROOT/data/io/  
  python convert_data_to_tfrecord.py --VOC_dir='***/VOCdevkit/VOCdevkit_train/' --save_name='train' --img_format='.jpg' --dataset='ship'
       
  ``` 
# Demo   
1、Unzip the weight $R2CNN_HEAD_ROOT/output/res101_trained_weights/*.rar    
2、put images in $R2CNN_HEAD_ROOT/tools/inference_image   
3、Configure parameters in $R2CNN_HEAD_ROOT/libs/configs/cfgs.py and modify the project's root directory    
4、     
  ```Shell    
  cd $R2CNN_HEAD_ROOT/tools      
  ```    
5、image slice         
  ```Shell    
  python inference.py   
  ```   

6、big image      
  ```Shell    
  cd $FPN_ROOT/tools
  python demo.py --src_folder=.\demo_src --des_folder=.\demo_des         
  ```   

# Train   
1、Modify $R2CNN_HEAD_ROOT/libs/lable_name_dict/***_dict.py, corresponding to the number of categories in the configuration file    
2、download pretrain weight([resnet_v1_101_2016_08_28.tar.gz](http://download.tensorflow.org/models/resnet_v1_101_2016_08_28.tar.gz) or [resnet_v1_50_2016_08_28.tar.gz](http://download.tensorflow.org/models/resnet_v1_50_2016_08_28.tar.gz)) from [here](https://github.com/yangxue0827/models/tree/master/slim), then extract to folder $R2CNN_HEAD_ROOT/data/pretrained_weights    
3、  
  ```Shell    
  cd $R2CNN_HEAD_ROOT/tools      
  ``` 
4、Choose a model([FPN](https://github.com/yangxue0827/FPN_Tensorflow)  and R2CNN)           
  ```Shell    
  python train.py   
  ```      

# Test tfrecord     
  ```Shell    
  cd $R2CNN_HEAD_ROOT/tools   
  python test.py      
  ```    

# eval   
  ```Shell    
  cd $R2CNN_HEAD_ROOT/tools   
  python eval.py    
  ```  

# Summary    
  ```Shell    
  tensorboard --logdir=$R2CNN_HEAD_ROOT/output/res101_summary/ 
  ```     
![01](output/res101_summary/fast_rcnn_loss.bmp) 
![02](output/res101_summary/rpn_loss.bmp) 
![03](output/res101_summary/total_loss.bmp) 

# Graph
![04](graph.png) 

# Test results   
![11](tools/test_result/01_horizontal_gt.jpg)   
![12](tools/test_result/01_horizontal_fpn.jpg)   
     
![13](tools/test_result/01_rotate_gt.jpg)   
![14](tools/test_result/01_rotate_fpn.jpg)  

![15](tools/test_result/08_horizontal_gt.jpg)    
![16](tools/test_result/08_horizontal_fpn.jpg)   
     
![17](tools/test_result/08_rotate_gt.jpg)    
![18](tools/test_result/08_rotate_fpn.jpg)     