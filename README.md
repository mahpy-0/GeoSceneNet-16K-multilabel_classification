
# multi label image classification

## about data

__*This dataset have 10 labels. They are "motorcycle, truck, train, bus, cycle, sitar, ektara, flutes, tabla, harmonium". Each image have one to multiple label. Good for multi label image classification.*__

[data source in kaggle](https://www.kaggle.com/datasets/meherunnesashraboni/multi-label-image-classification-dataset "https://www.kaggle.com/datasets/meherunnesashraboni/multi-label-image-classification-dataset")

## Imports

For this project I use numpy, pandas, matplotlib.pyplot, seaborn, openCV, sklearn, tensorflow, and keras

## Loading Data

In order to load data in colab I used google colad module and mounted my drive, then unziped data, after that using pandas I read the "multilabel_classifiction(7).csv" and started preprocessing.

## preprocessing

Since the labels column were big mess I renamed it to labels for simplicity and with that data frame is almost done.

next moving to images and first I need to have the path to images and then read them and resize them since they're not in same size.
I also applyed a lambda function to make sure only the images inside the images folder stay in data frame.

then image preprocessing starts, using a function to resize and normalize the data, I looped over all the data frame and filed the images and labels list with preprocessed images and their labels.

then using a multi label binarizer, binrized the labels (returned as numpy array).
I used the binarized labels to show the amount of images with each separated labels(not including duplicates). with "labels_df.sum(axis= 1).max()" we can see that the maximum number of label an image could have is 4. and next we can see the amount of images with each respected number of labels.

at the end turning images list into numpy array, and because of limited available ram I had to remove useless variables, and then split the data into train and val_test and then split again to validation and test

## model making

for model architecture I used sequential models. it has 3 convolution layers and 3 maximum pooling layers, then a flatten layer to pass the feature maps to dense network. this model has 2 hidden dense layer and 2 dropout layer and after all of this hidden net there is a dense layer for getting the predictions (which for this multilabel classification has sigmoid to just give the probability).

as for compiling I used adam for optimizer, binary cross entropy for loss, and accuracy for metric.

I also used early stopping so the model stop early in case of no significant progress.

then I fited the model with batch size of 2, 20 epochs, and early stopping callback with 10 patience.

after that I saved model.

## visualizing performance

now I visualized model train and validation accuracy and loss using matplotlib

after that I used evaluate method to get accuracy and loss of validation and test data.

then I get prediction of model and used normal 50% threshold to determine model predicted each class is in the image or isn't

at the end with sklearn I evaluated models accuracy and classification perfpormance with resulted 64% accuracy and 76% micro f1-score.