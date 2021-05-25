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
Number of data : 1244(days) x N(inputs)
   
Inputs : [CO, NO2, PM10, PM2.5, SO2, PM10≥80, PM2.5≥50, PM2.5≥80]
   
Particles(CO, NO2, ... SO2) : Weekly average of particle concentration   
Critical Point(PM10≥80, PM2.5≥50, PM2.5≥80) : sum of daily values of Critical Point(0~7)   
   
Case 1) : Results of All inputs   
Case 2) : Put only the particles of the input and exclude the critical point value   
Case 3) : All values ​​of input particles except PM10 and PM2.5   
   
## Case 1)   
Inputs : {CO, NO2, PM10, PM2.5, SO2, PM10≥80, PM2.5≥50, PM2.5≥80}   
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}

SHAP VALUE   
![case1_shap](https://user-images.githubusercontent.com/79160507/118438546-83522500-b71f-11eb-8477-16250faa7875.png)   
Loss   
![case1_loss](https://user-images.githubusercontent.com/79160507/118438581-906f1400-b71f-11eb-89ea-09d0a3f142c2.png)
   
## Case 2)   
Inputs : {CO, NO2, PM10, PM2.5, SO2}   
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}   
   
SHAP VALUE   
![case2_shap](https://user-images.githubusercontent.com/79160507/118438613-9c5ad600-b71f-11eb-9629-93214c78d809.png)   
Loss   
![case2_loss](https://user-images.githubusercontent.com/79160507/118438633-a41a7a80-b71f-11eb-9f8b-b7a4831d7cb9.png)   

## Case 3)   
Inputs : {CO, NO2, SO2, PM10≥80, PM2.5≥50, PM2.5≥80}   
Parameters : {Epoch:200, batchsize:32, loss : huber, act : sigmoid, layer_shape = [64,64,64,1]}
   
SHAP_VALUE    
![case3_shap](https://user-images.githubusercontent.com/79160507/118438679-b1d00000-b71f-11eb-9757-febc66862441.png)
   
Loss   
![case3_loss](https://user-images.githubusercontent.com/79160507/118438700-ba283b00-b71f-11eb-93e1-4e90d1f9da36.png)

## 2021.5.24   
#### Feedback 및 데이터 추출방법 재설정   
회의 후 Google Trend의 추출 기간을 년단위로 잡으면 데이터가 주간으로 밖에 나오지않아 3개월단위로 데이터를 일간으로 추출해 붙여넣는 방식의 문제점을 발견하여 Naver_DataLab를 통해 데이터를 다시 분석하기로 하였음   
   
Naver_DataLab도 Googletrend와 마찬가지로 해당 포털의 검색량을 기간별로 그래프화 시켜주는 API인데 위의 문제점의 이유로 datalab을 사용하였고 이 경우 또한 네이버만 기반으로하여 데이터가 추출되기 때문에 기타 검색포털(Daum, Google)등을 반영하지 못할것이라는 문제점이 있어 위 3가지 포털을 모두 포함하는 데이터를 추출해주는 KakaoTrend를 사용하려 했으나 KakaoTrend는 조회기간이 2018년 이후부터라서 데이터수의 부족문제가 있었다.   

따라서 Naver_Datalab이 3가지 포털의 데이터를 모두 기반으로하는 KakaoTrend와 검색량의 분포가 크게 다르지않으면 조회기간이 더 넓은 Naver를 사용하자 하였고   
실제로 Correlation분석을 해보니 Naver와 Kakao의 검색량 그래프가 0.921의 수치로 비슷한 경향을 가져 최종적으로 Naver_Datalab을 사용해   
미세먼지 검색량의 데이터를 미세먼지에 대한 관심도값으로 사용하기로 하였음
   
#### Analyzation with Naver_DataLab   


