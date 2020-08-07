# CS412Machine Learning Project
 This is a team project that includes a image classification task.


1. ABSTRACT

Skin cancer is a serious health problem that is widespread throughout the world. Like any cancer type, skin cancer has more of a chance of treatment if detected early, it has 99% five-year survival rate with a screening after the diagnose (Chaturvedi et al., 2020). This project aims to help early
diagnoses of skin cancer by assisting dermatologist using only the images of the suspected skin segment and Machine Learning (ML) methods that are suitable for this problem. This is a classification problem with 15,000 data instances. The approach to solve this problem involves preparing and preprocessing data, augmentation of data, creating and fine-tuning the model and finally testing to evaluate its success. In first step, we performed a train/test and validation split in data, then we vectorized the images and saved them in .csv files with the IDs and categories. The data was preprocessed and normalized using Keras preprocessing functions, and data were augmented for better training. After that, we tried several different CNN methods, and fine-tuned them. We achieved the best accuracy which is 80.7%, with Transfer Learning more specifically a pretrained ResNet-50 model. This model could be useful in the decision-making process of the dermatologists with a great success rate.


2. INTRODUCTION

The dataset consists of images of parts of skin that has skin cancer, image IDs and the type of skin cancer. It has 15,000 instances and 5 possible types of skin cancer which are melanoma, melanocytic nevus, basal cell carcinoma, actinic keratosis and benign keratosis. They are labeled as 1, 2, 3, 4 and 5 in our model respectively and the image sizes are 600x450 originally. Images needs to be vectorized to be used in mathematical models, the created vectors have integers between 0-255. However, the data needs to be equally scaled, so a normalization to a 0-1 range is needed. Data augmentation is generating more data instances by making minor alternations on the data at hand and it is needed because usually larger data causes better models with increased accuracy.

Keras is a high-level API written in Python designed for deep neural networks. In this project Keras and its CNN (Convolutional Neural Networks) and transfer learning applications are used. Transfer Learning is a learning method where models are pretrained on enormous amounts of data and the best weights are saved for reusing (Brownlee, 2017). This learning method makes the model training faster and the overall performance better. We used pretrained ResNet-50 for this particular problem.


3. APPROACHES

3.1. Preparing and Preprocessing of the data

Usually, the first step in a ML project is to prepare the raw data to a format that is suitable to the chosen ML method. In this case the raw data contained 15000 images that are originally sized 600x450 that needs to be resized, normalized and preprocessed. First, 5,000 data points were split from others and used only for final testing, rest 10,000 were split as 81/9/10 (training/validation/test). Considering 600x450 is not feasible in our case, we resized the images to 224x224. We tried 2 different approaches: first approach is to vectorize and reshape all the images using Image function from PIL (Python Imaging Library) library. After that, we added the vectors to a panda’s data frame with their Image IDs and categories. We saved the ready data frame into a .csv file because vectorizing and resizing takes a lot of time and consumes a lot of RAM. Second approach was to use flow_from_dataframe function, we did not use this approach because it did not give us the desired performance and we were not able to see and change the steps that gave us the data contrary to first approach. Second step was to normalize the data, at first, we simply divided the data by 255 but because it required a lot of RAM and were not as effective, we stopped using this approach. We used
preprocess_input function, which is designed specifically for ResNet, after seeing an improvement in performance and a decrease in RAM usage we decided to use this approach. Additionally, we used this function together with the data augmentation we conducted using DataImageGenerator function to acquire better results.

3.2. Model and Fine-Tuning

ResNet-152 is a 152-layer neural network that is pretrained on millions of images and won the ImageNet competition in 2014. ResNet-50 is a little bit less complex with 50 layers but has the same working principle. We used ResNet-50 in our project because it was a very good and commonly preferred Transfer Learning method that gave much better results and required much less computational power than its alternatives as shown in Figure 1. We tried AlexNet first which is a special CNN, and we got an accuracy of  ~60% and we thought it would be a good baseline. After trying other applications of keras such as VGG-16,NasNetMobile, MobileNet, the best model was decided to be ResNet-50. We fine tuned ResNet-50 model with trying different hyper-parameter combinations and freezing or adding layers. Resulting model has a base of ResNet model, a GlobalAveragePooling2D layer, a Dropout layer with a 0.35 rate and a Dense layer using SoftMax activation. We also use learning rate reduction to decrease the overfitting as well as Dropout and we use checkpoints to get the best model possible.

3.3. Evaluation

Last step of this project is evaluation. The chosen performance metric is accuracy. The process of getting the final score is as follows: we chose the best model by comparing the last epoch’s model’s accuracy and the best model that is saved by the checkpoint. After the best model is used, we predict and evaluate the model using the 10% test data. If it is satisfiable enough, we predict the categories of 5,000 test cases that are absolutely unseen, then we upload this result file to Kaggle. After finding the best model, we trained it again with 97/3 (train/validation) split and again uploaded the final file to Kaggle.


4. CONCLUSION

As a result of this project we created a complete ML model which takes raw image data and predicts the type of skin cancer with 80.7% accuracy. This model consists of the preparation of data, preprocessing and augmenting, and a Deep Neural Network model: ResNet-50. The chosen preparation method decreased the usage of RAM and the time, but it increased the memory usage. Preprocessing method was much faster, used little RAM but we were not able to trace every step to see if it works properly. ResNet-50 is a model that works very effectively and efficiently, but it is a little too complex for this problem and causes some overfitting even after taking actions to avoid overfitting. Accuracy is a very successful performance metric, but it might not be the best for this dataset because the classes are very imbalanced. Overall, this model is successful and might be useful for detecting skin cancer.


    REFERENCES
Figure 1 (Culurciello, 2016)
 Brownlee, J. (2017, December 20). A Gentle Introduction to Transfer Learning for Deep Learning. Retrieved from https://machinelearningmastery.com/transfer-learning-for-deep- learning/
Chaturvedi, S. S., Gupta, K. & Prasad, P.S. (2020). Skin Lesion Analyser: An Efficient Seven-Way Multi-class Skin Cancer Classification Using MobileNet. Advances in Intelligent Systems and Computing, 1141, 165-176. doi: https://doi.org/10.1007/978-981-15-3383-9_15
Culurciello, E. (2016, Jun 20). Training ENet on ImageNet. Retrieved from https://culurciello.github.io/tech/2016/06/20/training-enet.html
