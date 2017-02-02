# Biolock API

Biolock API is API interface for training and testing ECG data for authentication user.

![Workflow](https://raw.githubusercontent.com/thavryl/BiolockDemo/master/IMG/WorkFlow.png)


Available API:

* [Register API key](#register)
* [Enroll user](#enroll-user-data)
* [Verify test data](#verify-test-data)
    





## Register

| Name          | Type          | Description  |
| ------------- |:-------------:| -----|
| name          | String        | Name which will be used for future contact |
| email         | String        | Email which will be used for future contact |



```sh
$ curl -X POST http://34.198.199.171:1111/register  -d 'name=test&email=test@test.com'
```
  Sample response
```sh
{"Status":"Ok","APIKey":"c6qp3p4i6uulf39ms9f5u1ps6v"}
```

## Enroll user data

Enroll endpoint can be used to train the system to recognize specific user on his/her ECG data. The ECG sample with range of 1000 - 5000 beats is required to get better accuracy. ECG data should be put in CSV file, where each line represent value in millivolts. Sampling rate should be provided as a parameter to the call. The Enroll action can take from 30 seconds to several minutes to complete depending on server load and data size.


| Name | Type          | Description  |
| :-------------|:-------------:|:-----|
| apikey| String        | Your valid api key. |
| upload        | String        | CSV file with your ECG data for user which should be authenticated |


Sample request

```sh
curl -X POST --form upload=@/home/thavryl/ecg2/tarikTrain.csv http://10.128.97.196:1111/addTrainUserData?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```
sample response

```sh
{"Status":"Ok","Message":"Model trained"}
```

## Verify test data

Verify endpoint allows testing user ECG (similar format as for Enroll endpoint), as authentication modality. As a result, validation result (yes/no) and matching probability is returned.


| Name | Type          | Description  |
| :-------------|:-------------:|:-----|
| apikey| String        | Your valid api key. |
| upload        | String        | CSV file with your ECG data for user which should be authenticated

```sh
curl -X POST --form upload=@/home/thavryl/ecg2/tarikTest.csv http://34.198.199.171:1111/verify?apikey=c6qp3p4i6uulf39ms9f5u1ps6v
```
sample response

```sh
{"Status":"Ok","Message":"pass"}  //user didn`t match
or
{"Status":"Ok","Message":"fail"}  //user match
```
