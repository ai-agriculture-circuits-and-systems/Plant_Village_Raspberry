# Plant Village Raspberry

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-green?logo=creativecommons&logoColor=white)](https://creativecommons.org/licenses/by/4.0/)
[![Version](https://img.shields.io/badge/version-1.0.0-blue?logo=semver&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry)
[![GitHub stars](https://img.shields.io/github/stars/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Stars&color=orange&labelColor=orange&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry)
[![GitHub forks](https://img.shields.io/github/forks/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Forks&color=yellow&labelColor=yellow&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry)
[![GitHub watchers](https://img.shields.io/github/watchers/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Watchers&color=cyan&labelColor=cyan&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry)
[![GitHub issues](https://img.shields.io/github/issues/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Issues&color=red&labelColor=red&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=PRs&color=lime&labelColor=lime&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry/pulls)
[![GitHub contributors](https://img.shields.io/github/contributors/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Contributors&color=purple&labelColor=purple&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry/graphs/contributors)
[![GitHub last commit](https://img.shields.io/github/last-commit/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry?style=flat&logo=github&label=Last%20Commit&color=gray&labelColor=gray&logoColor=white)](https://github.com/ai-agriculture-circuits-and-systems/Plant_Village_Raspberry/commits)

Raspberry leaf classification dataset from Plant Village. Contains images of healthy raspberry leaves. This dataset follows the standardized layout specification.

- **Project page**: `https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset`
- **Original paper**: `https://arxiv.org/abs/1511.08060`
- **Dataset repository**: `https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset`

## TL;DR

- **Task**: Classification, Object Detection
- **Modality**: RGB
- **Platform**: Ground
- **Real/Synthetic**: Real
- **Images**: Labeled images (see Stats and Splits section)
- **Classes**: 1 category
  - `healthy`: Healthy raspberry leaves
- **Resolution**: 256×256 pixels
- **Annotations**: COCO JSON (object detection with bounding boxes)
- **Total annotations**: One per image for classification (full-image bounding boxes)
- **License**: CC BY 4.0 (see LICENSE)
- **Citation**: See below

## Table of Contents
- [Download](#download)
- [Dataset Structure](#dataset-structure)
- [Sample Images](#sample-images)
- [Annotation Schema](#annotation-schema)
- [Stats and Splits](#stats-and-splits)
- [Quick Start](#quick-start)
- [Evaluation and Baselines](#evaluation-and-baselines)
- [Datasheet (Data Card)](#datasheet-data-card)
- [Known Issues and Caveats](#known-issues-and-caveats)
- [License](#license)
- [Citation](#citation)
- [Changelog](#changelog)
- [Contact](#contact)

## Download

- **Original dataset**: `https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset`
- **This repository**: Hosts structure and conversion scripts only; place the downloaded folders under this directory.
- **Local license file**: See `LICENSE` (CC BY 4.0).

## Dataset Structure

This dataset follows the standardized dataset structure specification with subcategory organization:

```
Plant_Village_Raspberry/
├── raspberries/
│   ├── healthy/              # Healthy images
│   │   ├── csv/              # CSV annotations per image
│   │   ├── json/             # Original JSON annotations
│   │   ├── images/           # Healthy images
│   │   └── sets/             # Dataset splits for this subcategory (optional)
│   │       ├── train.txt
│   │       ├── val.txt
│   │       ├── test.txt
│   │       └── all.txt
│   ├── labelmap.json        # Label mapping
│   └── sets/                 # Combined dataset splits
│       ├── train.txt
│       ├── val.txt
│       ├── test.txt
│       └── all.txt
├── annotations/              # COCO format JSON (generated)
│   ├── raspberries_instances_train.json
│   ├── raspberries_instances_val.json
│   └── raspberries_instances_test.json
├── scripts/
│   └── convert_to_coco.py   # COCO conversion script
├── LICENSE
├── README.md
└── requirements.txt
```

- Splits: `raspberries/sets/*.txt` list image basenames (no extension). If missing, all images are used.

## Sample Images

Below are example images for each category in this dataset. Paths are relative to this README location.

<table>
  <tr>
    <th>Category</th>
    <th>Sample</th>
  </tr>
  <tr>
    <td><strong>Healthy</strong></td>
    <td>
      <img src="raspberries/healthy/images/sample.jpg" alt="healthy" width="260"/>
      <div align="center"><code>raspberries/healthy/images/sample.jpg</code></div>
    </td>
  </tr>
</table>

## Annotation Schema

- **CSV per-image schema** (stored under `raspberries/{subcategory}/csv/` folder):
  - Columns: `item, x, y, width, height, label`
  - Coordinates: `(x, y)` is top-left corner, `width` and `height` in pixels
  - Label: category ID (from labelmap.json)
  - Example:
    ```csv
    #item,x,y,width,height,label
    0,0,0,256,256,1
    ```
  
- **COCO-style** (generated):

```json
{
  "info": {...},
  "images": [
    {
      "id": 1,
      "file_name": "{category}/{subcategory}/images/image.jpg",
      "width": 256,
      "height": 256
    }
  ],
  "annotations": [
    {
      "id": 1,
      "image_id": 1,
      "category_id": 1,
      "bbox": [0, 0, 256, 256],
      "area": 65536,
      "iscrowd": 0
    }
  ],
  "categories": [
    {
      "id": 1,
      "name": "healthy",
      "supercategory": "plant"
    }
  ]
}
```

- **Label maps**: `raspberries/labelmap.json` defines the category mapping:

```json
[
  {
    "object_id": 0,
    "label_id": 0,
    "keyboard_shortcut": "0",
    "object_name": "background"
  },
  {
    "object_id": 1,
    "label_id": 1,
    "keyboard_shortcut": "1",
    "object_name": "healthy"
  }
]
```

## Stats and Splits

- **Total images**: See subcategory counts below
- **Splits**: train/val/test (default: 60%/20%/20%)
- **Splits provided via** `raspberries/sets/*.txt`. You may define your own splits by editing those files.

## Quick Start

### Using COCO API

```python
from pycocotools.coco import COCO
import json

# Load COCO annotations
coco = COCO('annotations/raspberries_instances_train.json')

# Get all image IDs
img_ids = coco.getImgIds()
print(f"Total images: {len(img_ids)}")

# Get all category IDs
cat_ids = coco.getCatIds()
categories = [coco.loadCats([id])[0]['name'] for id in cat_ids]
print(f"Categories: {categories}")

# Load a specific image and its annotations
img_id = img_ids[0]
img_info = coco.loadImgs([img_id])[0]
ann_ids = coco.getAnnIds(imgIds=[img_id])
anns = coco.loadAnns(ann_ids)

print(f"Image: {img_info['file_name']}")
print(f"Size: {img_info['width']}x{img_info['height']}")
print(f"Annotations: {len(anns)}")
```

### Converting to COCO format

If you need to regenerate COCO annotations from CSV files:

```bash
python scripts/convert_to_coco.py --root . --out annotations --splits train val test
```

### Dependencies

**Required**:
- `Pillow>=9.5` (for image processing)

**Optional**:
- `pycocotools>=2.0.7` (for COCO API)

Install with:
```bash
pip install -r requirements.txt
```

## Evaluation and Baselines

- **Primary metric**: 
  - Classification: Accuracy, Precision, Recall, F1-score (per class and macro-averaged)
  - Object Detection: mAP@[.50:.95], mAP@.50, mAP@.75
- **Baseline results**: See original Plant Village paper

## Datasheet (Data Card)

### Motivation

This dataset was created to support research in plant disease detection and classification, specifically for raspberry leaf classification, which is crucial for automated disease detection in agricultural applications.

### Composition

The dataset consists of:
- **Image types**: RGB images of raspberry leaves
- **Categories**: 1 class (healthy)
- **Annotation format**: Image-level classification annotations (via full-image bounding boxes) and object-level detection annotations

### Collection Process

- **Source**: Images collected from various sources and manually labeled by experts
- **Annotation tool**: Images annotated for classification and detection tasks
- **Validation**: Images resized to 256×256 pixels

### Preprocessing

- Images resized to 256×256 pixels
- Annotations converted to bounding box format
- Dataset split into train/val/test sets

### Distribution

- Dataset is distributed under CC BY 4.0 license
- Original data available from Plant Village dataset
- This repository provides standardized structure and conversion scripts

### Maintenance

- Dataset structure has been standardized according to the dataset structure specification
- COCO format annotations are generated from CSV files using the provided conversion script

## Known Issues and Caveats

- Images are preprocessed to 256×256 pixels
- Some images may have multiple bounding boxes (for detection task)
- Coordinate system: top-left origin (0,0), pixel units
- File naming: image basenames (without extension) are used in split files

## License

This dataset is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

Check the original dataset terms and cite appropriately.

See `LICENSE` file for full license text.

## Citation

If you use this dataset, please cite:

```bibtex
@article{mohanty2016using,
  title={Using Deep Learning for Image-Based Plant Disease Detection},
  author={Mohanty, Sharada P. and Hughes, David P. and Salathé, Marcel},
  journal={Frontiers in Plant Science},
  volume={7},
  pages={1419},
  year={2016},
  publisher={Frontiers Media SA}
}
```

## Changelog

- **V1.0.0** (2025): Initial standardized structure and COCO conversion utility

## Contact

- **Maintainers**: Open to contributions via issue tracker
- **Original authors**: Plant Village Contributors (David Hughes, Marcel Salathé)
- **Source**: `https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset`
