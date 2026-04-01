# Pothole Detection using YOLOv8

## Overview

This project focuses on detecting potholes on road surfaces using a deep learning-based object detection model built with YOLOv8. The model is trained on a custom dataset and evaluated using standard computer vision metrics.

---

## Features

* Custom pothole detection model using YOLOv8
* Training and evaluation pipeline
* Real-time detection using webcam
* Performance analysis using metrics such as loss, precision, recall, and mAP

---

## Technologies Used

* Python
* OpenCV
* Ultralytics YOLOv8
* PyTorch

---

## Dataset

The model is trained on a custom pothole dataset.

**Dataset Structure:**

```
dataset/
│
├── train/
│   ├── images/
│   ├── labels/
│
├── valid/
│   ├── images/
│   ├── labels/
```

> Note: Large datasets are not included in this repository.

---

## Training

To train the model:

```bash
yolo detect train model=yolov8n.pt data=data.yaml epochs=50 imgsz=640
```

---

## Evaluation

To evaluate the model:

```bash
yolo detect val model=runs/detect/train/weights/best.pt data=data.yaml
```

### Metrics Used:

* **Loss** (box_loss, cls_loss, dfl_loss)
* **Precision**
* **Recall**
* **mAP@50**
* **mAP@50-95**

---

## Results

* mAP@50: ~0.70
* mAP@50-95: ~0.35
* Precision: ~0.78
* Recall: ~0.60

These results indicate that the model performs well in detecting potholes but can be improved in terms of bounding box accuracy.

---

## Inference

To run prediction on an image:

```bash
yolo detect predict model=runs/detect/train/weights/best.pt source="test.jpg"
```

---

## Real-Time Detection

```python
from ultralytics import YOLO
import cv2

model = YOLO("best.pt")
cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    results = model(frame)
    annotated = results[0].plot()

    cv2.imshow("Pothole Detection", annotated)

    if cv2.waitKey(1) == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

---

## Future Improvements

* Increase dataset size and diversity
* Improve annotation quality
* Train for more epochs
* Use larger YOLO models (yolov8s, yolov8m)
* Optimize for real-time performance

---

## Repository Structure

```
project/
│
├── dataset_sample/
├── outputs/
├── runs/
├── data.yaml
├── train.py
├── README.md
```

---

## Acknowledgements

* Ultralytics YOLOv8
* OpenCV community

---

## Author

Midhun P Jose
