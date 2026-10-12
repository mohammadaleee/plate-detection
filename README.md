# Design and Implementation of a Persian License Plate Recognition System Using Deep Learning

## 1. Introduction and Project Objective

The objective of this project is to develop a computer vision system for detecting and recognizing Iranian vehicle license plates. The system combines deep learning and image processing techniques to identify the plate's corner points, correct perspective distortion, recognize individual characters, and store the extracted information in a database.

## 2. License Plate Keypoint Detection Using YOLO

In the first stage, a trained YOLO keypoint detection model is used to identify the four corner points of the license plate in the input image. The coordinates of these points are extracted and used in the subsequent image rectification stage.

## 3. License Plate Perspective Correction

Due to camera angles, vehicle positioning, and imaging conditions, a license plate may appear tilted or geometrically distorted. To address this issue, a perspective transformation is applied.

First, a transformation matrix is calculated using the coordinates of the detected corner points. The transformation is then applied to convert the plate into a rectangular image with dimensions of 400 × 100 pixels. This process produces a more standardized image for subsequent processing.

## 4. Character Segmentation

After perspective correction, the regions corresponding to the digits and the letter on the license plate are extracted using predefined coordinates. In the current implementation, character segmentation is performed using fixed image regions.

The purpose of this stage is to prepare individual character images for classification by the convolutional neural network.

## 5. Character Recognition Using a Convolutional Neural Network

A Convolutional Neural Network (CNN) is used to recognize the digits and letters on the license plate. The network extracts visual features from each character image and classifies it into one of the predefined character classes.

Before classification, each character image is converted to grayscale and resized to 32 × 32 pixels. The trained model then predicts the most likely class for each character.

In this implementation, the CNN recognizes characters individually rather than predicting the entire license plate text directly.

## 6. License Plate Text Reconstruction

After individual characters have been recognized, their predictions are arranged according to their positions on the license plate. The digits and letter are extracted from the corresponding predictions and combined to reconstruct the plate's textual identifier.

The accuracy of this stage depends on the quality of character segmentation, the ordering of the detected corner points, and the performance of the character classification model.

## 7. Database Storage Using SQLite

SQLite is used to store the recognition results. In the current implementation, the extracted plate information is stored in two fields: the numerical portion and the letter.

This allows recognized license plates to be recorded and retrieved for future analysis or application development.

## 8. Result Visualization and System Development

The implementation supports displaying the rectified license plate, the segmented character images, and the character classification results.

An initial video-processing section has also been prepared in the code. Once enabled and tested, it can be extended to process video frames or live camera input, allowing the system to recognize license plates from video streams.

## 9. Current Limitations

One limitation of the current implementation is the use of fixed coordinates for character segmentation. This approach may not perform reliably when license plates vary in size, position, spacing, or alignment.

Furthermore, errors in corner-point detection or character classification can affect the final recognition result.

Potential improvements include developing a more flexible character segmentation method, evaluating the system on a separate test dataset, and measuring performance using metrics such as Character Error Rate (CER) and exact plate recognition accuracy.

## 10. Conclusion

This project implements a license plate recognition pipeline consisting of YOLO-based keypoint detection, perspective correction, character segmentation, CNN-based character classification, text reconstruction, and SQLite database storage.

The resulting system serves as a prototype for Persian license plate recognition and provides a foundation for future improvements, including more robust character segmentation, quantitative performance evaluation, and real-time video processing.