# Amazon Rekognition Custom Label Lab

One challenge for certain business cases is, to detect objects in images that are not part of the default Amazon Rekognition model. To address this issue [Amazon Rekognition custom labels](https://aws.amazon.com/rekognition/custom-labels-features/) provides the possibility to train a model with own images and labels. This lab walks you through the steps of creating the needed dataset, labeling the important objects in the objects and finally training the model.

For this lab we will use an image set of power plants and detect cooling tower and chimneys in the images. The lab is not restricted to these images and can be run with an image set of your choice.

On prerequisit is that a region is selected where Amazon REkognition is already available, i.e. us-east-1, us-east-2 or eu-west-1

## Deploy Rekognition Custom Labels Demo App

To get started the first step is to deploy the [Amazon Rekognition Custom Labels Demo](https://github.com/aws-samples/amazon-rekognition-custom-labels-demo). The demo app deploys a web application that make it easy to interact with the model as soon it is deployed and available.

Please follow these [deployment instructions](https://github.com/SaschaRodekamp/amazon-rekognition-custom-labels-demo#deployment)

While the CloudFormation Stack is deploying, we can prepare the model with the custom labels.

## Create a custom labels project

Go to the [Amazon Rekognition Console](https://console.aws.amazon.com/rekognition/home?)

1. Choose `Use Custom Labels` from the main menu on the left
2. If you seeing the Amazon Rekognition Custom Labels splash screen, click `Get started`
3. Type a project name "PowerPlantDetection"
4. Click `Create Project`

## Create Data Set

When the Project is created a Dataset with the custom images needs to be created. A Dataset contains images, labels and bounding boxes which will be used to train a model.

1. In the menu on the left choose `Datasets`
2. Click `Create dataset`
3. Enter a name for the Dataset "PowerPlantImages"
4. Choose `Upload images from your computer` from the tiles
5. Click `Submit` (lower right of the page)

The 'tool guide' will open automatically, take a few minutes to go through the tips before closing the popup.

6. Click `Add images` and `Choose files` from the popup
7. Select all files from the training folder
8. Click `Upload images` at the bottom of the image list

Images now getting uploaded to the dataset.

## Labeling Data

To tell the model which objects are of interest in the pictures, the objects needs to be labeled. For that we draw a bounding box around the objects in each image. One image can be labeled with multiple bounding boxes and different bounding boxes can overlap.

To get more information, click `Labeling tips`

### Add Labels

1. First we create the needed labels. Click `Add` in the label overview box (Filter by labels).  
2. Type in the name of the first label "CoolingTower" and hit `Add label`.
3. Add a second label "Chimney" and click `Add label`
4. Close the dialog with `Save`

### The Labeling

1. Select all pictures on the first page
2. Click `Draw bounding boxes`

Take a few minutes to read "Tips for Drawing Bounding Boxes" which opens automatically.

3. Select the label you want to mark in the image from the list on the right. The number beside each label is the shortcut to quickly select the label.
4. Draw a box around the object on the image
5. If you want to label a second object, select the appropriate label from the list (or by using the short key) and draw the box around any additional object.
6. As soon all objects are marked, click `Next` to jump to the next image  
7. Continue until all objects in all image are labeled, then click `Done` to save everything
8. Jump to the next page of images and start over from point 3. until all images are labeled

## Training the model

1. From the main menu on the left choose `Projects`
2. Select the created project "PowerPlantDetection"
2. Click `Train new Model`
3. In the Training Details choose:
    - Choose training dataset: "PowerPlantImages"
    - Select `Split training dataset` from the tiles
    - Click `Train` to start the training process

Back on the project detail page the model will have the status "TRAINING_IN_PROGRESS" until the process has been finished.

## Starting the model

