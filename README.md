# GAN-Based MRI Image Translation: T1 to T2 Modality

Magnetic Resonance Imaging (MRI) is widely used in medical diagnosis, with different modalities like T1-weighted and T2-weighted scans providing complementary information about tissues. However, acquiring both types of scans for every patient can be time-consuming, costly, and may not always be feasible.

This experiment presents a deep learning-based approach using a CycleGAN model to translate T1-weighted MRI images into T2-weighted images. By doing so, it aims to reduce the need for multiple scan sessions while preserving important anatomical and diagnostic details.


## Table of Contents
- [Objective of the Experiment](#objective-of-the-experiment)
- [Dataset](#dataset)
- [Workflow](#workflow)
- [Results](#results)
- [Future Direction](#future-direction)



## Objective of the Experiment
To train a GAN-based model capable of synthesizing realistic T2-weighted MRI images from T1-weighted inputs, without requiring perfectly aligned image pairs. This experiment is useful during the following situations: 
1. Cross-Modality Translation: Enables inference of T2-weighted scans from T1-only datasets, reducing dependence on acquiring both modalities.
2. Cost & Time Efficiency: Minimizes the need for multiple scanning sessions, reducing patient burden and operational load.
3. Scalability: The approach is generalizable to other imaging modalities and datasets (e.g., CT ↔ MRI, PET ↔ CT).

## Dataset
The dataset comprises MRI images, organized into two sub-directories,
”trainT1” and ”trainT2”. Each sub-directory contains a distinct
set of images, with 43 images in ”trainT1” and 46 images in
”trainT2”. Each image in the dataset is of size 181X217. The
dataset can be used for working on translating images from
one modality to another and testing how well they can be
translated. The figures below provide sample images from the
dataset.





![image](https://github.com/user-attachments/assets/9dee4834-7a00-4c8b-b99e-b8350b041e13)
![image](https://github.com/user-attachments/assets/41cc4f1e-a825-4412-8ff8-0e486b8f91d3)
## Workflow
The process begins by loading both the T1 and T2 MRI images. After loading, the images are read and then converted to NumPy arrays. The images are then resized to 256 X 256 pixels to ensure that all images are of uniform dimensions. The pixel values are also normalized to a range of [-1 1]. This is performed by dividing the pixel values by 127.5 and subtracting 1 from them. The GAN consists of two main components, the generator and
the discriminator networks. The image below describes the workflow process. 



![image](https://github.com/user-attachments/assets/a4449193-4bc8-408d-8f1f-0c49638b2bfc)


 



**The Generator Network**


The generator is based on the U-net architecture. U-Net
is used because it is known to be very effective in image to
image translation. The Generator Network is primarily broken
down into the following blocks as shown in the figure below.


![image](https://github.com/user-attachments/assets/e86bbbc0-cb03-4f3d-a440-aa7171a39611)

1) **Downsampling**: The Downsampling block is used to
extract features while reducing the spatial dimensions of
the input images. Every Downsampling block consists of a
Convolutional layer, followed by an Instance Normalization
layer. The output from the Instance Normalisation layer is then
passed through a Leaky ReLU Activation. A Convolutional
layer serves the purpose of detecting specific patterns in
the input image and to extract low level features. An Instance
Normalization layer helps in normalizing the features to make
sure that the training is stabilized and the rate of convergence
can be accelerated. The Leaky ReLU introduces non-linearity
and helps learn complex patters and mappings between the
input and the output. Also the vanishing gradient problem is
addressed with the help of Leaky ReLU function.
2) **Residual Blocks**: After the Downsampling block, the
output is then sent to the Residual Blocks. The Convolutional,
Instance Normalization and the Leaky ReLU function remain
the same in the Residual Blocks. But the Residual Blocks are
followed by a second Convolutional layer and then the output
of the second Convolutional layer is finally concatenated with
the input feature map. This property is called skip connection
and helps in creating a proper gradient flow and also maintaining
training stability.
3) **Upsampling**: The output from the Residual Blocks are
upsampled or reconstructed to form high resolution images.
Every Upsampling block contains a Transposed Convolutional
layer, Instance Normalization layer and ReLU Activation just
like the Downsampling block. In the Transposed Convolutional
layer, the spatial dimensions of the images are expanded.
4) **Output Layer**: The output layer of the generator is
a convolutional layer that makes use of the tanh activation
function. The tanh activation function is used since it maps
the pixels to a range of [-1 1].



**The Discriminator Network**


The discriminator network is based on PatchGAN architecture.
It penalises the image structure at the local level.
Then it classifies the image if it is real or fake using the
NxN patch of the image. Similar to the Generator Network,
the architecture contains a downsampling block followed by
convolutional layers and the output layer. Unlike the output
layer in the Generator Network, it does not have any activation
function. Rather it represents the probability of each patch
whether it is real or fake for NXN patches. The following figure represents the Discriminator Architecture.

![image](https://github.com/user-attachments/assets/34e3af19-74f4-4748-a364-dcc906159c67)

**Loss Functions**


The loss functions that are used to ensure smooth training
are Adversarial Loss, Cycle-Consistency Loss and Identity
Loss. The Adversarial Loss function plays a vital role in
generating the image in the most genuine way possible.This
is achieved by calculating the error between the generated
image and the real image. Cycle-Consistency Loss function
is responsible for maintaining the consistency between the
translated and the original image throughout the cycle. The
content of the image is preserved throughout the translation
process. This is made sure by employing the Identity loss
function, which penalizes the differences between the input
and the translated image.




## Results
After completing the training process of the cyclic GAN
model, significant results have surfaced, highlighting its proficiency
in image translation tasks. The following figures demonstrates
the generation of an image using random noise with
untrained generator models. It can be understood from this
figure that it exhibits inherent randomness and lacks coherence
with the target images.




![image](https://github.com/user-attachments/assets/15aaa1c7-6a32-46c7-9f4f-549b011ed326)
![image](https://github.com/user-attachments/assets/f3c60447-080b-4a0f-9374-12de468add0c)



However, as the training unfolds and the model iteratively
refines its parameters, a improvement in image translation
becomes apparent. The figures below depict the evolution of
the model’s performance across different epochs, specifically
showcasing outputs at epoch 1, epoch 100, and epoch 145 respectively.
These visualizations provide a comprehensive view of how the
model refines its translation capabilities over time, showcasing
its learning progression and improvement. The comparison in
this study helps in understanding how the model behaves in
the very initial stages and how it can advance through several
epochs and achieve a good performance.


![image](https://github.com/user-attachments/assets/eb447272-7ec1-4beb-b67e-dd095b514e22)
![image](https://github.com/user-attachments/assets/955953c0-935c-4be7-a7b7-b41c742db338)
![image](https://github.com/user-attachments/assets/b399ce06-0dd5-4654-afd1-21e6f4fe0298)



## Future Work

1. Augment the existing training dataset with supplementary MRI images from diverse sources to improve model accuracy and robustness.
2. Evaluate across different modalities and organs.
3. Test the CycleGAN model on a wider range of MRI modalities and various organs to assess its performance comprehensively and ensure its applicability in diverse clinical scenarios.
4. Integrate more sophisticated evaluation metrics to better capture the quality and clinical relevance of the generated images, ensuring the model's effectiveness and reliability in medical practice.


## Publication

If you want further details, use this link:

[GAN-Based MRI Image Translation: T1 to T2 Modality - Published Paper](https://ieeexplore.ieee.org/abstract/document/10725367)


