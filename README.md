# Arabic_OCR

The implementation of the OCR system for Arabic historical documents using the selected pre-processed data from KITAB corpus. The figure below shows the main phases in our methodology for recognizing Arabic text using deep learning. The process begins with line segmentation followed by word segmentation. The segmented word images are then divided into three distinct sets, consisting of a training set (80%), a validation set (10%) for monitoring the performance of the during training, and a testing set (10%) for evaluating the model.

![Picture1](https://user-images.githubusercontent.com/109873009/224418772-44c9e35a-00b4-42a7-ab71-39e914f5b2e4.jpg)



# Step 1: Line and Word Segmentation

Line segmentation steps include blurring the image and the horizontal projection algorithm. As for the word segmentation, we used findContours function in OpenCV library, which finds the boundary of each word after smoothing the image.

The results of the line segmentation method

![Picture2](https://user-images.githubusercontent.com/109873009/224419888-7a89779f-9915-4c41-acee-159523304435.jpg)

The results of the word segmentation method

![Picture3](https://user-images.githubusercontent.com/109873009/224420040-a886ee12-6d7c-48e8-9315-d8028ed48cb3.jpg)


# Step 2: Deep Learning Model

The architecture of this model consists of 15 layers including the input and output layers. The architecture begins with an input layer, where every pre-processed word-segmented image in the dataset is resized to a width of 64 pixels and a height of 32 pixels with the number of channels as 1 since the image is grey-scaled and binarized. Followed by two convolution and pooling layers. The first convolution layer consists of 32 filters and the second convolution layer consists of 64 filters. Both layers have a filter of size (3, 3), ‘ReLu’ as the activation function, ‘he_normal’ weight initializer, and zero padding. After each convolution layer is a batch normalization layer. Next is a reshaping layer, followed by a dense layer then a dropout layer with 20% dropout rate. This architecture consists of two Bi-LSTM layers with 128 and 64 hidden units respectively. Lastly, the output of the Bi-LSTM layers is fed to a dense layer followed by the output layer to compute the CTC loss.

# Experimental Result

We present the experimental result obtained from exploring pre-processing techniques, which were tested but not included in the methodology steps.

Pre-processing for Arabic Collections Online (ACO) dataset

The first phase is grey scaling, where the image is converted to a grey-scale image. The second phase is skew correction using the horizontal and vertical projection profiles method. This method takes the binary images and creates a horizontal histogram in which the hills of the histogram are the center locations of the horizontal ruled lines. Then we normalized the image. This process changes the range of pixel intensity values. The purpose of performing normalization is to achieve the consistency of the image range of values for the different inputs. The next phase is noise removal, smoothing out the images by removing small dots with higher intensities than the rest of the images. To remove the noise from the image, we applied a median filter and mean filter. Then, we sharpened the image to raise the text details in the image to be clear to identify. Then, applied morphologic operation (opening) was to remove salt-and-pepper noise in the image. The last phase is binarization; since our dataset has a uniform background, a background with simple noise, we applied the Otsu method for binarization. Otsu method uses global thresholding. The Otsu threshold is derived from the histogram of grayscale image intensity values. It chooses an optimal threshold that separates the image into two different classes.

The result of pre-processing on a sample bad-quality page

![Picture5](https://user-images.githubusercontent.com/109873009/224421297-eecf520e-a55b-41a4-b34b-3414bb6b9e5d.png)


The ACO books are not annotated. So, we changed the dataset to annotated books from KITAB corpus.

