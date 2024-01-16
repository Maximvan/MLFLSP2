# Machine Learning for Life Sciences Project 2 - Multi-Label Protein Organelle Localization Prediction
This project aims to predict protein organelle localization in a dataset of confocal microscopy images, featuring 10 diverse labels across 10 different cell types, framing the challenge as a multi-label classification problem and employing mean F1-score as the evaluation metric in the context of the Machine Learning for Life Sciences course at Ghent University.

## Introduction
The primary objective of this project is to predict the localization labels of protein organelles for each sample in a dataset containing images obtained through confocal microscopy. The dataset encompasses 10 distinct labels representing various protein organelle localizations. It is crucial to note that the dataset includes 10 different cell types, each exhibiting highly diverse morphologies, which directly influence the protein patterns of various organelles. Images within the dataset may have one or more labels associated with them.

The overarching goal of this project is to develop a model capable of predicting, for a given image the classes determining one or more proteins. This problem is framed as a multi-label classification challenge, and the mean F1-score is selected as the evaluation metric. The project is the second and final project as part of the course Machine Learning for Life Sciences at Ghent University.

## Data Exploration and Processing
In this section of the report, I aim to delve into the features of the dataset. The dataset comprises images with a resolution of 128 x 128 pixels and is composed of three channels (RGB). All images are formatted in PNG.

The training set encompasses 15,389 images, while the test set includes 3,847 images. To facilitate the analysis, the data is uploaded to the temporary file directory of the Google Colab notebook as a compressed zip file. Subsequently, it is extracted and organized into the appropriate directories for further processing.

The class labels associated with the images are stored in a CSV file, featuring 'Image' and 'Label' columns. Each 'Image' corresponds to the image file name, with '.png' appended for ease of loading during model training and testing. Additionally, the categorical labels, ranging from 0 to 9, are separated into distinct columns within the DataFrame. This arrangement facilitates later retrieval and transformation into one-hot encoded labels.

The label categories are defined as follows:
- 0: 'Mitochondria'
- 1: 'Nuclear bodies'
- 2: 'Nucleoli'
- 3: 'Golgi apparatus'
- 4: 'Nucleoplasm'
- 5: 'Nucleoli fibrillar center'
- 6: 'Cytosol'
- 7: 'Plasma membrane'
- 8: 'Centrosome'
- 9: 'Nuclear speckles'

## Model Training and Validation
Due to imbalances in both individual labels and label combinations, the limited size of the training dataset (approximately 14,000 images), and the intricate nature of protein localization, a pretrained model is employed. Specifically, the InceptionResNetV2 model, pretrained on ImageNet, is utilized. The initial classification layer is omitted, and a custom 'head' is appended, consisting of two additional layers. The final layer incorporates a sigmoid activation function, producing probabilities for each label. This choice aligns with the principles of transfer learning, allowing the model to leverage knowledge gained from a large-scale dataset for improved generalization. InceptionResNetV2's architectural design makes it resilient to variations in input images, making it suitable for the diverse and complex nature of cellular images.

I opted for InceptionResNetV2 for this task due to its powerful feature extraction capabilities and proven effectiveness in discerning intricate patterns in images. This architecture combines the strengths of Inception and ResNet, providing a robust framework for capturing detailed hierarchical features, which is crucial for the complex nature of protein localization. The fact that InceptionResNetV2 has been pretrained on ImageNet is a major advantage, as it brings a broad understanding of visual features to the model, facilitating better performance with our limited training dataset of around 14000 images.

Inception, known for its inception modules, excels in extracting features at various spatial scales simultaneously. This allows the network to capture both fine and coarse details in the images, essential for discerning complex protein localization patterns.

The incorporation of residual connections from the ResNet architecture enhances the model's ability to tackle the challenges of training deep networks. Residual connections facilitate the smooth flow of gradients during backpropagation, mitigating issues like vanishing gradients. This is particularly advantageous when dealing with deep architectures, ensuring effective learning and feature representation.

## Additional Reflections
In this section, I aim to document various techniques that were experimented with but did not yield favorable results. These endeavors encompassed the exploration of different models, optimizers, loss functions, preprocessing techniques, and the generation of final test predictions. Although these methods were employed in diverse manners with the goal of enhancing the Kaggle score, the outcomes did not surpass the score of the final submission. Despite the lack of improvement in the final score, some of these attempts are documented below to highlight the diverse strategies explored throughout this project. Techniques that were explored and are briefly discussed:

- Segmentation of the images
- Training a 'simple' CNN for 170 epoch
- Different loss functions
- Optimal threshold selection

## Potential Enhancements
While the model achieved a suboptimal macro F1 score, there are various factors that could have contributed to this outcome. Subsequent to the deadline, I explored avenues for improvement by experimenting with smaller batch sizes, employing alternative model architectures, introducing additional image normalization techniques, and incorporating the average intensity in each layer for enhanced normalization of the input images.
