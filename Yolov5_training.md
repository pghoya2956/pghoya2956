

```python
from google.colab import drive
drive.mount('/content/gdrive', force_remount=True)
```


```python
cd /content/gdrive/MyDrive/Colab/Yolov5/yolov5/
```


```python
!git clone https://github.com/ultralytics/yolov5  # clone repo
%cd yolov5
%pip install -qr requirements.txt  # install dependencies
```


```python
%pip install -qr requirements.txt  # install dependencies
```


```python
%pip install wandb
```


```python
%pip install nbconvert
```


```python
!curl -L "https://public.roboflow.com/ds/6VwdOguyZI?key=otvxJV3YcL" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip
```


```python
cat dataset_Mask_Wearing/data.yaml
```


```python
%cd /
from glob import glob

train_img_list = glob('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/train/images/*.jpg')
test_img_list = glob('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/test/images/*.jpg')
valid_img_list = glob('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/valid/images/*.jpg')

print(len(train_img_list))
print(len(test_img_list))
print(len(valid_img_list))
```


```python
with open('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/train.txt', 'w') as f:
    f.write('\n'.join(train_img_list) + '\n')

with open('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/val.txt', 'w') as f:
    f.write('\n'.join(valid_img_list) + '\n')
```


```python
import yaml

with open('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/data.yaml', 'r') as f:
    data = yaml.load(f)

print(data)

data['train'] = '/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/train.txt'
data['val'] = '/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/val.txt'

with open('/content/gdrive/MyDrive/Colab/Yolov5/yolov5/dataset_Mask_Wearing/data.yaml', 'w') as f:
    yaml.dump(data, f)

print(data)
```


```python
cd /content/gdrive/MyDrive/Colab/Yolov5/yolov5
```


```python
!python train.py --img 416 --batch 16 --epochs 300 --data dataset_Mask_Wearing/data.yaml --cfg ./models/yolov5l.yaml --weights yolov5l.pt --name dataset_Mask_Wearing_yolov5x_results2
```


```python
!python detect.py
```


```python
!jupyter nbconvert --to markdown Yolov5_training.ipynb
```
