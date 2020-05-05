---
published: true
title: Open Jupyter Notebooks in Google Cloud Platform
categories: [GCP,Python]
---

Google cloud platform can be tricky to work with offering so many products and when you are looking to work in your familar Jupyter lab IDE it can be a daunting task to navigate your way in an unfamilar enviroment. While taking numerous courses on coursera I had the Google cloud resources at my disposal and I could try understanding the complex ecosystem of offering

Below is a quick step by step guide on how to launch a python notebook and work with big query tables. 

PS: There can be alternative ways too feel free to explore and share 


Step 1: Once in Google Cloud Console pin the AI platform and open the notebooks which enables you to create a notebook instance and launch Jupyter notebooks 

![](/images/GCP/step1.png){: .center-image }

Step 2: Click on New Instance which by default create a 4vCPU and 16GB RAM notebook instance to host jupyterlab ( preinstalled and preconfigured ) you get the option to customise to R or Python 


![](/images/GCP/step2.png){: .center-image }
![](/images/GCP/step3.png){: .center-image }

```diff
- PS: Creating a new instance is not free and incur charges to account for the time the instance is up and running
```

![](/images/GCP/step4.png){: .center-image }



Step 3: It takes about 2 mins for the instance to be created , Once created click on Open JupyterLab and you have your friendly python notebooks

![](/images/GCP/step5.png){: .center-image }
![](/images/GCP/step6.png){: .center-image }

Step 4: Open a new Python 3 notebook, write BQL styled queries run the job for extracting relevant data for analysis 

![](/images/GCP/step7.png){: .center-image }

Step 5: To avoid your organisation getting billed please stop the instance  



