# linde_hackathon

## Summary:

* The tanks are classified into limited number of groups
* Preparation of data and label
* constructing and training a model for each group of tanks
* Predicting using the trained models

## Preprocessing (Preprocessing.ipnyb)

* Adding a new feature called Sensor status that gives information whether the sensor is down or not.
* Deals with random 0s in the timestamp
* Dealing with sharp changes in the tank level readings
* Visualization

## Classification of tanks (final_deli_freq_calc.ipynb)

* Having a model for every tank is too costly in all means like memory and computation
* For this purpose the tanks have to be grouped and for each group a model will be used to predict the value. 
* The tanks with similar trend in the level readings should be grouped together. 
* It can be observed that the trend can be defined by the number of deliveries done in a certain time period. 
* Hence we calculate the delivery frequency i.e average of number of days between two consecutive deliveries.
* The tanks with same number of delivery frequency are grouped

## Model (CreateManyModels.ipynb)

* We use reccurrent neural network (LSTM or GRU) to predict the next level readings
* The RNNs are trained for one to one prediction i.e. the models take a single value as input and gives single value as an output
* Hence, if the current reading is given to the model it will give the prediction of next reading
* The model consist of single RNN cell

## Data (CreateManyModels.ipynb)

* The Linde group has provided the instant level readings of the different tanks around the world.
* We create 'processed_level.csv' by removing the noise as we saw in the previous section.
* It might be too hard for the model to predict the number that represents the prediction 
* For this purpose, it is trained to predict only the difference and the direction(whether it increases or decreases)

## Prediction (submission_forecast.ipynb)

* For a given vessel, based on its delivery frequency we select a model to do the prediction
* The output of the selected model gives the difference and direction
* Instead of adding the difference to previous value we add it to the reading which is recorded 10 days back (this value is available in the given data)
* Addition of the difference to 10 days back value gives us the new prediction

## RNN with the use of multiple previous data points (LINDE_Large_Window_Prediction.ipynb)