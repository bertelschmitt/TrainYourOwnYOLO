# TrainYourOwnYOLO: Building a Custom Object Detector from Scratch [![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

This repo let's you train a custom image detector using the state-of-the-art [YOLOv3](https://pjreddie.com/darknet/yolo/) computer vision algorithm. For a short write up check out this [medium post](https://medium.com/@muehle/how-to-train-your-own-yolov3-detector-from-scratch-224d10e55de2). 

### Pipeline Overview

To build and test your YOLO object detection algorithm follow the below steps:

 1. [Image Annotation](/1_Image_Annotation/)
	 - Install Microsoft's Visual Object Tagging Tool (VoTT)
	 - Annotate images
 2. [Training](/2_Training/)
 	- Download pre-trained weights
 	- Train your custom YOLO model on annotated images 
 3. [Inference](/3_Inference/)
 	- Detect objects in new images and videos

## Repo structure
+ [`1_Image_Annotation`](/1_Image_Annotation/): Scripts and instructions on annotating images
+ [`2_Training`](/2_Training/): Scripts and instructions on training your YOLOv3 model
+ [`3_Inference`](/3_Inference/): Scripts and instructions on testing your trained YOLO model on new images and videos
+ [`Data`](/Data/): Input Data, Output Data, Model Weights and Results
+ [`Utils`](/Utils/): Utility scripts used by main scripts

## Getting Started

### Requisites
The only hard requirement is a running version of python 3.3 or newer. To install the latest python 3.x version go to 
- [python.org/downloads](https://www.python.org/downloads/) 

and follow the installation instructions. Note that this repo has only been tested with python 3.6 and thus it is recommened to use `python3.6`.

To speed up training, it is recommended to use a **GPU with CUDA** support. For example on [AWS](/2_Training/AWS/) you can use a `p2.xlarge` instance (Tesla K80 GPU with 12GB memory). Inference is very fast even on a CPU with approximately ~2 images per second. 


### Installation

#### 1a Setting up Virtual Environment [Linux or Mac]

Clone this repo with:
```
git clone https://github.com/AntonMu/TrainYourOwnYOLO
cd TrainYourOwnYOLO/
```
Create Virtual **(Linux/Mac)** Environment (requires [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) which is included in the standard library of Python 3.3 or newer):
```
python3 -m venv env
source env/bin/activate
```
Make sure that, from now on, you **run all commands from within your virtual environment**.

#### 1b Setting up Virtual Environment [Windows]
Use the [Github Desktop GUI](https://desktop.github.com/) to clone this repo to your local machine. Navigate to the `TrainYourOwnYOLO` project folder and open a power shell window by pressing **Shift + Right Click** and selecting `Open PowerShell window here` in the drop-down menu.

Create Virtual **(Windows)** Environment (requires [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) which is included in the standard library of Python 3.3 or newer):

```
py -m venv env
.\env\Scripts\activate
```
![PowerShell](/Utils/Screenshots/PowerShell.png)
Make sure that, from now on, you **run all commands from within your virtual environment**.

#### 2 Install Required Packages [Windows, Mac or Linux]
Install all required packages with:

```
pip install -r requirements.txt
```
If this fails, you may have to upgrade your pip version first with `pip install pip --upgrade`. If your system has working CUDA drivers, it will use your GPU automatically for training and inference.

## Quick Start (Inference only)
To test the cat face detector on test images located in [`TrainYourOwnYOLO/Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) run the `Minimal_Example.py` script in the root folder with:

```
python Minimal_Example.py
```

The outputs are saved in [`TrainYourOwnYOLO/Data/Source_Images/Test_Image_Detection_Results`](/Data/Source_Images/Test_Image_Detection_Results). This includes:
 - Cat pictures with bounding boxes around faces with confidence scores and
 - [`Detection_Results.csv`](/Data/Source_Images/Test_Image_Detection_Results/Detection_Results.csv) file with file names and locations of bounding boxes.

 If you want to detect cat faces in your own pictures, replace the cat images in [`Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) with your own images.

## Full Start (Training and Inference)

To train your own custom YOLO object detector please follow the instructions detailed in the three numbered subfolders of this repo:
- [`1_Image_Annotation`](/1_Image_Annotation/),
- [`2_Training`](/2_Training/) and
- [`3_Inference`](/3_Inference/).
 
**To make everything run smoothly it is highly recommended to keep the original folder structure of this repo!**

Each `*.py` script has various command line options that help tweak performance and change things such as input and output directories. All scripts are initialized with good default values that help accomplish all tasks as long as the original folder structure is preserved. To learn more about available command line options of a python script `<script_name.py>` run:

```
python <script_name.py> -h
```

## License

Unless explicitly stated otherwise at the top of a file, all code is licensed under the MIT license. This repo makes use of [**ilmonteux/logohunter**](https://github.com/ilmonteux/logohunter) which itself is inspired by [**qqwweee/keras-yolo3**](https://github.com/qqwweee/keras-yolo3).

## Acknowledgements
Many thanks to [Niklas Wilson](https://github.com/NiklasWilson) for contributing towards making this repo compatible with Tensorflow 2.0. 

## Troubleshooting

0. If you encounter any error, please make sure you follow the instructions **exactly** (word by word). Once you are familiar with the code, you're welcome to modify it as needed but in order to minimize error, I encourage you to not deviate from the instructions above. If you would like to file an issue, please use the provided template and make sure to fill out all fields. 

1. If you encounter a `FileNotFoundError` or a `Module not found` error, make sure that you did not change the folder structure. In particular, your  working directory needs to look like this: 
    ```
    TrainYourOwnYOLO
    └─── 1_Image_Annotation
    └─── 2_Training
    └─── 3_Inference
    └─── Data
    └─── Utils
    ```
    If you want to use a different folder layout (not recommended) you will have to specify your paths as command line arguments. Also, try to avoid spaces in folder names, i.e. don't use a folder name like this `my folder` but instead use `my_folder`.

2. If you are using [pipenv](https://github.com/pypa/pipenv) and are having trouble running `python3 -m venv env`, try:
    ```
    pipenv shell
    ```

3. If you are having trouble getting cv2 to run, try:

    ```
    apt-get update
    apt-get install -y libsm6 libxext6 libxrender-dev
    pip install opencv-python
    ```

4. If you are a Linux user and having trouble installing `*.snap` package files try:
    ```
    snap install --dangerous vott-2.1.0-linux.snap
    ```
    See [Snap Tutorial](https://tutorials.ubuntu.com/tutorial/advanced-snap-usage#2) for more information.

## Filing an Issue
If you would like to file an issue, please use the provided issue template and make sure to complete all fields. This makes it easier to reproduce the issue for someone trying to help you. 

![Issue](/Utils/Screenshots/Issue.gif)

Issues without a completed issue template will be deleted after 7 days. 


+*Like everything new, YOLO can have a steep learning curve. Here is the beginning of a hopefully growing list of articles that help us ease into the matter.*
## VOTT's up: Tips & Tricks
Good object detection rides on a good model, and a good model needs to be babied to grow up strong and smart. An essential tool for the care and feeding of your custom model is VOTT, a free app that lets you annotate objects in pictures. Say you want to train your model on balls. You look for many pictures containing balls. You pull them into VOTT, and you then manually draw a box around each ball, and assign the tag “ball” to it. Next time you train your model, it will be having a ball. VOTT is written in TypeScript/JavaScript, and it should run on Windows, Linux, and OSX. VOTT has a few rough edges, and the (at the time of this writing) latest release, v2.1, is from April 2019. VOTT can be [downloaded here](https://github.com/Microsoft/VoTT/releases).
VOTT can be a little temperamentful, so here are a few tips to make it woerk for you:
#### 1. Thou shalt have only one VOTT

You may be used to starting apps with a double-click of the mouse (or a few more clicks if the computer is a bit slow.) Start VOTT only with one click. Why? More clicks can start more instances of VOTT, and when you do that, all hell tends to break loose. Suddenly, you can’t find your project. You “open local project” and VOTT complains about not finding a security token, all because you are working with a 2nd instance of VOTT. In your desperation, you create a new project, and the work of tagging hundreds of pictures is down the drain. So next time, start one and only VOTT. And VOTT developers, how about preventing a 2nd instance?

#### 2. Let your fingers do the tagging

Tagging goes much faster with one hand on the mouse, and with the other hand on the keyboard, assigning tags. You have keys from [0] to [9]. If you have more than 10 tags, then you can make a tag hotkeyable by moving the tag into the 10 tags with key numbers. For that, select a tag, and use the up-arrow/down-arrow buttons to move the tags around. Don’t worry, the sequence of tags does not matter until the images are shipped to YOLO for training. Oh, and be careful. Tagging now is so easy that I can (and occasionally do)  assign hundreds of wrong tags by hitting the wrong key. See below.  

#### 3. Use “Active Learning”

VOTT's "Active Learning" isn't really learning much. It tries to detect what you want to tag in a picture, and when it does, it draws a grey box around it to spare you the aggravation of moving your mouse. You then assign the proper tag. You need to do this rather quickly. If you wait too long, VOTT will think you drew a box without assigning a tag. Then, VOTT will turn into a mule, and it will refuse to move at all. Hit the DEL key to delete the box you never drew, and the mule will move again.  Active Learning is hit and miss, sometimes it works, sometimes not. Active Learning can also try to guess the tag, but I turned that feature off quickly. Allegedly, you can feed your custom model to VOTT to put detection on steroids, but the Internet is full of people who want to know how, and who never receive an answer. Active Learning seems to work a little better when tagging videos, which leads us to … 

#### 4. Tagging videos
Tagging videos instead of still pictures tends to produce faster and better results, especially when you use video taken with the same camera, and from the same angle as later used for detection. For that, you can pull the video file into VOTT, and then tag frame by frame. With “Active Learning” cooperating, you can tag along quite briskly. 

Sometimes, mule VOTT will refuse to ingest the video you have fed it. This happens when the video is produced with a CODEC VOTT doesn’t like. I had problems with videos created by YOLO with the h.264 CODEC. I tried a few CODECs with ffmpeg (a handy command-line tool) and VOTT balked, until I converted the h.264 video produced by YOLO into a new video converted by ffmpeg employing the, drumroll, h.264 CODEC, apparently, a subtly different h.264 vintage. Go figure, but keep trying. For enhanced training, I coerced YOLO into making videos that have a bounding box in every odd video frame, and no box in every even frame. Running this video through VOTT, I can now see where YOLO has low, or no detection results, and on the next frame, I can draw a box and tag it to give YOLO some help at the next training round. To produce that kind of videos involves changes to the YOLO code, and it is beyond the scope of this article. Ask if you want to know how it’s done. 

#### 5. Care and filing

Models are a living thing, they start small, and they need help to become big and powerful. You will probably re-train more than a few times, and the more pictures you add, the better the model usually gets. For that, it is best practice to keep just one directory as the output connection in VOTT, and let the images and output file grow. This way, when you later add to your model, VOTT will dump more images into the vott-csv-export directory, and it will update the export file. 

By default, VOTT will output a JSON file, which YOLO can’t use, it wants a CSV file. Set VOTT’s Export Settings to “Comma Separated Values (CSV)” and the Asset State to “Only Tagged Assets,” and select “Include Images.” That way, the vott-csv-export directory, a subdirectory created in your Target Connection, will fill with images, and in the same directory, a CSV file will be created that has information about the tagged clips and their coordinates within the images. Treat this file carefully, it is a record of all of your hard work, and this file is what YOLO needs for learning. YOLO expects that file to be named “Annotations-export.csv.” That will be its out-of-the-box name, as long as you call your VOTT project “Annotations.” If you call your great project “My_great_project,” then My_great_project.csv will be created, and you either have to rename the file before training, or you will have to tell YOLO via the command line to look for My_great_project.csv. Feed both to YOLO for training, and it will munch on it for hours, if not days.

#### 6. Advanced VOTT pruning
What if you want to add to your model, but you have already created a new project in VOTT that ended in a new *-export.csv file? Now you need to do some manual pruning. Open the newly created *-export.csv file, and add it to the end of your master Annotations-export.csv file by whatever means necessary (text editor, Excel, cat My_great_project.csv >> Annotations-export.csv …) Make sure the images dumped by VOTT into the vott-csv-export directory (you did select “Include Images,” did you?) go into the vott-csv-export directory used by YOLO for training. It is easy, but because of that, we can also mess up royally. 

In late-night sessions, I once produced thousands of duplicate entries YOLO valiantly tried to catch. That confused me even more, because now, YOLO reported thousands fewer pictures as ingested. It took me weeks to find out where the “missing” images went. Then, there was a nastier input mistake. Somehow, I tagged a few hundred images twice, but with different tags. YOLO dutifully recognized them as no duplicates, it used both tags for the same images, and you can imagine what that did to the quality (or not) of the model. So before blaming the garbage model, let’s remember GIGO, and check for garbage fed to the machine. I did this by throwing together a few lines of code that cross-referenced the Annotations-export.csv file with the data_train.txt file that gets produced when starting Convert_to_YOLO_format.py (don’t forget running that, or YOLO will happily re-train the old model.)

*That’s enough tricks and VOTT-not for today. What tricks do you have? Don’t keep them up your sleeve, share them in a message, or add them to the document.* 

## Stay Up-to-Date

- ⭐ **star** this repo to get notifications on future improvements and
- 🍴 **fork** this repo if you like to use it as part of your own project.

![CatVideo](/Utils/Screenshots/CatVideo.gif)
