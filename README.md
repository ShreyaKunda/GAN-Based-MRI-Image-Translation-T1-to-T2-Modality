# Bridging-the-Modality-Gap-Generative-Adversarial-Networks-for-T1-T2-MRI-Image-Translation
## About the project
CycleGAN, a significant deep learning model, has transformed medical imaging by providing a remedy for translating MRI images between different modalities. Its ability to transform T1-weighted to T2-weighted images is crucial in healthcare environments where obtaining multiple scans can be timeconsuming
and burdensome for patients. This can be achieved by
utilizing CycleGAN, which generates images that contains vital
information that will help the healthcare professionals to diagnose
the patient without exposing them to further radiations. This
unleashes an effective and safer way of diagnosing patients. The
adaptability of CycleGAN also allows scalability and the ability to
customize it for different types of medical images, where scanning
can be achieved with less exposure to radiation, without loosing
or compromising any important information.

## Working
![image](https://github.com/user-attachments/assets/a4449193-4bc8-408d-8f1f-0c49638b2bfc)

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





