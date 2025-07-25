# Image Restoration using Knowledge Distillation

## Introduction

This project focuses on restoring blurred images using a knowledge distillation approach. A pre-trained teacher model (Restormer - Motion Deblurring) is used to guide a lightweight student CNN. The student model is designed to be lightweight and efficient, yet capable of producing high-quality restored images.

The training procedure involves using the output of the teacher model and the ground truth to help the student model learn better image reconstruction. A custom loss function combining multiple metrics is used to optimize the student model’s performance.

## Team Members

| Name                | Roll Number         |
|---------------------|---------------------|
| Sampath             | VU22CSEN0500075     |
| Hrishikesh           | VU22CSEN05000043    |
| Ravindranath Tagore | VU22CSEN0600109     |

**Mentor**: Dr. S. Anuradha

## Dataset and Project Video

- **Dataset Link**: [Google Drive](https://drive.google.com/drive/folders/195dmOS4l2ltLfIncxxar9D3vs-FO0kas?usp=sharing)
- **Project Demo Video**: [Google Drive](https://drive.google.com/drive/folders/1ewjKEJROSeblKg2HJc5VQg4oKnw3RbEU?usp=sharing)
- **Restored images**: [Google Drive](https://drive.google.com/drive/folders/1xX3VSRaYSGs8vrcJvxNhzvbw8ZQZWvCA?usp=sharing)

> ### **Note**
1. In the system architecture part of the video, the output image size is shown as 256×480, but the actual output size used during training and inference is **1920×1080**.  
2. The Input and ReLU layers are not explicitly shown in the architecture diagram.  
3. The dataset containing **5200 images** is used exclusively for **training**, while the **validation dataset with 200 images** is used solely for **testing** the model.

## System Architecture

### Preprocessing
- All images are resized to **1920×1080**.
- Each image is split into four equal parts: top-left, top-right, bottom-left, bottom-right.
- Blurred images are generated by downscaling and upscaling to simulate real-world degradation.

### Teacher Model
- The teacher model used is **Restormer (Motion Deblurring)** with pre-trained weights.
- It generates high-quality deblurred images used as guidance for training the student model.
- Achieved SSIM score: **0.8838**

### Student Model
A custom lightweight CNN designed with:
- **Encoder**: Conv → ReLU → MaxPool
- **Middle Block**: Conv → ReLU
- **Decoder**: Upsample → Conv → ReLU → Sigmoid

> Input and output images throughout the model maintain the original size of **1920×1080**.

### Training Details
- **Training Method**: Knowledge Distillation
- **Sources of Learning**:
  - Ground Truth Images
  - Teacher Model Outputs

### Training Configuration
- **Batch Size**: 32  
- **Epochs**: 10  
- **Optimizer**: Adam  
- **Learning Rate**: 1e-4  

## Loss Function

The custom **Distillation Loss** used is a weighted combination of:

- **L1 Loss**
- **SSIM Loss**
- **VGG-based Feature Loss**

These help the student model learn accurate structures and perceptual quality.

## Results Summary

- The **student model** achieved an average SSIM score of **0.9023**, outperforming the teacher model's score of **0.8838**.
- The student network restored sharper and cleaner images with fewer parameters and faster inference.

## Technologies Used

- Python 3
- PyTorch
- torchvision
- OpenCV
- PIL (Pillow)
- pytorch-msssim
- Google Colab

