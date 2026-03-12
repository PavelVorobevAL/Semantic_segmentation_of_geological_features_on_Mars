# Semantic_segmentation_of_geological_features_on_Mars

The purpose of this project is to apply semantic segmentation to Mars rover imagery in order to classify surface terrain. By identifying terrain types such as sand, soil, and rock, the project aims to help rovers better understand the terrain on Mars. This can improve autonomous navigation, reduce the need for manual control from humans, and make rover operations safer. In this work, a subset of the AI4Mars dataset was used together with semantic segmentation models such as U-Net, DeepLabV3, and DeepLabV3+.

## Dataset

The AI4Mars dataset is a large publicly available dataset containing about 35,000 high-resolution images of Martian terrain captured by the Curiosity, Opportunity, and Spirit rovers. The images were labeled through a crowdsourcing process where volunteers annotated main terrain classes. https://zenodo.org/records/15995036

For this project, a preprocessed subset was obtained from https://huggingface.co/datasets/Ankhitan/1000Samples. It contains 932 PNG images and a corresponding number of preprocessed PNG masks. 

Image and mask size - 512x512;

Classes:
0 - Unwanted regions (sky / rover components);
1 - Sand (409 mentions);
2 - Soil (524 mentions);
3 - Rock (582 mentions)

Example of image and mask:

<img width="256" height="256" alt="unnamed" src="https://github.com/user-attachments/assets/7a41eca0-1d97-4509-a4f8-a7034f8ab19b" />            <img width="256" height="256" alt="unnamed" src="https://github.com/user-attachments/assets/139a3fe0-d2dd-4c70-9e72-3b398c7602c7" />



## Models

U-net:

U-Net is an encoder–decoder segmentation model. Its U-shaped architecture combines downsampling and upsampling paths with skip connections that concatenate corresponding feature maps, allowing the network to capture both detailed spatial information and high-level features.

<img width="850" height="608" alt="U-Net-architecture-used-in-this-study-Input-images-of-size-512-by-512-pixels-upper" src="https://github.com/user-attachments/assets/996cf8c6-08c4-44fb-9e57-b8642f774c04" />



DeepLabV3:

DeepLabV3 is a semantic segmentation model that uses atrous (dilated) convolutions and an Atrous Spatial Pyramid Pooling (ASPP) module to capture multi-scale contextual information without reducing spatial resolution. 

![download](https://github.com/user-attachments/assets/566711c8-782d-4af1-8077-2ba696e282a6)


DeepLabV3+:

DeepLabV3+ is the latest model in the DeepLab family (following DeepLabV1, V2, and V3) and extends this architecture by adding a decoder and skip connections to refine object boundaries.

<img width="1037" height="551" alt="1_2mYfKnsX1IqCCSItxpXSGA" src="https://github.com/user-attachments/assets/9b64517d-df74-449e-aa0b-1c7779cb1a14" />


## Training

For training, the pre-processed dataset was divided in the following ratio:

Training set - 70% (653 images)
Validation set - 20% (186 images)
Testing set - 10% (93 images)

The following hyperparameters were used: Batch Size - 2, Epochs - 40, Loss function - Cross-Entropy, Optimizer - Adam, Scheduler - ReduceLROnPlateau (mode - "min", factor - 0.5, patience  - 3 epochs)

## Experimental Setup 

The U-Net, DeepLabV3, and DeepLabV3+ models were implemented using PyTorch and trained locally in a Jupyter Notebook environment. Each model was trained in four configurations, combining two backbone architectures (ResNet50 and ResNet101) with two initial learning rates (0.001 and 0.0001). In all experiments, models were trained and validated on training and validation sets and tested on the testing sets. Performance was evaluated on the test set using pixel-level accuracy (Acc), class-wise Intersection over Union (IoU), and mean Intersection over Union (mIoU) across all classes. ? During the training 
process, the best model is identified as the one that achieves 
the highest mIoU on the validation set ?

## Results


![Снимок](https://github.com/user-attachments/assets/d624d270-93b1-4fe0-a444-cc8e3fb3b673)


Regarding the results, the learning rate 0.0001 gave better results in all experiments. Models trained with the smaller learning rate achieved higher mIoU and accuracy. Also, the lower learning rate helped avoid sharp jumps in the metrics during training. This all shows that a smaller learning rate leads to more stable training and a better segmentation.

Models with ResNet101 generally performed slightly better than models with ResNet50. However, the improvement was small, so both backbones work well for this task.

Analysis of class-wise IoU shows that Sand is the most difficult class to segment, while Soil and Rock are predicted more accurately. The sand class likely shows lower IoU because it appears less frequently in the dataset and can look similar to other terrain types, making it harder for the model to distinguish.

DeepLabV3 and DeepLabV3+ with ResNet101 architecture showed the best results, with a small difference between these two experiments in metrics of about 1–2%. 

