# fine-grain
This project aims to leverage the capabilities offered by a framework called fastai
to implement transfer learning and perform fine grain classification. 
The dataset that is being used to perform this task is the stanford cars dataset. 

# About the dataset
The Cars dataset contains 16,185 images of 196 classes of cars. 
The data is split into 8,144 training images and 8,041 testing images, where each 
class has been split roughly in a 50-50 split.Classes are typically at the level
of Make, Model, Year, e.g. 2012 Tesla Model S or 2012 BMW M3 coupe.

The Dataset hsa been downloaded manually from the following official link:
https://ai.stanford.edu/~jkrause/cars/car_dataset.html
They have been placed in the following file system:
the root folder where this jupyter notebook resides must have a directory by the name 
of fastai/data/.
data directory contains 3 directories and one .mat extension file (cars_test_annos_withlabels.mat)
containig labels for test data: 
1. car_devkit
2. cars_train
3. cars_test

In order to run the project, simply load the data in the above mentioned structure.
And then just run the cells in the order to performa some data cleaning and creating normalized 
dataset.

Then once the 2 palceholders "data" and "test_data" are created. We straight away load the pre-
trained mode called ResNet into a variable called "learn".
We start training the model on the "data" and keep on training it by estimating the correct range 
of learning rate using the methods lr_find() and recorder.plot() with untill we see a plateau in accuracy.
We keep saving the imtermediate models so that we dont have to from scratch again and again. 
So we do the follwing steps once:<br/>
<br/>
*learn = cnn_learner(data, models.resnet152, metrics=[accuracy]).mixup() <br/>
*learn.lr_find()<br/>
*learn.recorder.plot()<br/>
*learn.save('<mode_name>')<br/>


at this point the last group of our neural network named learn has been updated according to out "data".
We use learn.unfreeze() to make all the weights of the neural network modifiable.
Now we need to repeat the follwing steps till we plateau our Accuracy.<br/>

------Repeating Steps------------<br/>

*learn.lr_find()<br/>


*learn.recorder.plot()<br/>


*learn.fit_one_cycle(epochs, lr)<br/>


*learn.save('<mode_name>')<br/>

Once i was satisfied with the model Accuracy, we Call the cnn_learner() method and 
loading the model that we created using load() member function. 


-learn = cnn_learner(data, models.resnet152, metrics=[accuracy]).load('version-5-res152')
and then finally call 


-learn.validate(test_data.valid_dl)


on our "test_data" to validate the accuracy.







