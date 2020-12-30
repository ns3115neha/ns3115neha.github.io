---
published: true
title: Deploying offline trained models on GCP
categories: [GCP,Python]
---

Recently my team was tasked for lifting and shifting a model currently deployed in Local linux machine to Google Cloud Platform.I found this process quite challenging since storage buckets and IAM permissions on Google cloud platform are controlled by external vendor and since it was first live implementation it was important to understand the architecture of data streams set up


The process of deploying and serving model predictions from GCP is quite straightforward, given the set up is right in first place. ( More on that later) 

There are broadly speaking 5 main steps to deploy model 

1. Have a packaged model ready for deployement 
For our case we used a model trained offline using sklearn and Regularised logistic regression. I will be using sample code with breast cancer data (available in sklearn dataset package) to show to package your model correctly 

2. Create a Google Cloud Storage Bucket
Pitfall : Create the GCS bucket as regional and in the similar region to your Python Notebook instance otherwise your  packaged model packaged file would not be accessible and you may encounter an error "Bad Model Detected"

3. Upload your Packaged Model to GCS Bucket created in above step 

4. Define an AI platform prediction resource 

5. Define an AI platform version resource 



### Packaging a model correctly 

The below sample codes shows how to create a baseline model using breast cancer data and save the model to be copied to GCS bucket and used for creating version 

Constraints 

1. GCP accepts models in format joblib,pickle or protobuf formats
2. GCP has a standard nomenclature for accepting model names and ideally all trained models should be named as model.pkl or model.joblib , naming models with a different name would throw error during version create time 




```python
'''
import sklearn
from sklearn import datasets 
from sklearn import linear_model
import pickle 

#load data
breast_cancer = datasets.load_breast_cancer()

#define baseline model
model = sklearn.linear_model.LogisticRegression()

#save baseline model 
model.fit(breast_cancer.data, breast_cancer.target) 
with open('model.pkl', 'wb') as model_file: 
    pickle.dump(model, model_file)
    
'''
```




### Create a Google Cloud Storage Bucket 

A storage bucket is needed to act as a placeholder for your offline trained model to be deployed. Creating bucket can be done using command line interface or using GUI and following the steps attached

As mentioned earlier it is very important to make sure the region name is same for GCS bucket to that of Notebook instance,This would allow for error free deployement 



```python
'''
$gsutil mb -l <region_name> gs://<bucket_name>
'''

```




    '\n$gsutil mb -l <region_name> gs://<bucket_name>\n'




![](/images/Model_Deployment/Storage_Bucket_Creation_1.PNG){: .center-image }


    
### Upload your Packaged Model to GCS Bucket created in above step 



![](/images/Model_Deployment/Upload_Model_GCS_Bucket.PNG){: .center-image }


### Define an AI platform prediction resource 


There are some pre-requistes before a prediction resouce can be defined. If there is no Python/Tensorflow instance ( Depending on the model you are trying to deploy on cloud) an instance needs to be created 

The model API is by deafult enabled if not kindly enable the API manually in your case 

Once done create a model resource to act as place holder for when the version is created 



![](/images/Model_Deployment/Create_Python_Instance.PNG){: .center-image }
![](/images/Model_Deployment/enable_models_api.PNG){: .center-image }




### Define an AI platform version resource 


If all the above steps have been warning/error free then the below should run smoothly. However some pre-requiste information is needed before creating the version and the commands below can help in identifying the runtime and framework version for the model created

It is very important to specify the right versions for compiling the model else it would throw errors

Once the job is submitted for version creation it would be completed in 2-3 minutes 


```python
# Verify python version installed
from platform import python_version
print(python_version())

```

    3.7.3
    


```python
import sklearn
sklearn.__version__
```




    '0.21.3'





![](/images/Model_Deployment/model_version.PNG){: .center-image }


### Model all Deployed and Ready for serving predictions 

![](/images/Model_Deployment/model_version_created.PNG){: .center-image }

    

### Appendix 

Offical Documentation for deploying models on cloud platform 
https://cloud.google.com/ai-platform/prediction/docs/deploying-models
    
Offical Documentation for serving predictions using deployed models
https://cloud.google.com/ai-platform/prediction/docs/online-predict
    

