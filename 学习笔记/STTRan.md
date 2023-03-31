## STTran中数据集Action Genome 的处理

##### Action  Genome官网包含三个文件:

annotations+Chrades_v1_480.zip+Chrades_rgb.tar

<img src="C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230222202042603.png" alt="image-20230222202042603" style="zoom:100%;" />

![image-20230222202151879](C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230222202151879.png)

##### 对于这三个文件的解压或使用：

1、对于Chrades_v1_480.zip可以直接解压成视频文件夹即可

2、对于Chrades_rgb.tar需要使用https://github.com/JingweiJ/ActionGenome上的tools进行解压所有的视频帧，而非只是打标的帧

```python
# 注意 ffmpeg版本必须要高于2.8.15，否则帧解压不出来
python tools/dump_frames.py --all_frames
```

3、对于annotations中的五个文件，object_bbox_and_relationship.pkl包含的结构如下所示：

```
{...
    'VIDEO_ID/FRAME_ID':
        [...
            {
                'class': 'book',
                'bbox': (x, y, w, h),
                'attention_relationship': ['looking_at'],
                'spatial_relationship': ['in_front_of'],
                'contacting_relationship': ['holding', 'touching'],
                'visible': True,
                'metadata': 
                    {
                        'tag': 'VIDEO_ID/FRAME_ID',
                        'set': 'train'
                    }
            }
        ...]
...}
```

注意：'visible'表示交互对象在帧中是否可见。

 `person_bbox.pkl` 包含每个帧中的人物框. 

 `frame_list.txt` 包含所有已打标的帧列表

 `object_classes.txt` 包含所有对象的类别

 `relationship_classes.txt` 包含所有人和对象之间关系的类别

##### 处理好后的数据存放在文件中的位置：

```python
|-- action_genome
    |-- annotations   #gt annotations
    |-- frames        #sampled frames
    |-- videos        #original videos
```

##### 加载两个pkl文件：

```python
with open(root_path + 'annotations/person_bbox.pkl', 'rb') as f:
    person_bbox = pickle.load(f)
f.close()
with open(root_path+'annotations/object_bbox_and_relationship.pkl', 'rb') as f:
    object_bbox = pickle.load(f)
f.close()
```

person_bbox是一个字典内容为：

```python
{'001YG.mp4/000089.png': 
  {'bbox': array([[ 24.29774 ,  71.443954, 259.23602 , 268.20288 ]], dtype=float32), 
   'bbox_score': array([0.9960979], dtype=float32), 
   'bbox_size': (480, 270), 
   'bbox_mode': 'xyxy', 
   'keypoints': array([[[149.51952 , 120.54931 ,   1.      ],
        [146.48587 , 111.43697 ,   1.      ],
        [141.09274 , 115.824394,   1.      ],
        [111.76759 , 123.58676 ,   1.      ],
        [112.44173 , 124.26174 ,   1.      ],
        [ 82.10537 , 154.6362  ,   1.      ],
        [113.45295 , 168.47343 ,   1.      ],
        [153.56436 , 207.96022 ,   1.      ],
        [162.66527 , 247.44699 ,   1.      ],
        [146.48587 , 149.91127 ,   1.      ],
        [216.59659 , 229.22232 ,   1.      ],
        [112.10466 , 243.73456 ,   1.      ],
        [163.3394  , 267.69662 ,   1.      ],
        [237.83205 , 202.56032 ,   1.      ],
        [239.18031 , 202.56032 ,   1.      ],
        [186.93436 , 219.0975  ,   1.      ],
        [220.9785  , 227.87234 ,   1.      ]]], dtype=float32),        'keypoints_logits': array([[11.073427, 10.578527, 10.863391,  3.6263876 , 11.451177  ,
         4.500312  ,  6.419147  ,  3.4865067 ,  7.920906  ,  5.6766253 ,
         9.343614  , -0.7024717 , -0.36381796,  1.039403  ,  1.1701871 ,
        -0.03817523, -2.2913933 ]], dtype=float32)}
```

object_bbox是一个字典的内容，字典的value是一个list[0,1]

```python
'CUZND.mp4/000424.png':
    [
        {'class': 'light', 
      'bbox': None, 
      'attention_relationship': None, 
      'spatial_relationship': None, 
      'contacting_relationship': None, 
      'metadata': {'tag': 'CUZND.mp4/light/000424', 
                   'set': 'train'},    	  
      'visible': False},
     
     {'class': 'phone/camera', 
      'bbox': (226.7415413533836, 62.54913324979104, 11.84210526315789, 22.368421052631575),
      'attention_relationship': ['looking_at'], 
      'spatial_relationship': ['in_front_of'], 			    			  'contacting_relationship': ['holding'], 
      'metadata': {'tag': 'CUZND.mp4/phone_camera/000424', 
                   'set': 'train'}, 
      'visible': True}
    ]
```



# 断点调试

文件：sttran.py 位置：331行  entry = self.object_classifier(entry)之后

**entry**是一个包含14个key的字典：

'boxes'(Tensor 109 *5) 

'lables'(Tensor 109)

```python
tensor([ 1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,
         1, 32,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1,
        16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,
         7, 15,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,  7, 15,
         1, 16,  7, 15,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,
         7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1,  7,  1,  7,  1,
         7], device='cuda:0')
```

'scores'(Tensor 109 ) 

```python
tensor([1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
        1.], device='cuda:0')
```

'im_idx'(Tensor 71) 

```python
tensor([ 0.,  1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 10., 11., 11.,
        12., 12., 13., 13., 14., 14., 15., 15., 16., 16., 17., 17., 18., 18.,
        18., 19., 19., 19., 20., 20., 20., 21., 21., 21., 22., 22., 22., 23.,
        23., 23., 24., 24., 24., 25., 25., 25., 26., 26., 27., 27., 28., 28.,
        29., 29., 30., 30., 31., 31., 32., 32., 33., 33., 34., 34., 35., 36.,
        37.])
```

'pair_idx'(Tensor 71*2) 

```
tensor([[  0,   1], [  2,   3], [  4,   5], [  6,   7],  [  8,   9], [ 10,  11],[ 12,  13], [ 14,  15], [ 16,  17],
[ 18,  19],[ 20,  21],[ 20,  22],[ 23,  24],[ 23,  25],[ 26,  27],[ 26,  28],[ 29,  30],[ 29,  31],[ 32,  33],[ 32,  34],
[ 35,  36],[ 35,  37],[ 38,  39],[ 38,  40],[ 41,  42],[ 41,  43], [ 44,  45],[ 44,  46],[ 44,  47],[ 48,  49],[ 48,  50],
[ 48,  51],[ 52,  53],[ 52,  54], 52,  55],[ 56,  57],[ 56,  58],[ 56,  59],[ 60,  61],[ 60,  62],[ 60,  63],[ 64,  65],[ 64,  66],[ 64,  67],[ 68,  69],[ 68,  70],[ 68,  71],[ 72,  73],[ 72,  74],[ 72,  75], [ 76,  77],[ 76,  78], [ 79,  80], [ 79,  81],[ 82,  83],[ 82,  84],[ 85,  86],[ 85,  87],[ 88,  89],[ 88,  90],[ 91,  92],[ 91,  93],[ 94,  95],[ 94,  96],[ 97,  98],[ 97,  99],[100, 101],[100, 102],[103, 104],[105, 106],[107, 108]])
```

'human_idx'(Tensor 38 *1) 

```python
tensor([[  0],
        [  2],
        [  4],
        [  6],
        [  8],
        [ 10],
        [ 12],
        [ 14],
        [ 16],
        [ 18],
        [ 20],
        [ 23],
        [ 26],
        [ 29],
        [ 32],
        [ 35],
        [ 38],
        [ 41],
        [ 44],
        [ 48],
        [ 52],
        [ 56],
        [ 60],
        [ 64],
        [ 68],
        [ 72],
        [ 76],
        [ 79],
        [ 82],
        [ 85],
        [ 88],
        [ 91],
        [ 94],
        [ 97],
        [100],
        [103],
        [105],
        [107]], device='cuda:0')
```

'features'(Tensor 109 *2048) 

'union_feat'(Tensor 71 *1024 * 7 * 7) 

'union_box'(Tensor 71 *5) 

'spatial_masks'(Tensor 71 *2 * 27 * 27) 

'attention_gt'(list 71) 

```python
[[0], [2], [1], [1], [1], [2], [2], [1], [2], [1], [0], [0], [0], [0], [0], [0], [0], [0], [0], [0], [0], [0], [0], [0], [2], [0], [2], [0], [1], [0], [0], [1], [0], [1], [0], [0], [0], [1], [0], [0], [0], [0], [1], [1], [0], [0], [2], [1], [0], [0], [0], [0], [2], [1], [0], [1], [0], [1], [0], [1], [0], [1], [0], [0], [0], [0], [0], [0], [0], [1], [0]]
```

'spatial_gt'(list 71) 

```python
[[2], [2], [0], [2], [2], [2], [2], [3], [2], [3], [1, 2], [2], [1], [2], [1, 2], [2], [1, 2], [2], [1, 2], [2], [1], [2, 4], [1, 2], [4], [1], [2, 4], [1], [2], [5], [1], [2, 4], [5], [1], [4, 2], [5], [1], [2], [5], [0], [2, 4], [5], [1, 2], [2], [3], [1, 2], [2, 4], [5], [2, 1], [2], [5], [1, 2], [2], [1, 2], [2], [1, 2], [2], [1, 2], [2], [1, 2], [2], [1], [2], [1, 2], [2], [1, 2], [2], [1, 2], [2], [2], [2], [2]]
```

'contacting_gt'(list 71) 

```python
[[8], [8], [12], [12], [12], [8], [12], [8], [8], [8], [11], [8], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [8], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [5], [11], [8], [8], [5], [8]]
```

'pred_labels'(Tensor 109) 

```python
tensor([ 1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,  1, 32,
         1, 32,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1,
        16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,
         7, 15,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,  7, 15,  1, 16,  7, 15,
         1, 16,  7, 15,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,
         7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1, 16,  7,  1,  7,  1,  7,  1,
         7], device='cuda:0')
```

**obj_class** (Tensor 71) 

```python
tensor([32, 32, 32, 32, 32, 32, 32, 32, 32, 32, 16,  7, 16,  7, 16,  7, 16,  7,
        16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,
         7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 16,  7,
        16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 16,  7,  7,  7,  7],
       device='cuda:0')
```

**obj_rep** (Tensor 71*512) 

**obj_emb**(Tensor 71*200)

**subj_class** (Tensor 71) 全为1

**sub_rep** (Tensor 71*512) 

**subj_emb**(Tensor 71 *200)

**vr** (Tensor 71*512) 

**x_visual** (Tensor 71*1536) 

**x_semantic** (Tensor 71*400) 

**rel_features** (Tensor 71*1936) 

**obj_class** (Tensor 71) 

```py
tensor([32, 32, 32, 32, 32, 32, 32, 32, 32, 32, 16,  7, 16,  7, 16,  7, 16,  7,
        16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,
         7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 15, 16,  7, 16,  7,
        16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 16,  7, 16,  7,  7,  7,  7],
       device='cuda:0')
```

![image-20230228124545094](C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230228124545094.png)

![image-20230228125050950](C:\Users\pc\AppData\Roaming\Typora\typora-user-images\image-20230228125050950.png)

**self模块=Sttran**

```python
STTran(
  (object_classifier): ObjectClassifier(
    (RCNN_roi_align): ROIAlign(output_size=(7, 7), spatial_scale=0.0625, sampling_ratio=0)
    (obj_embed): Embedding(36, 200)
    (pos_embed): Sequential(
      (0): BatchNorm1d(4, eps=1e-05, momentum=0.001, affine=True, track_running_stats=True)
      (1): Linear(in_features=4, out_features=128, bias=True)
      (2): ReLU(inplace=True)
      (3): Dropout(p=0.1, inplace=False)
    )
    (decoder_lin): Sequential(
      (0): Linear(in_features=2376, out_features=1024, bias=True)
      (1): BatchNorm1d(1024, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)
      (2): ReLU()
      (3): Linear(in_features=1024, out_features=37, bias=True)
    )
  )
  (union_func1): Conv2d(1024, 256, kernel_size=(1, 1), stride=(1, 1))
  (conv): Sequential(
    (0): Conv2d(2, 128, kernel_size=(7, 7), stride=(2, 2), padding=(3, 3))
    (1): ReLU(inplace=True)
    (2): BatchNorm2d(128, eps=1e-05, momentum=0.01, affine=True, track_running_stats=True)
    (3): MaxPool2d(kernel_size=3, stride=2, padding=1, dilation=1, ceil_mode=False)
    (4): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
    (5): ReLU(inplace=True)
    (6): BatchNorm2d(256, eps=1e-05, momentum=0.01, affine=True, track_running_stats=True)
  )
  (subj_fc): Linear(in_features=2048, out_features=512, bias=True)
  (obj_fc): Linear(in_features=2048, out_features=512, bias=True)
  (vr_fc): Linear(in_features=12544, out_features=512, bias=True)
  (obj_embed): Embedding(37, 200)
  (obj_embed2): Embedding(37, 200)
  (glocal_transformer): transformer(
    (local_attention): TransformerEncoder(
      (layers): ModuleList(
        (0): TransformerEncoderLayer(
          (self_attn): MultiheadAttention(
            (out_proj): NonDynamicallyQuantizableLinear(in_features=1936, out_features=1936, bias=True)
          )
          (linear1): Linear(in_features=1936, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=1936, bias=True)
          (norm1): LayerNorm((1936,), eps=1e-05, elementwise_affine=True)
          (norm2): LayerNorm((1936,), eps=1e-05, elementwise_affine=True)
          (dropout1): Dropout(p=0.1, inplace=False)
          (dropout2): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (global_attention): TransformerDecoder(
      (layers): ModuleList(
        (0): TransformerDecoderLayer(
          (multihead2): MultiheadAttention(
            (out_proj): NonDynamicallyQuantizableLinear(in_features=1936, out_features=1936, bias=True)
          )
          (linear1): Linear(in_features=1936, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=1936, bias=True)
          (norm3): LayerNorm((1936,), eps=1e-05, elementwise_affine=True)
          (dropout2): Dropout(p=0.1, inplace=False)
          (dropout3): Dropout(p=0.1, inplace=False)
        )
        (1): TransformerDecoderLayer(
          (multihead2): MultiheadAttention(
            (out_proj): NonDynamicallyQuantizableLinear(in_features=1936, out_features=1936, bias=True)
          )
          (linear1): Linear(in_features=1936, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=1936, bias=True)
          (norm3): LayerNorm((1936,), eps=1e-05, elementwise_affine=True)
          (dropout2): Dropout(p=0.1, inplace=False)
          (dropout3): Dropout(p=0.1, inplace=False)
        )
        (2): TransformerDecoderLayer(
          (multihead2): MultiheadAttention(
            (out_proj): NonDynamicallyQuantizableLinear(in_features=1936, out_features=1936, bias=True)
          )
          (linear1): Linear(in_features=1936, out_features=2048, bias=True)
          (dropout): Dropout(p=0.1, inplace=False)
          (linear2): Linear(in_features=2048, out_features=1936, bias=True)
          (norm3): LayerNorm((1936,), eps=1e-05, elementwise_affine=True)
          (dropout2): Dropout(p=0.1, inplace=False)
          (dropout3): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (position_embedding): Embedding(2, 1936)
  )
  (a_rel_compress): Linear(in_features=1936, out_features=3, bias=True)
  (s_rel_compress): Linear(in_features=1936, out_features=6, bias=True)
  (c_rel_compress): Linear(in_features=1936, out_features=17, bias=True)
)
```



# 代码记录分析

##### 加载预训练模型的参数：

```python
resnet = resnet101()
state_dict = torch.load(model_path)
resnet.load_state_dict({k:v for k,v in state_dict.items() if k in resnet.state_dict()})
```

model.eval() 在测试和验证时不改变模型的权重

###### 图像显示RGB

```python
        # 日常图片和PIL的颜色通道为RGB
        # matplot plt中图像保存格式是RGB
        # opencv读取图片的像素是BGR
        # caffe底层基于opencv 因此也是BGR
        # opencv拆分通道方法1：
        B,G,R=cv2.split(img)
        # opencv拆分通道方法2：
        # B = img[:,:,0] # 通道的第0个是B
        # G = img[:,:,1]
        # R = img[:,:,2
        # 颜色通道融合：
        # img2 = cv2.merge((B,G,R))
        # cv_show('merged',img2)
        # 只保留某个通道
        # 首先复制一张图像
        # img3 = img.copy() # 复制img
        # 只保留G通道
        # img3[:,:,0] = 0  # B通道为0
        # img3[:,:,2] = 0  # R通道为0
        # cv_show('G-channel',img3)
显示图像：
opencv.imshow()使用BGR，而matplotlib.pyplot 则是RGB模式
```

###### 镜像地址：

1、华南理工大学镜像源 http://pypi.hustunique.com/simple/%29
2、清华大学
https://pypi.tuna.tsinghua.edu.cn/simple
3、豆瓣
http://pypi.douban.com/simple/
4、清华大学开源镜像站
https://mirrors.tuna.tsinghua.edu.cn/
5、网易开源
http://mirrors.163.com/
6、华为
https://mirrors.huaweicloud.com/
7、阿里巴巴
https://opsx.alibaba.com/mirror/

###### 修改linux地址：

- 命令：nmtui
- 命令：nmcli connection up enp0s3

三维数据转4维数据：

```python
blob = np.zeros((num_images, max_shape[0], max_shape[1], 3),
                dtype=np.float32)
```

特征图可视化：

```python
 # feed image data to base model to obtain base feature map
        base_feat = self.RCNN_base(im_data)
        # 一个图像帧得到一个特征图(1024 50 38)
        # base_feat:10 1024 50 38
        # base_feat:4*1024*h*w
        for i in range(base_feat.shape[0]):
            feature = base_feat[i].detach().cpu().numpy()
            # im = np.squeeze(feature)
            feature = np.transpose(feature, [1, 2, 0])
            plt.figure()
            for i in range(12):
                ax = plt.subplot(3, 4, i + 1)
                plt.imshow(feature[:, :, 80*i])
                # 80*i表示打印的是第几个维度的，一共有1024维(channel)
                # img = feature[:, :, 1]
                # plt.savefig('img-{}.png'.format(i + 1))
                # save_image(torch.from_numpy(img), 'img-{}.png'.format(i + 20))
            plt.savefig('img85.png')
```



# 七月在线

precision：预测中准不准

recall：正确中能找回多少个

