# Advanced Machine Learning Project - Domain-To-Text 

Basic code to reproduce the baselines (point 1 of the project). 

## Dataset

1 - Download PACS dataset from the portal of the course in the "project_topics" folder.

2 - Place the dataset in the DomainToText_AMLProject folder making sure that the images are organized in this way:

```
PACS/kfold/art_painting/dog/pic_001.jpg
PACS/kfold/art_painting/dog/pic_002.jpg
PACS/kfold/art_painting/dog/pic_003.jpg
...
```

## Pretrained models

In order to reproduce the values reported in the table, you have to download the pretrained models from this link: https://drive.google.com/drive/folders/17tWDDDPY9fRLrnL3YbwkHrilq12oii2M?usp=sharing

Then, you have to put the "outputs" folder into 

```
/DomainToText_AMLProject/
```
**Note** :For reproducing the baseline please make sure that in eval_ensamble, line#103 should be uncomment and line#104 should be commented. It is basically path to weights file. 

## Environment

To run the code you have to install all the required libraries listed in the "requirements.txt" file.

For example, if you read

```
torch==1.4.0
```

you have to execute the command:

```
pip install torch==1.4.0
```
# STEPS
1. **Initial Directory Setup:** Before start I would like to give a brief about directory structure of projects. Basically we have two projects, one is DomainToText_AMLProject and second one is DescribingTextures(**Modified Version of DescribingTexture:** https://github.com/aamirashrafi/DescribingTextures). All the files related to DomainToText_AMLProject are under /content/drive/MyDrive/DomainToText_AMLProject directory, and all the files related to DescribingTextures are under /content/drive/MyDrive/DescribingTextureCopy/DescribingTextures directory. For the sake of simplicity and avoiding each time change the path in the code I would prefer 1st to move in the project directory and then run the respective code to train the model.
2. **Label the PACS dataset describing the visual domain attributes:** We have labeled our assigned images manually. These lables are in the file image_descriptions.json. We also need to create image split file image_splits.json. These two files can be found here https://drive.google.com/drive/folders/1g41kTfoCQGdhCtIbfrO0fijLYeCrgc1B?usp=sharing.
3. **Traing DescribingTexture Model:** Place the dataset in the DescribingTextures folder making sure that the images are organized in this way:

```
data_api/data/images/art_painting/dog/pic_001.jpg
data_api/data/images/art_painting/dog/pic_002.jpg
data_api/data/images/art_painting/dog/pic_003.jpg
...
```
and image_descriptions.json and image_splits.json should me in the directory

```
data_api/data/image_descriptions.json
data_api/data/image_splits.json
```
4. **Set Sentence Encoder:** We need to set ``Bert`` as sentense encoder. So in the config_default.py file me need to write C.MODEL.LANG_ENCODER = 'bert'.  To train this model,  the evaluation split was intended to be the same as the training  split.
5. **BEST_checkpoints.pth:** When the image retrieval and phrase retrieval MAP on the validation set stopped improving, the model training will be stopped, and we will get the best weights under output/triplet_match/temp/checkpoints directory.
6. **Retrain DomainToText with BEST_checkpoints.pth:** Now we have to train our DomainToText model with new best weights. For applying new best weights either we can replace BEST_checkpoints.pth file or we can set path to BEST_checkpoints.pth file in eval_ensamble.py. So we need to make sure that in eval_ensamble.py line#103 should be commented and line#104 should me un-commented.
7. **Train the model:** Now we can train the model and observe the result. 

