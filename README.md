# GradDesc

This is a user manual of using the R package GradDesc. The purpose of the GradDesc package is to make a binary logistic regression with the use of the stochastic gradient descent algorithm. It works on every dataset but the exploratory variables have to be quantitative and the target variable has to be binary.
In this demonstration, we are going to use two differents datasets : “breast_cancer” and "default_of_credit_card_clients" from UCI dataset to see how the algorithm behaves by exploiting the capacities of multicore processors.

Installing the package and access to the library
----------------------
    
    install.packages("devtools")
    library(devtools)

    devtools::install_github("FD155/GradDesc")
    
    library(GradDesc)
    
How to understand the expectations of the function parameters
----------------------   
You can just use the fonction help(function name) to see all the documentation about your function.

    help("fit")
   
----------------------  
    
Short descriptions of datasets
----------------------   

### Breast Cancer : 

This first dataset is about breast cancer diagnostic. Features are computed from a digitized image of a breast mass. The dataset contain 699 observations and 10 columns. The target variable is the class with two modalities : malignant cancer or begnin cancer. 

<img width="620" alt="Capture d’écran 2021-11-26 à 19 31 11" src="https://user-images.githubusercontent.com/73121667/143619934-0c3f828b-8c78-44bc-b141-85016d5d4bb0.png">


### Default of credit card clients :

The "default of credit card clients" data frame has 30 000 rows and 24 columns of data from customers default payments research. This research employed a binary variable, default payment (Yes = 1, No = 0), as the response variable.

<img width="649" alt="Capture d’écran 2021-11-26 à 19 43 24" src="https://user-images.githubusercontent.com/73121667/143620746-5a553513-0c7b-47eb-b1f7-cf3d447f1301.png">



    
Demonstration
----------------------  


Load your dataset
----------------------  
First, load your dataset on R like the example below. We begin with the shortest dataset, breast cancer.
    
    library(readxl)
    data <- read_excel("/Users/.../breast.xlsx")


Fit function
----------------------   
To use the GradDesc R package, the first function you have to call is the fit function which correspond to the implementation of binary logistic regression with stochastic gradient descent. The possibility of exploiting the capacities of multicore processors is available for the batch mode of the gradient descent. To detect the number of cores you have access on your computer, use this code :

    library(parallel)
    detectCores()
    
Then, call the fit function and store the function call in an object variable. You have to informed the target variable and the explanatory variables in the formula parameter. The example below show you how to use the fit function.

    LogisticRegression <- fit(formula=classe~.,data=data,coef=0.5,mode="batch",batch_size=0,learningrate=0.1,max_iter=100)
    
You must obtain a graphic like this one which show you the loss function according to the number of epochs. Here, we chose the mode "batch" of the gradient descent with a number of iteration fixed at 100.

<img width="648" alt="Capture d’écran 2021-11-26 à 20 10 16" src="https://user-images.githubusercontent.com/73121667/143622527-1f828441-f0f8-4031-81a5-7ee5a4505372.png">


To see the gradient descent, print or summarize it like this :

    print(LogisticRegression)
    summary(LogisticRegression)

The print call inform you which modality the algorithm takes as the positive modality. By default, it takes the modality that appears first in the dataset. This first call also show the number of epochs, the gradient descent use to converges to the final coefficients. You have access to these final coefficients and the loss function at each iteration. The summary call also gives you the formula on which the descent gradient is based. 


Predict function
----------------------   
The second function of the package is the predict function.


----------------------  

Let’s practice on your own dataset
----------------------  
Now that you have seen how the package works, it is up to you to use it on your own data. Remember to use the help() function to access to all the documentation.

Authors
----------------------  

Franck Doronzo, Candice Rajaonarivony, Gwladys Kerhoas
