# Plothole - An AI aided Pothole Reporting System

The driving experience on roads degrade drastically due to potholes and they are the root cause of a majority of road accidents.
On an average, around 10k road accidents are caused in a year just due to potholes.Currently there are next to no feasible and automated solutions to effectively report potholes.

The components of the system are:

* https://github.com/teambitflip/plothole-validator-backend
* https://github.com/teambitflip/plothole-dashboard
* https://github.com/teambitflip/plothole-app

## Our Solution

Our objective is to design a mobile based dynamic reporting system which will facilitate
the flow of information among the civic authorities. The core part of the solution is a
Deep Learning model that can accurately validate whether an image is a pothole or not
and can assign a severity metric to that image. Use of AI heavily reduces the use of
middlemen to verify the images, this makes the system extremely scalable and helps
take action much faster.

### Mobile + Web

Our solution consists of an android app that citizens can use to click photos of potholes.
The photo is stored on our servers with the gps coordinates and the submission is added
to a job queue. The jobs on the queue are sequentially executed by feeding the
submitted images to a deep learning model which evaluates the validity of the image
(whether its a pothole or not) and its severity. These results are stored on the database. 


A web admin portal, which is meant for the authorities, is used to display the results, sorted
according to severity and validity. We used Firebase for Authentication, Image storage
and Database. The solution is hosted on a Microsoft Azure VM running Ubuntu 18.04.
The android app was built using Kotlin. The admin portal uses React in the frontend. The
backend services are written in Python3 using Flask as an HTTP Router. Redis and RQ
were used to implement the job queuing. Python3 proved to be very useful in integrating
the Deep Learning Model with the backend services.

### Deep Learning

The AI model is constructed on top of Convolutional Neural Networks using transfer
learning on a real world dataset which was collected by us. We have used an
architecture named VGGnet16 which has shown state of the art performance on the
ImageNet challenge previously , we modified and improved it by adding more
convolutional and fully connected dense layers to it, to fine tune the model weights and
processing on the image so that it catches every pixel from the image matrix. We have
trained the model for 40 epochs using mini batch gradient descent where the loss
function was binary-cross entropy.

This classifier has two classes where one shows validity and the other shows the severity
of the pothole if present in the supplied image. We were able to achieve a test accuracy
of 96% on our test dataset as well as real world examples.

[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/made-with-javascript.svg)](https://forthebadge.com)
[![forthebadge](https://forthebadge.com/images/badges/built-for-android.svg)](https://forthebadge.com)


