# Biolock API

Biolock API is API interface for training and testing ECG data for authentication user.
![Workflow](https://raw.githubusercontent.com/thavryl/BiolockDemo/master/IMG/WorkFlow.png)


Available API:
    - **[Register API key](#register)**  
    - **[Upload data for train](#Train-data)** 
    - **[Upload data for test](#Test-data)** 
    - **[Train your network](#Train-network)**
    - **[Clean user ECG data](#Clean-user-ECG)**
    - **[Clean test ECG data](#Clean-test-ECG)**
    - **[Validate test user](#Validate)**






## Register

- @name -your name for future contact.
- @email -your email for future contact.
```sh
$ curl -X POST http://10.128.97.196:1111/register  -d 'name=test&email=test@test.com'
```
  Sample response
```sh
{"Status":"Ok","APIKey":"c6qp3p4i6uulf39ms9f5u1ps6v"}
```

## Train data
 
- @apikey -your valid api key. 
- @upload -CSV file with your ECG data for user which should be authenticated.
 
```sh
curl -X POST --form upload=@/home/thavryl/ecg2/tarikTrain.csv http://localhost:1111/addTrainUserData?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```
sample response

 ```sh
{"Status":"Ok","Message":"File added"}
```

## Upload test data
 
- @apikey -your valid api key.
- @upload -CSV file with your ECG data for user which will be tested.
 
```sh
curl -X POST --form upload=@/home/thavryl/ecg2/tarikTest.csv http://localhost:1111/addTestUserData?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```
sample response

```sh
{"Status":"Ok","Message":"File added"}
```


## Train model
  System is trained based on previously uploaded training data 
- @apikey -your valid api key.
    
```sh
    curl -X POST http://localhost:1111/trainNetworkForAPIKey?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```

- Note training process might take about 1 minute

 Sample response 
 
```sh
  {"Status":"Ok","Accuracy":" 0.944599"} 
```


## Clean train data ECG
- @apikey -your valid api key.

```sh
  curl -X POST   http://localhost:1111/cleanTrainUserData?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```

Sample response

```sh
 {"Status":"Ok","Message":"Files deleted"}
```


## Clean test data ECG
- @apikey -your valid api key.

```sh
  curl -X POST   http://localhost:1111/cleanTestUserData?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```

Sample response

```sh
 {"Status":"Ok","Message":"Files deleted"}
```

## Validate user  
 Test data is used for validation 

- @apikey -your valid api key.


```sh
    curl -X POST http://localhost:1111/validateUser?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```
Sample response
```sh
   {"Status":"Ok","result":{"predictions":0.97727275,"probability":0.95189613}}
```





