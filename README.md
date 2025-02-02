# QR Code Detection with YOLOv8 and OpenCV

This project uses YOLOv8 for detecting QR codes in images and OpenCV for image processing. The detected QR codes are then decoded using the `pyzbar` library, and the results are output in JSON format.

## Introduction

This project uses a YOLOv8 model to detect QR codes in images and OpenCV to preprocess the images. Detected QR codes are then decoded using the `pyzbar` library.

![QR_detect decode](https://github.com/srivatsavsurya/QR_Detect_Decode/assets/109732969/9cb8ed6b-0dcd-4d25-a4d1-7c75b312ac05)


## Features

- Detect QR codes in images using a YOLOv8 model.
- Preprocess images using OpenCV.
- Decode QR codes using `pyzbar`.
- Output results in JSON format.

## Installation

### Prerequisites

- Git
- Python 3.6+

### Clone the Repository

```sh
git clone https://github.com/srivatsavsurya/qr-detect-decode.git
cd qr-detect-decode
```
### Set Up Virtual Environment

It's recommended to use a virtual environment to manage dependencies.
```sh
pip install -r requirements.txt
```
### Download the YOLOv8 Model
Place the best.pt model file in the project directory. You can train your model using Roboflow.

### Usage

#### if you have a bunch of pdf, create a folder ./Images and ./PDFs
and run
```sh
python3 convert_pdf_to_image.py
```

#### Run the script with an image:

##### To use tf model and detect the QR
```sh
python detect.py --image_path <path/to/your/image.jpg>
```

##### To use open-cv2
```sh
python crop.py --image_path <path/to/your/image.jpg>
```


## JSON Output Format
The output is a JSON array containing objects with the following structure:
```json
[
  {
    "bounding_box": {
      "x": <x-coordinate>,
      "y": <y-coordinate>,
      "width": <width>,
      "height": <height>
    },
    "data": "<decoded QR code data>"
  }
]
```

## Contributing
Contributions are welcome! Please open an issue or submit a pull request for any changes.
