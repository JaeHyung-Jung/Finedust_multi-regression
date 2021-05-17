# Finedust_multi-regression

Finedust Shapvalue(daily)

After selecting the optimal hyper parameter, the Shap Value result according to the change of the input

Model : Multi Linear Regression
```
Model: "sequential"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
dense (Dense)                (None, 64)                576       
_________________________________________________________________
batch_normalization (BatchNo (None, 64)                256       
_________________________________________________________________
dense_1 (Dense)              (None, 64)                4160      
_________________________________________________________________
batch_normalization_1 (Batch (None, 64)                256       
_________________________________________________________________
dense_2 (Dense)              (None, 64)                4160      
_________________________________________________________________
batch_normalization_2 (Batch (None, 64)                256       
_________________________________________________________________
dense_3 (Dense)              (None, 1)                 65        
_________________________________________________________________
batch_normalization_3 (Batch (None, 1)                 4         
=================================================================
Total params: 9,733
Trainable params: 9,347
Non-trainable params: 386
```
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

SHAP VALUE   
![case1_shap](https://user-images.githubusercontent.com/79160507/118438546-83522500-b71f-11eb-8477-16250faa7875.png)   
Loss   
![case1_loss](https://user-images.githubusercontent.com/79160507/118438581-906f1400-b71f-11eb-89ea-09d0a3f142c2.png)
   
Case 2)   
Inputs : {CO, NO2, PM10, PM2.5, SO2}   
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}   
   
SHAP VALUE   
![case2_shap](https://user-images.githubusercontent.com/79160507/118438613-9c5ad600-b71f-11eb-9629-93214c78d809.png)   
Loss   
![case2_loss](https://user-images.githubusercontent.com/79160507/118438633-a41a7a80-b71f-11eb-9f8b-b7a4831d7cb9.png)   

Case 3)
Inputs : {CO, NO2, SO2, PM10≥80, PM2.5≥50, PM2.5≥80}   
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}
   
SHAP_VALUE    
![case3_shap](https://user-images.githubusercontent.com/79160507/118438679-b1d00000-b71f-11eb-9757-febc66862441.png)
   
Loss   
![case3_loss](https://user-images.githubusercontent.com/79160507/118438700-ba283b00-b71f-11eb-93e1-4e90d1f9da36.png)
