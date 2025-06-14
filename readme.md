##  Helmet Detection Using YOLOv8

This project uses **YOLOv8** from the **Ultralytics** library to detect helmets in images and videos. It is a custom object detection model trained on a single class: **helmet**.

---

###  Project Structure

```
Helmet-Detection-YOLOv8/
├── data/
│   ├── images/
│   │   ├── train/
│   │   ├── val/
│   └── labels/
│       ├── train/
│       └── val/
├── data.yaml
├── train.py
├── README.md
```

---

###  Dependencies

Make sure you have the following installed (preferably in a virtual environment):

```bash
pip install ultralytics
pip install opencv-python
```

Or create a conda environment:

```bash
conda create -n helmet_env python=3.9 -y
conda activate helmet_env
pip install ultralytics opencv-python
```

---

###  Data/Data Format
* data link:https://www.kaggle.com/datasets/andrewmvd/helmet-detection
* Annotation format: **YOLO** (each line: `class x_center y_center width height`)
* All bounding boxes are labeled with **class `0`** (helmet).
* * All bounding boxes are labeled with **class `1`** (without helmet).

Example (label `.txt`):

```
0 0.138750 0.496255 0.132500 0.205993
0 0.393750 0.411985 0.177500 0.329588
```

---

###  `data.yaml` Example

```yaml
path: data
train: images/train
val: images/val
names:
  0: With Helmet
  1: Without Helmet
  2: Head
```

---

###  Training

To train the model:

```python
from ultralytics import YOLO
model = YOLO('yolov8n.yaml')
model.model.nc = 3
model.model.names = ['With Helmet', 'Without Helmet', 'Head']
# Now train it with your dataset
model.train(data='data/data.yaml', epochs=25, imgsz=640)
```

###  Author

**Jariful Hassan**
MSc Applied Mathematics, South Asian University
Email: [jariful076@gmail.com](mailto:jariful076@gmail.com)
LinkedIn: [@jariful-hassan](https://www.linkedin.com/in/jariful-hassan-69142424a/)


