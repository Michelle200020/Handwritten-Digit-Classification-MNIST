# Handwritten-Digit-Classification-MNIST
HANDWRITTEN DIGIT IMAGE CLASSIFICATION USING CNN REPORT

BUSINESS PROBLEM
To create a model for Image classification of Handwritten Digits from 0-9.

ABOUT THE DATASET
The MNIST database (Modified National Institute of Standards and Technology database) of handwritten digits consists of a training set of 60,000 examples, and a test set of 10,000 examples. It is a subset of a larger set available from NIST consisting of black and white 28x28 pixel images. The goal of the problem is to classify a given image of a handwritten digit as an integer from 0 to 9. This is a multiclass image classification problem.

THE MODEL
The TensorFlow and Keras software libraries were used extensively for this project. TensorFlow is a free and open-source software library for machine learning and artificial intelligence with a primary focus on training deep neural networks. Keras is an API that provides a Python interface for the TensorFlow library.

The MNIST dataset was loaded from TensorFlow’s datasets and split into training and testing set. A few images were visually displayed and some basic information of the dataset was acquired. The dataset has 10 labels consisting of numbers from 0 to 9 which are the target variables. The images in the x-train and x-test variables are stored as 3 dimensional arrays with pixel values ranging from 0 to 255.



ANN VS CNN
ANN requires one dimensional tabular data in the input layer such as the image features which is seldom the case in multidimensional coloured pixelated images of the real world. It is not very effective in capturing sequential or image orientation information from the data and thus performs poorly if these factors are slightly different in the input. For instance, ANN would not be able to correctly classify an inverted image despite the network being trained on the exact image when not inverted.  Hence ANN is sensitive towards any changes that are happening to images and is not suitable for Computer vision tasks.
CNNs rely on kernels and filters of different sizes that scans the images, each responsible for detecting various image features such as arcs, diagonals etc. These unique features extracted by the CNN model are able to correctly classify images even with different orientations. Moreover, CNNs were designed keeping image processing in mind and are thus able to tackle the problem of increasing parameters/ dimensions of regular neural networks by having pooling layers.
Thus, CNNs are more suitable for image classification problems as compared to ANN’s and for these reasons was selected as the preferred neural network type for this project.

STANDARDIZING THE DATA
The data was normalized which scaled the values between 0 and 1. Normalisation of data speeds up the learning process and leads to faster convergence. This subsequently reduces training time and aids in faster data processing by the network. Although normalisation is not a mandatory step for neural networks, it is almost always done to help improve the performance of a neural network.

DATA TRANSFORMATION
Since the TensorFlow CNN models expect a 3-dimensional input array the data was reshaped to the following format (number of observations, rows, columns, channels).


THE CNN ARCHITECTURE
There are two main parts to a CNN architecture-
A convolution tool that separates and identifies the various features of the image for analysis in a process called as Feature Extraction
A fully connected layer that utilizes the output from the convolution process and predicts the class of the image based on the features extracted in previous stages

There are three types of layers that make up the CNN which are the convolutional layers, pooling layers, and fully-connected (FC) layers. In addition to these three layers, there are two more important parameters which are the dropout layer and the activation function which are defined below.
CONVOLUTION LAYERS
This layer is the first layer that is used to extract the various features from the input images and constitutes the main building block of any CNN model. In this layer, the mathematical operation of convolution is performed between the input image and a filter of a particular size MxM. The size of the filters is usually smaller than the actual image. An activation map is created by sliding the filter over the input image and taking the dot product between the filter and the pixel values of the input image. The output is termed as the Feature map which gives us information about the image such as the corners and edges.

For my model, the first convolution layer had 32 different kernels (filters=32) each having a kernel size of 3x3.  For the second convolution layer, the number of filters was increased to 64.
POOLING LAYERS
The primary aim of this layer is to decrease the size of the convolved feature map to reduce the computational costs. The pooling layer summarises the features present in a region of the feature map generated by a convolution layer. So, further operations are performed on summarised features instead of precisely positioned features generated by the convolution layer. This makes the model more robust to variations in the position of the features in the input image. There are different types of pooling filters such as Max Pooling, Min Pooping and Mean Pooling.
For my model Max Polling was used which selects the maximum element from the region of the feature map covered by the filter. Thus, the output after max-pooling layer would be a feature map containing the most prominent features of the previous feature map. A 2x2 pool size was used with no stride was used.
FLATTENING LAYER
The flattening layer is used to convert all the resultant 2-Dimensional arrays from pooled feature maps into a single long continuous linear 1-dimensional vector. The flattened matrix is fed as input to the fully connected layer to classify the image.

DROPOUT LAYER
To overcome this problem of overfitting prevalent in many neural network models, a dropout layer is utilised wherein a few neurons are randomly dropped from the neural network during training process resulting in reduced size of the model.
For my model, two dropout layers were used, one before the flattening layer and one before the output layer.

FULLY CONNECTED/ DENSE LAYERS
The Fully Connected (FC) is a feed forward neural network where the weights and biases are calculated for each neuron that is connected with every neuron in the next layer. These layers are usually placed before the output layer and form the last few layers of a CNN Architecture. In this, the input image after flattening is fed to the different FC layers where the mathematical operations usually take place and the classification process begins.
The number of neurons or units to be selected in each layer is arbitrary and somewhat of a trial-and-error process. For my model, 128 units was selected in the dense layer. The final output layer consisted of 10 neurons each representative of the 10 different labels the images had to be classified into.

ACTIVATION FUNCTION
In artificial neural networks, the activation function of a node defines the output of that node given an input or set of inputs. An Activation Function decides whether a neuron should be activated or not. This means that it will decide whether the neuron's input to the network is important or not in the process of prediction using simpler mathematical operations. There are several commonly used activation functions such as the ReLU, SoftMax, tanH and the Sigmoid functions.
For my model, rectified linear activation function or ReLU activation function was which is the most commonly used activation function in deep learning models especially CNN. The function returns 0 if it receives any negative input, but for any positive value xx it returns that value back. So, it can be written as f(x)=max (0, x) f(x)=max (0, x).
For the final output layer, a SoftMax function was used that converts a vector of K real numbers into a probability distribution of K possible outcomes. Simply putting it, in our case, for a given input it will output the probabilities of that image belonging to the 10 different classes. SoftMax is similar to a sigmoid activation function but unlike the latter which is used in binary classification, SoftMax is used for multiclass classification tasks.


MODEL COMPILATION
Model configuration typically requires three main parameters to be decided- the loss function, optimizer and evaluation metric. 
The loss function in a neural network quantifies the difference between the expected outcome and the outcome produced by the machine learning model. From the loss function, we can derive the gradients which are used to update the weights. My CNN model uses sparse categorical cross entropy which is a popular loss function for multiclass classification problems when the classes are mutually exclusive.
An optimizer is a function or an algorithm that modifies the attributes of the neural network, such as weights and learning rate. Thus, it helps in reducing the overall loss and improve the accuracy. For my model, Adam (Adaptive Moment Estimation) optimizer was used which is an extension to stochastic gradient descent and a popular optimizer for neural networks owing to its computational efficiency and fewer parameter requirement for tuning.
For the evaluation metric accuracy was used which simply tells us the percentage of correct classifications made by the model.

MODEL EVALUATION
After 10 epochs an accuracy score of 0.992 with a loss of 0.025 was achieved. A confusion matrix was also created and visualised with the help of a heatmap which showed the number of correct classifications as well the misclassifications for each class. The model has the greatest number of misclassifications for the 9-digit class and the least number of misclassifications for 0- and 1-digit classes.
A graph between the accuracy and validation scores of the training and testing set for the various epochs was plotted. For the training set accuracy shoots up and loss drastically falls down after 2 epochs which continues to reach a stable path by 10 epochs. The validation dataset shows a smoother slow incline for accuracy and decline for loss as the epochs increase. These graphs show that are model performance is excellent.

TESTING THE MODEL WITH DIGITS I WROTE
As part of a mini experiment, in order to test the model’s performance on new data, I wrote a few digits in paint, converted it into images and ran it through the model. The model was successfully able to classify the digits I had written. This was an interesting and exciting way to see how models like CNN perform in the real world.






