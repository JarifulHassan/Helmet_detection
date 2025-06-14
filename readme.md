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

###  Data Format

* Annotation format: **YOLO** (each line: `class x_center y_center width height`)
* All bounding boxes are labeled with **class `0`** (helmet).

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

nc: 1
names: ['helmet']
```

---

###  Training

To train the model:

```python
from ultralytics import YOLO

model = YOLO('yolov8n.pt')  # or yolov8s.pt for better accuracy
model.model.names = ['helmet']  # optional, for clarity
model.train(data='data.yaml', epochs=25, imgsz=640)
```

---

### Inference

```python
results = model('path/to/image.jpg', show=True)
```

---

###  Cleaning Labels (if needed)

To force all class labels to be `0`, run this script:

```python
import os

label_dir = 'data/labels'

for root, dirs, files in os.walk(label_dir):
    for file in files:
        if file.endswith('.txt'):
            path = os.path.join(root, file)
            with open(path, 'r') as f:
                lines = f.readlines()
            with open(path, 'w') as f:
                for line in lines:
                    parts = line.strip().split()
                    if parts:
                        parts[0] = '0'
                        f.write(' '.join(parts) + '\n')
```

---

###  Author

**Jariful Hassan**
MSc Applied Mathematics, South Asian University
Email: [jariful076@gmail.com](mailto:jariful076@gmail.com)
LinkedIn: [@jariful-hassan](https://www.linkedin.com/in/jariful-hassan-69142424a/)


