# QR Code Detection and Decoding

Detects QR codes in document images and decodes them to JSON. The main script uses a **YOLOv8** model ([Ultralytics](https://github.com/ultralytics/ultralytics)) for detection and `pyzbar` for decoding; OpenCV handles image processing. Built for scanning QR codes on batches of converted PDF pages.

![QR_detect decode](https://github.com/srivatsavsurya/QR_Detect_Decode/assets/109732969/9cb8ed6b-0dcd-4d25-a4d1-7c75b312ac05)

## Scripts

| Script | What it does |
| --- | --- |
| `decode.py` | **Main script.** YOLOv8 (`best.pt`, 22 MB, included) detects each QR code, `pyzbar` decodes the crop, results print as JSON. |
| `crop.py` | Model-free alternative: finds QR-like contours with OpenCV thresholding and decodes them. |
| `convert_pdf_to_image.py` | Turns every PDF in `./PDFs` into enhanced page images in `./Images`. |
| `app.py` | Experiment: same pipeline with a PyTorch Faster R-CNN detector. |
| `model.py` | Experiment: TensorFlow SavedModel detector. |

## Setup

```sh
git clone https://github.com/srivatsavsurya/QR_Detect_Decode.git
cd QR_Detect_Decode
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

`pyzbar` needs the system `zbar` library (`apt install libzbar0` on Debian/Ubuntu), and `pdf2image` needs `poppler-utils`.

## Usage

To scan a folder of PDFs, put them in `./PDFs` first:

```sh
python3 convert_pdf_to_image.py
```

Then detect and decode QR codes in an image:

```sh
python3 decode.py Images/page-0001.png                 # YOLOv8
python3 crop.py Images/page-0001.png                   # OpenCV, no model needed
python3 app.py Images/page-0001.png --model <faster-rcnn-weights.pt>   # PyTorch experiment; needs its own weights, best.pt is YOLO
```

Each script also writes `cropped_qr_<n>.jpg` crops for inspection.

## JSON Output Format

```json
[
  {
    "data": "<decoded QR code data>",
    "type": "QRCODE",
    "rect": { "x": <x>, "y": <y>, "width": <w>, "height": <h> }
  }
]
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes.
