# Semantic_segmentation_of_geological_features_on_Mars

The purpose of this project is to apply semantic segmentation to Mars rover imagery in order to classify surface terrain at the pixel level. By identifying terrain types such as sand, soil, and rock, the project aims to support terrain-aware perception that can improve autonomous rover navigation, reduce reliance on manual path planning, and increase operational safety on Mars. In this work, the AI4MARS dataset and models such as U-net, DeepLabV3 and DeepLabV3+ were used.

## Dataset

The AI4Mars dataset is a large publicly available dataset containing about 35,000 high-resolution images of Martian terrain captured by the Curiosity, Opportunity, and Spirit rovers. The images were labeled through a crowdsourcing process where volunteers annotated four main terrain classes—Soil, Bedrock, Sand, and Big Rock—while regions. https://zenodo.org/records/15995036

For this work, the processed dataset provided was used...

## Models

U-net:

U-Net is an encoder–decoder segmentation model. Its U-shaped architecture combines downsampling and upsampling paths with skip connections that concatenate corresponding feature maps, allowing the network to capture both detailed spatial information and high-level features.

![u_net](https://github.com/user-attachments/assets/843ac9f5-0e0e-41a6-80b9-5a13ca71862e)


DeepLabV3:

DeepLabV3 is a semantic segmentation model that uses atrous (dilated) convolutions and an Atrous Spatial Pyramid Pooling (ASPP) module to capture multi-scale contextual information without reducing spatial resolution. 

![download](https://github.com/user-attachments/assets/566711c8-782d-4af1-8077-2ba696e282a6)


DeepLabV3+:

DeepLabV3+ is the latest model in the DeepLab family (following DeepLabV1, V2, and V3) and extends this architecture by adding a decoder and skip connections to refine object boundaries.

<img width="1037" height="551" alt="1_2mYfKnsX1IqCCSItxpXSGA" src="https://github.com/user-attachments/assets/9b64517d-df74-449e-aa0b-1c7779cb1a14" />





