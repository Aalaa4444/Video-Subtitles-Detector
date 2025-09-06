# Video-Subtitles-Detector

## Overview
The Video Subtitles Detector is designed to detect and highlight subtitles within a video. It identifies the area containing the subtitles by drawing bounding boxes around them and further detects the location of each word within the subtitles. The program processes the video using basic filters and morphological operations, without relying on deep learning, machine learning, or OCR techniques.

## Features
* Frame Extraction: Extracts frames from a video file and saves them in different formats.
* Preprocessing: Converts frames to grayscale, applies Gaussian blur, and thresholding.
* Subtitle Segmentation: Detects and highlights subtitle areas using different morphological techniques.
  * Draw red bounding boxes around each line of subtitles.
  * Draw green bounding boxes around each word within the subtitles.
  * Process and apply bounding boxes to all subtitles in the video.
* Video Reconstruction: Compiles segmented frames into a new video file.
## Installation
Ensure you have Python installed along with the required libraries. You can install the necessary libraries using pip:

```bash
    pip install numpy opencv-python matplotlib
```
## Usage
1- Place your <a href="https://drive.google.com/file/d/1mUOdZbcvRS_UTIoi4wGdfp9i8pNl3fYM/view" target="_blank">video</a>  file in the main directory if you will use jupyter or in src file if you will run python files .

2- Modify the base_directory variable to specify where you want to save the output frames and video.

3- Execute video_processing.py to process the video. It will:

* Create directories for storing frames and processed data.
* Extract frames from the video.
* Perform preprocessing on each frame.
* Apply text segmentation techniques.
* Save segmented frames and compile them into a new video.
```bash
    python video_processing.py
```
## Output Examples
<p >     
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output.png" width="400">     
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output2.png" width="400">
</p>
<p >     
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output3.png" width="400">
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output4.png" width="400">
</p>
<p > 
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output5.png" width="400">
    <img src="https://github.com/Aalaa4444/Video-Subtitles-Detector/blob/main/output_examples/output6.png" width="400">
</p>

## Advanced Features
1. Advanced Text Detection
Optical Character Recognition (OCR): Integrate OCR to extract the actual text from the segmented regions.

```bash
import pytesseract

def extract_text_from_frame(frame):
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    text = pytesseract.image_to_string(gray)
    return text
Deep Learning Models: Use pre-trained deep learning models like EAST or CRNN for more accurate text detection.
```
2. Subtitles Extraction and Formatting
Subtitle Files: Format extracted text into subtitle files (e.g., SRT format).

```bash
def save_subtitles_as_srt(subtitles, output_filename):
    with open(output_filename, 'w') as f:
        for i, (start_time, end_time, text) in enumerate(subtitles):
            f.write(f"{i + 1}\n")
            f.write(f"{start_time} --> {end_time}\n")
            f.write(f"{text}\n\n")
```
3. Video Analytics
Statistics and Analytics: Analyze video content for word counts, subtitle duration, and frequency.

```bash
def analyze_subtitles(subtitles):
    word_counts = {}
    for _, _, text in subtitles:
        words = text.split()
        for word in words:
            word_counts[word] = word_counts.get(word, 0) + 1
    return word_counts
```
4. User Interface
GUI Application: Develop a GUI using Tkinter or PyQt.

```bash
from tkinter import Tk, Label, Button, filedialog

def browse_file():
    filename = filedialog.askopenfilename()
    print(f"Selected file: {filename}")

root = Tk()
root.title("Video Subtitle Segmentation")

Label(root, text="Select a video file").pack()
Button(root, text="Browse", command=browse_file).pack()

root.mainloop()
```
5. Batch Processing
Multiple Videos: Process multiple videos in a batch.

```bash
def process_videos(video_files):
    for video_file in video_files:
        # Process each video file
        pass
```
6. Integration with Other Tools
Integration with Media Players: Create plugins for media players like VLC.

API Integration: Build an API with Flask or FastAPI.

```bash
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/segment', methods=['POST'])
def segment_video():
    video_file = request.files['video']
    # Process the video and return results
    return jsonify({'status': 'success'})

if __name__ == '__main__':
    app.run(debug=True)
```
7. Performance Optimization
Parallel Processing: Speed up frame processing with parallel processing.

```bash
from concurrent.futures import ThreadPoolExecutor

def process_frame(frame):
    # Processing logic here
    pass

with ThreadPoolExecutor() as executor:
    results = list(executor.map(process_frame, frames))
```

## Contributing
Contributions are welcome! Please open an issue or submit a pull request if you have improvements or bug fixes.

## Acknowledgments
OpenCV for image processing.
NumPy for numerical operations.
Matplotlib for visualization.
