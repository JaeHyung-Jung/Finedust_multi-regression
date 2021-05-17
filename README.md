# Finedust_multi-regression

Finedust Shapvalue(daily)

After selecting the optimal hyper parameter, the Shap Value result according to the change of the input

Model : Multi Linear Regression
_________________________________________________________________
Layer (type) Output Shape Param #
=================================================================
dense (Dense) (None, 64) 448(Input ±100)
_________________________________________________________________
batch_normalization (BatchNo (None, 64) 256
_________________________________________________________________
dense_1 (Dense) (None, 64) 4160
_________________________________________________________________
batch_normalization_1 (Batch (None, 64) 256
_________________________________________________________________
dense_2 (Dense) (None, 64) 4160
_________________________________________________________________
batch_normalization_2 (Batch (None, 64) 256
_________________________________________________________________
dense_3 (Dense) (None, 1) 65
_________________________________________________________________
batch_normalization_3 (Batch (None, 1) 4
=================================================================
Total params: 9,733(Input ±100)
Trainable params: 9,347(Input ±100)
Non-trainable params: 386
Number of data : 244(weeks) x N(inputs)
   
Inputs : [CO, NO2, PM10, PM2.5, SO2, PM10≥80, PM2.5≥50, PM2.5≥80]
   
Particles(CO, NO2, ... SO2) : Weekly average of particle concentration
Critical Point(PM10≥80, PM2.5≥50, PM2.5≥80) : sum of daily values of Critical Point(0~7)   
   
Case 1) : Results of All inputs   
Case 2) : Put only the particles of the input and exclude the critical point value   
Case 3) : All values ​​of input particles except PM10 and PM2.5   
   
Case 1)
Inputs : {CO, NO2, PM10, PM2.5, SO2, PM10≥80, PM2.5≥50, PM2.5≥80}
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}

<SHAP_VALUE>

<X: Concern, Y: Concern value predicted after learning>

Case 2)
Inputs : {CO, NO2, PM10, PM2.5, SO2}
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}

<SHAP_VALUE>

<X: Concern, Y: Concern value predicted after learning>

Case 3)
Inputs : {CO, NO2, SO2, PM10≥80, PM2.5≥50, PM2.5≥80}
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}

<SHAP_VALUE>

<X: Concern, Y: Concern value predicted after learning>
