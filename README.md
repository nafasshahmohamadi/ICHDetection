# Intracranial Hemorrhage Detection from Brain CT Slices Using Deep Learning

> **Bachelor's thesis --- Electrical Engineering (Control)**\
> **Supervisor:** Dr. Mehdi Aliyari Shoorehdeli\
> **Defense:** Shahrivar 1404 (2025)

This repository contains selected code and experiments from a bachelor's
thesis on detecting intracranial hemorrhage (ICH) in brain CT scan
slices using deep learning. The work evaluates YOLO-based detection
models and uses Segment Anything Model 2.1 (SAM 2.1) for additional
segmentation and qualitative analysis.

> **Research disclaimer:** This project is an academic research project,
> not a clinically validated diagnostic system. Its outputs must not be
> used as a substitute for assessment by qualified medical
> professionals.

## Overview and Abstract

Intracranial hemorrhage is a potentially life-threatening condition for
which timely and accurate interpretation of brain computed tomography
(CT) scans is important. Subtle hemorrhagic findings can be difficult to
identify, motivating research into computer-assisted analysis of CT
images.

This project investigates deep-learning-based detection of intracranial
hemorrhage in individual brain CT slices. YOLOv8 and YOLOv11 are used as
base detection-model families. The workflow also explores oriented
bounding boxes (OBB) and a custom data-augmentation technique,
**RandomWindowing**, intended to improve the visibility and detection of
subtle findings. SAM 2.1 is used for further segmentation-oriented and
qualitative analysis.

The project focuses on comparing approaches and examining how
preprocessing, augmentation, object localization, and segmentation can
contribute to the analysis of brain CT images. Quantitative conclusions
should be interpreted in the context of the dataset, evaluation
protocol, and experimental results reported in the thesis.

## Key Innovations and Techniques

### Oriented Bounding Boxes (OBB)

Oriented bounding boxes represent localized findings with rotated boxes
rather than restricting every annotation to an axis-aligned rectangle.
In this project, OBB-based detection is explored for localizing
hemorrhagic regions in CT slices. The exact benefit depends on
annotation quality, the geometry of the target regions, and the
evaluation setup.

### Custom RandomWindowing Augmentation

**RandomWindowing** is a custom data-augmentation approach designed to
vary CT windowing during training. CT windowing changes how
Hounsfield-unit values are mapped to image intensity, which can affect
the visibility of structures and subtle abnormalities.

The aim is to expose the detector to useful variations in image contrast
and brightness so that subtle hemorrhagic findings may be easier to
learn. The implementation and its parameters should be taken from the
code in this repository; no performance gain is assumed without
supporting experimental results.

### Detection and Segmentation Analysis

-   **YOLOv8 and YOLOv11:** evaluated as base object-detection model
    families.
-   **SAM 2.1:** used for additional segmentation and qualitative
    examination of selected regions.
-   **Comparative experimentation:** investigates model and
    preprocessing choices within the thesis workflow.

## Models and Workflow

The high-level workflow is:

1.  **CT slice preparation** --- load and prepare brain CT slices and
    their corresponding annotations.
2.  **Preprocessing** --- apply the image preparation and CT windowing
    steps used by the experiment.
3.  **Data augmentation** --- apply the custom RandomWindowing technique
    and any other augmentations configured for the experiment.
4.  **Detection model training** --- train and evaluate YOLOv8 and
    YOLOv11 models using the relevant annotation format, including OBB
    where configured.
5.  **Evaluation and comparison** --- compare model outputs using the
    metrics and evaluation procedure defined in the experiments.
6.  **Segmentation and qualitative analysis** --- use SAM 2.1 to inspect
    selected regions and explore segmentation-oriented results.
7.  **Result review** --- review predictions and visualizations
    alongside the thesis findings.

### High-level architecture

``` text
Brain CT slices + annotations
            |
            v
Preprocessing / CT windowing
            |
            v
RandomWindowing augmentation
            |
            v
YOLOv8 / YOLOv11 detection
       (OBB where configured)
            |
            v
Evaluation and comparison
            |
            v
Selected regions -> SAM 2.1
            |
            v
Segmentation and qualitative review
```

## Repository Contents

The repository currently contains selected notebooks and experiments
from the thesis. The structure may evolve as the work is organized.

``` text
.
├── notebooks and experiment files
├── README.md
└── requirements.txt          # if included in this repository
```

Not every experiment or supporting file is necessarily included. Dataset
files may be excluded because of size, access restrictions, licensing,
or privacy considerations.

## Technology Stack

-   **Language:** Python
-   **Deep learning:** PyTorch
-   **Object detection:** YOLOv8, YOLOv11
-   **Segmentation and qualitative analysis:** SAM 2.1
-   **Image processing:** OpenCV
-   **Numerical computing:** NumPy

## Installation

The commands below are a starting point. Adapt the repository URL,
environment setup, and dependency installation to the files actually
included in this repository.

### 1. Clone the repository

``` bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
```

### 2. Create and activate a virtual environment (recommended)

**Windows --- Command Prompt:**

``` bat
python -m venv .venv
.venv\Scripts\activate.bat
```

**macOS / Linux:**

``` bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

If a `requirements.txt` file is present:

``` bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If the repository does **not** yet include `requirements.txt`, install
dependencies according to the individual notebook or experiment
instructions. Do not assume that one generic dependency list will cover
every YOLO and SAM 2.1 experiment. Check the official installation
instructions for the relevant model versions, PyTorch, and hardware/CUDA
configuration.

## Usage

The repository currently provides selected experiment notebooks. Open a
notebook in Jupyter, VS Code, or Google Colab and follow its cells in
order.

1.  Clone or download the repository.
2.  Review the notebook's first cells for expected dependencies, paths,
    and configuration.
3.  Obtain the dataset separately, if it is not included, and place it
    where the notebook expects it.
4.  Update dataset and checkpoint paths for your environment.
5.  Run the preprocessing, training, evaluation, or visualization cells
    relevant to that experiment.

Because exact script names and notebook paths can vary, this README
intentionally does not prescribe a specific `train.py` command. Add
notebook-specific commands here once the final repository structure and
entry points are settled.

## Dataset, Reproducibility, and Results

-   **Dataset:** Add the dataset name, source, access requirements, and
    citation here when these details are ready to be shared.
-   **Splits and evaluation:** Document the train/validation/test split
    policy and evaluation metrics used in the thesis.
-   **Model configurations:** Record model variants, image sizes,
    hyperparameters, random seeds, and relevant software/hardware
    versions when available.
-   **Results:** Add a concise table of the actual experimental metrics
    from the thesis or saved evaluation outputs. Do not report estimated
    or unverified numbers.
-   **Reproducibility:** Ensure that paths, dependencies, preprocessing
    steps, annotation formats, and model checkpoints are documented
    sufficiently for another researcher to reproduce the experiments.

## Limitations and Responsible Use

This repository is intended for educational and research purposes.
Performance can vary with the dataset, annotation quality, scanner
settings, patient population, preprocessing choices, and evaluation
protocol. Results from a limited dataset may not generalize to other
clinical settings.

The models and visualizations have not been established here as a
replacement for radiologist review or as a clinically validated
diagnostic device. Do not use the outputs to make patient-care
decisions.

## Citation

If you use or discuss this work, please cite the thesis. Replace the
placeholders below with the author's name and university details before
publication.

``` bibtex
@thesis{<author_surname>2025ich,
  author       = {<Author Full Name>},
  title        = {Intracranial Hemorrhage Detection Using Brain CT Scan Slices and Deep Learning},
  type         = {Bachelor's thesis},
  institution  = {<University Name>},
  department   = {Electrical Engineering, Control},
  year         = {2025},
  month        = {September},
  note         = {Supervisor: Dr. Mehdi Aliyari Shoorehdeli}
}
```

**Persian title:** تشخیص خونریزی داخل جمجمه‌ای با استفاده از برش‌های
تصاویر CT Scan مغز و یادگیری عمیق

## Acknowledgments

This work was completed as a bachelor's thesis in Electrical Engineering
(Control), under the supervision of **Dr. Mehdi Aliyari Shoorehdeli**,
and defended in **Shahrivar 1404 (2025)**.

------------------------------------------------------------------------

*This README describes the intended research workflow. Update the
repository structure, setup instructions, dataset details, and results
as the code and documentation are finalized.*
