---
title: Phishing Websites Detection
author: Vishwa Vasu
type: post
date: 2023-11-20T20:31:43+00:00
url: /detect-phishing-urls-using-machine-learning/
featured_image: /wp-content/uploads/2023/11/phishing-websites-high-resolution-logo-480x360.png
nimbo_mb_gallery_thumb_type:
  - slider
nimbo_mb_video_thumb_type:
  - iframe
nimbo_mb_audio_thumb_type:
  - iframe
nimbo_mb_link_target:
  - blank
categories:
  - Machine Learning
tags:
  - AI
  - machinelearning
  - ML
  - phishing
  - phishingurl
  - phishingwebsites
  - URLs

---
<a href="https://www.w3schools.com/python/python_ml_getting_started.asp" target="_blank" rel="noreferrer noopener" data-type="URL" data-id="https://www.w3schools.com/python/python_ml_getting_started.asp">Machine learning</a> trains a computer to make decisions by studying data and statistics.



Machine learning originated in the 1950s with the development of Artificial intelligence. Machine learning is a sub of Artificial Intelligence that shares AI&#8217;s natural characteristics. Deep learning is also a subfield of machine learning, and its concept is based on artificial neural networks.



Machine learning makes decisions by studying the data and statistics. Machine learning can be classified mainly into four parts.



<ul class="wp-block-list">
  <li style="list-style-type: none;">
    <ul>
    </ul>
  </li>
</ul>

<li style="list-style-type: none;">
  <ul>
    <li>
      Supervised Machine Learning
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Unsupervised Machine Learning
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Semi-Supervised Machine Learning
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Reinforcement Machine Learning
    </li>
  </ul>
</li>





I have used the <a href="https://www.ibm.com/topics/machine-learning" target="_blank" rel="noreferrer noopener" data-type="URL" data-id="https://www.ibm.com/topics/machine-learning">supervised machine learning</a> model for this project. Supervised learning predicts the results based on the sample inputs. The supervision of human interference is led by supervised learning. It used labelled data as classifications that help to pre-define the outcome.



## Introduction of Phishing:



This is an attempt to detect phishing URLs using machine learning techniques. First of all, let&#8217;s check what Phishing and Phishing URLs are.



Phishing is one of the well-known social engineering attacks. Cybercriminals employ ambiguous approaches to trick victims into divulging sensitive information or taking actions which could compromise their privacy and financial well-being. Human emotions and human errors are mainly caused by phishing attacks since keywords such as &#8220;payment&#8221; and &#8220;hacked&#8221; are used to evoke and make short-sighted decisions from victims.



The website Phishing category has become a prevalent and ever-evolving threat to cyber security. Website Phishing is associated with forged websites that camouflage legitimate platforms such as online banking and social media. These forged websites are designed to gimmick the users to provide credentials and personal information like credit card details and social security numbers. Being a victim of a Phishing attack could be severe. The information stolen by fraudulent websites can lead to identity theft, unauthorised access, and financial fraud.



Protecting from Phishing websites requires awareness, caution, and security measures. The users should inspect the legitimacy of a website by checking the secure hypertext transfer protocol (HTTPS), the sign of authenticity from padlock icons or a trusted certificate. Nevertheless, the latest phishing techniques are designed not to identify by only inspecting the legitimacy and authenticity since the most unsuspecting phishing websites are almost identical to legitimate websites. Therefore, it requires a more robust way to detect a possible Phishing attempt since a considerable amount of traffic is generated in a single host in a business-like operation, and inspection is impossible.



The feature extraction method is one way of detecting Phishing with machine learning. The characteristics of web links take into consideration labelling. Attributes such as the presence of an IP address instead of a domain address, HTTP instead of HTTPS, length of the URL, the presence of symbols in the URL such as &#8220;.&#8221;, &#8220;@&#8221;, &#8220;/&#8221;, and &#8220;#&#8221; and the count of the symbols are features, tiny URLs that are usually used for detectable characteristics and WHOIS information, DNS information, status code, and SSL certification features that are used to label URLs by inspecting the exclusive information by programming the inspection.



However, most legitimate and Phishing websites are almost identical in URL frame features. It does not make any significance to the accuracy of the machine learning, and the results could give a false positive result. Therefore, this research will only consider programmable inspections to identify the non-detectable characteristics in visible form and the presence of HTTP instead of HTTPS.



This research blog relies on feature extraction on URLs. The URLs from the datasets will run through several feature extraction methods to identify the unique features in Phishing URLs and Legitimate URLs. The following feature extraction methods will run through each URL.



<ul class="wp-block-list">
  <li style="list-style-type: none;">
    <ul>
    </ul>
  </li>
</ul>

<li style="list-style-type: none;">
  <ul>
    <li>
      The presence of &#8220;HTTP&#8221; instead of &#8220;HTTPS.&#8221;
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Presence of WHOIS information availability
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Validity of the domain age
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Status code of the domain
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Sender Policy Framework availability
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      IP address resolvable from the domain
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      The resolved IP address is Blacklisted or not Blacklisted
    </li>
  </ul>
</li>



<li style="list-style-type: none;">
  <ul>
    <li>
      Availability of the subdomains
    </li>
  </ul>
</li>





The datasets for the research have been collected from the following sources. Phishing websites have been collected from the Phishtank organisation. The Cisco Talos Intelligence Group operates it. In this dataset, there are more than 60000 verified Phishing website records. The reliability of this source is high since the URLs submitted to the database have to be confirmed as Phishing by the organisation before being published to the public.



The legitimate website information was collected from the &#8220;Majestic Million&#8221; web service. The Majestic dataset is listed with the most referring subnets on the Internet. This research follows feature engineering and binary classification theory. Therefore, 15000 URLs have been taken into feature extraction from each dataset. Jupyter Notebook has been chosen as the IDE for this research, and Python is used for programming with machine learning.



**Note:** The results may vary according to the machine&#8217;s performance, and the project is not about 100% accurate outcome. It&#8217;s about how we can use artificial intelligence techniques in cybersecurity.



## Coding:



Importing the required packages.



    import ipwhois.exceptions
    import whois
    from ipwhois import IPWhois, IPDefinedError
    import requests
    from urllib.parse import urlparse,urlencode
    from urllib.parse import urlparse
    from urllib3.exceptions import ReadTimeoutError
    import ipaddress
    import dns.resolver
    from bs4 import BeautifulSoup
    import OpenSSL
    import socket
    import ssl, socket
    import re
    import os
    from datetime import datetime
    import datetime
    import time
    from sklearn.preprocessing import StandardScaler
    #Numerical Operations and Data Visualisation packages
    import pandas as pd
    import numpy as np
    import seaborn as sns
    import matplotlib.pyplot as plt
    import math
    #XGBoost Classification model
    from xgboost import XGBClassifier
    #Train and Test data ration Modelling 
    from sklearn.model_selection import train_test_split
    #Confusion matrix and classification report packages
    from sklearn.metrics import confusion_matrix
    from sklearn.metrics import classification_report
    from sklearn.metrics import recall_score
    from sklearn.metrics import precision_score
    from sklearn.metrics import accuracy_score
    from sklearn.metrics import f1_scoreC
    #AUC-ROC analysis package
    from sklearn.metrics import roc_curve, roc_auc_score
    import sklearn.metrics as metrics
    #Package for store data
    import pickle



Loading the test dataset.



    df = pd.read_csv("verified_online.csv")



## Proposed feature extraction methods for Phishing detection:



### The presence of&#8221; HTTP&#8221; instead of&#8221; HTTPS&#8221;

Almost all the URLs contain an extra layer of security: &#8220;HTTPS&#8221;. With &#8220;HTTPS,  
webpage contents are encoded and encrypted, and &#8220;HTTP-only website contents are transferred in clear text. The &#8220;HTTP&#8221; existence returns as &#8220;1&#8221;.



    def ishttp(Address):
       parsed_url = urlparse(Address)
       if parsed_url.scheme == 'http':
         return 1
       elif parsed_url.scheme == 'https':
         return 0
       else:
         return 0



### Presence of WHOIS information availability

WHOIS protocol retrieves information about the registered domain names and IP addresses. It gives information about the domain&#8217;s ownership, registration, and administrative information. That information is stored in the public WHOIS database. When a website is registered, the registrar collects the information from the registrant. This feature checks for the registrar information&#8217;s availability and returns &#8220;1&#8221; if it does not exist.



    def domain_validity(Address):
       try:
           url = whois.whois(Address)
           entry = url.registrar
       if entry is None:
           return 1
       else:
           return 0
       except whois.parser.PywhoisError:
           return 1



### Validity of the domain age

WHOIS protocol has information regarding domain registration and expiration dates. This research looks for the age of the domain, and if the age is less than six months, it returns &#8220;1&#8221;. The newly registered domains tend to be suspicious; thus, Phishing theory has been considered.



    def get_domain_age(Address):
      try:
         domain_info = whois.whois(Address)
         if isinstance(domain_info.creation_date, list):
             creation_date = domain_info.creation_date[0]
         else:
             creation_date = domain_info.creation_date
         if creation_date:
             current_date = datetime.datetime.now()
             age = (current_date - creation_date).days
             if age < 180:
               return 1
             else:
               return 0
         else:
             return 0
      except socket.gaierror:
         return 1
      except requests.ConnectionError:
         return 1
      except ssl.SSLError:
         return 1
      except ConnectionRefusedError:
         return 0
      except TimeoutError:
         return 1
      except requests.ReadTimeout:
         return 1
      except ReadTimeoutError:
         return 1
      except requests.exceptions.TooManyRedirects:
         return 1
      except whois.parser.PywhoisError:
         return 1
      except TypeError:
         return 1
      except UnicodeError:
         return 0



### Status code of the domain

Attackers often pay attention to the status code &#8220;500&#8221;, as targeting the internal servers could lead to offensive success. The status code &#8220;302&#8221; appears if the web application redirects to another web. Therefore, this function checks for the status codes starting with &#8220;5&#8221; and &#8220;3&#8221; and returns one if true.



    def status_code(Address):
       try:
          headers = {
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)
    AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.
    36'}
          response_info = requests.head(Address, headers=headers,
          allow_redirects=False, timeout=10)
          status = response_info.status_code
          if str(status).startswith('3') or str(status).startswith('5'):
             return 1
          else:
             return 0
       except requests.ConnectionError:
          return 0
       except requests.exceptions.ReadTimeout:
          return 0
       except requests.exceptions.Timeout:
          return 0
       except requests.exceptions.TooManyRedirects:
          return 1
    



### Sender Policy Framework availability

SPF record is used to prevent spoofing of sender addresses in emails. Thereby, the receiving party of the email can ensure that an email has been received from the authorised email sender of the domain. This function is taken as an assumption as if a Phishing website sends an email Phishing to victims by replicating an original website or covering the tracks of discovering the sender by removing the SPF records from DNS records. It returns &#8220;1&#8221; if the SPF record cannot be found in the domain.



    def spf_check(Address):
       try:
         domain = urlparse(Address).netloc
         response_dns = dns.resolver.resolve(domain, 'TXT')
         spf_info = response_dns.response.answer
         if 'spf1' in str(spf_info):
             return 0
         else:
             return 1
       except dns.resolver.NoAnswer:
          return 1
       except dns.resolver.NXDOMAIN:
          return 1
       except dns.resolver.NoNameservers:
          return 1
       except dns.exception.Timeout:
          return 1



### IP address resolvable from the domain

Due to coverups and exceptions, some URLs cannot be translated into IP addresses. Those URLs are assumed suspicious in this research, and the URLs do not give an IP address return as &#8220;1&#8221;.



    def ip_availability(Address):
       try:
          domain = urlparse(Address).netloc
          ip = socket.gethostbyname(domain)
          if isinstance(ip, str):
             return 0
          else:
             return 1
       except socket.gaierror:
          return 1



### The resolved IP address is Blacklisted or not Blacklisted

If the fixed IP addresses have records of being blocklisted for bad reputations, those URLs are assumed to be suspicious in this research. The continuously updated blocklist of IP address data has been used to check the blocklist IP address. Actual events return the presence of a blocked IP for that URL.



    def blacklist_ip(Address):
       try:
          domain = urlparse(Address).netloc
          ip = socket.gethostbyname(domain)
       except socket.gaierror:
          return 0
       except ipwhois.exceptions.IPDefinedError:
          return 0
       with open(r"blackip.txt", 'r') as fp:
          for l_no, line in enumerate(fp):
              if ip in line:
                 return 1
              else:
                 return 0



### Availability of the subdomains

**  
** Phishers could use the opportunity to have subdomains in their domain to make the URL appear legitimate. Therefore, this function checks for the subdomains and excludes the main domain and the top-level domain, and if there are any domains other than those domains, it returns true, which is suspicious according to this research.



    def get_subdomains(Address):
       parsed_url = urlparse(Address)
       subdomains = parsed_url.hostname.split(".")
       if len(subdomains[:-2]) > 0:
          return 1
       else:
          return 0



The features mentioned above compile and join with the following function.



    def featureExtraction():
      features = []
      features.append(Address)
      features.append(ishttp(Address))
      features.append(domain_validity(Address))
      features.append(get_domain_age(Address))
      features.append(status_code(Address))
      features.append(spf_check(Address))
      features.append(ip_availability(Address))
      features.append(blacklist_ip(Address))
      features.append(get_subdomains(Address))
      features.append(Label)
      return features



This research labels phishing websites as&#8217; 1&#8242; and Legitimate websites as&#8217; 0&#8242;. The example code shows the Phishing URL labelling. This loop goes through each URL and compiles the functions mentioned above. Finally, join all extracting features results.



    phish_features = []
    Label = 1
    for i in range(0,len(df)):
        Address = df['Address'][i]
        print(i)
        phish_features.append(featureExtraction())



## The final feature extracted dataset for Phishing website detection



    data.head()

<figure>

<img decoding="async" src="https://vazdefense.com/wp-content/uploads/2023/11/fxctphishing.png" alt="" /> 

<figcaption>Last Feature Extracted Dataset for Phishing</figcaption> </figure> 



### Assumptions in Phishing Data Classification

The Phishing dataset has been generated using two different datasets. The verified Phishing URLs have been collected from the PhishTank organisation&#8217;s developer&#8217;s information. Since identifying Phishing websites relies on domain features, legitimate URLs have been collected from the Majestic Million dataset. It has only the domain name without any navigation paths in the URI. Moreover,&#8221; HTTPS&#8221; is externally included for each URL.





## Statistical and Visual Analysis



    data.hist(bins = 50, color = 'Blue', lw=10, figsize = (15,15))
    plt.show()

<figure>

<img decoding="async" src="https://vazdefense.com/wp-content/uploads/2023/11/statgraphphish.png" alt="" /> 

<figcaption>Visualisation of data circulation in Phishing Dataset</figcaption> </figure> 



The following figure shows how the feature extracted dataset has distributed its features in statistical form. According to that data, the SPF availability and count of the subdomains offer a nearly balanced feature.



    data.describe()



The following figure is the graphical representation of the statistical distribution of data. It graphically shows the balanced distribution of Phishing, legitimate labelling, and other features.

<figure>

<img decoding="async" src="https://vazdefense.com/wp-content/uploads/2023/11/statphish-1024x262.jpg" alt="" /> 

<figcaption>Mathematical description/statistic of Phishing dataset</figcaption> </figure> 



The correlation heatmap represents the correlation between the data. The strong relationships are shown with dark blue, and light colours show the weak/negative relationships between the data. The&#8217; Label&#8217; should be ignored since it does not make sense to the machine learning program. Therefore, strong correlations are shown for the phishing websites, which are the count of subdomains and SPF availability, the IP address availability for the domain, the age of the domain, and SPF availability.



    correlation_matrix_sns = data.corr()



I created the Seaborn Heatmap and defined the feature relations&#8217; chart size, visualisation colours, width, and roundup values.



    plt.figure(figsize=(10,8))
    sns.heatmap(correlation_matrix_sns, annot=True, cmap='Blues', fmt='.2f', linewidths=0.5)
    plt.title('Correlation Heatmap')
    plt.show()

<figure>

<img decoding="async" style="width: 507px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/hmphish.png" alt="" /> 

<figcaption>Correlation HeatMap of Phishing Dataset</figcaption> </figure> 



I am defining&#8217; X&#8217; and&#8217; y&#8217;. Extract the&#8217; Label&#8217; column and store it in the variable&#8217; y&#8217;. Drop the&#8217; Label&#8217; column and keep the data frame variable&#8217; X&#8217;.



    y = data['Label']
    X = data.drop('Label',axis=1)
    X.shape, y.shape



I am separating the labelled dataset into train and test sets: 80-20 split ratio and getting the shape of training and test feature arrays. X\_train : (80% ratio, eight features), X\_test (20% ratio, eight features)importing the required packages.



    X_train, X_test, y_train, y_test = train_test_split(X, y,test_size = 0.2, random_state = 12)
    X_train.shape, X_test.shape



I am creating holders to store the model performance results and make a function to call for storing the results of classification report data.



    ML_Model = []
    acc = []
    prec = []
    rec = []
    f1 = []
    def storeResults(model, a,b,c,d):
        ML_Model.append(model)
        acc.append(a)
        prec.append(b)
        rec.append(c)
        f1.append(d)



## Machine Learning



In the research, I used seven different machine-learning algorithms. But in this blog, I will use only one machine learning algorithm for the demonstration for simplification purposes.



_XGBoost  
Random Forest  
Decision Tree  
MLP  
KNN  
Naïve Bayes  
SVM_



### XGBoost ML Model



Instantiate and train the model.



    xgb = XGBClassifier(learning_rate=0.4,max_depth=7)
    xgb.fit(X_train, y_train)



Predicting the target value from the model for the test.



    y_test_xgb = xgb.predict(X_test)



Create a confusion matrix for the XGBoost Model and name the value labels.



    cm_xgb = confusion_matrix(y_test, y_test_xgb)
    cm_xgb = pd.DataFrame(cm_xgb, index=['Actual Negatives', 'Actual Positives'], columns=['Predicted Negative', 'Predicted Positive'])



Generating the classification report and naming the target names.



    target_names = ['Legitimate', 'Phishing']
    cl_report = classification_report(y_test, y_test_xgb, target_names = target_names)
    



Plot the confusion matrices and define the attributes of the figure.



    plt.figure(figsize=(12,6))
    plt.subplot(1,2,1)
    sns.heatmap(cm_xgb, annot=True, fmt='d', cmap='Blues')
    plt.xlabel('Predicted')
    plt.ylabel('Actual')
    plt.title('XGBoost Confusion Matrix')
    plt.tight_layout()
    plt.show()



The XGBoost machine learning model performed best among the other machine learning models used in this research. The following is the confusion matrix correctness of the representation model and errors. According to the XGBoost confusion matrix among 6000 testing data, TN (True Negative) value is 2845 as actual negatives represented in the dataset, FP (False Positive) value is 181 as predicted positives for the testing dataset, FN (False Negative) value is 391 as the expected negative for the testing dataset. Finally, the TP (True Positive) value is 2583 as predicted positives. Therefore, overall, the XGBoost did a significant job in this research for Phishing website prediction.

<figure>

<img decoding="async" style="width: 404px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/xgbphish.png" alt="" /> 

<figcaption>Highest accuracy given model for Phishing detection</figcaption> </figure> 



Extracting classification report data for evaluation.



    rs = recall_score(y_test,y_test_xgb)*100
    rs = math.ceil(rs*100)/100
    rs = np.float64(rs)
    ps = precision_score(y_test,y_test_xgb)*100
    ps = math.ceil(ps*100)/100
    ps = np.float64(ps)
    asc = accuracy_score(y_test,y_test_xgb)*100
    asc = math.ceil(asc*100)/100
    asc = np.float64(asc)
    fs = f1_score(y_test,y_test_xgb)*100
    fs = math.ceil(fs*100)/100
    fs = np.float64(fs)



I am storing the results for evaluation.



    storeResults('XGBoost', rs,ps,asc,fs)



<mark style="background-color: rgba(0, 0, 0, 0);">Other ML algorithms have not been mentioned here.</mark>



## Summarising the accuracies



    results = pd.DataFrame({ 'ML Model': ML_Model,'Accuracy %': acc, 'Precision %' : prec, 'Recall %' : rec, 'F1 Score %' : f1})
    results



Sorting the data frame by the accuracy.



    results.sort_values(by=['Accuracy %', 'Precision %'], ascending=False)

<figure>

<img decoding="async" style="width: 469px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/phiacc-1024x461.jpg" alt="" /> 

<figcaption>Summary of ML Performance for Phishing</figcaption> </figure> 



## ROC Analysis



The ROC curve is a figure that shows the sensitivity on the y-axis as the True Positive. Rate against the specificity on the x-axis as the False Positive Rate. The 45-degree diagonal line corresponds to the random chance. The AUC(Area Under the Curve) represent all the ML models used in this research. According to the representation of the AUC, except for the Naive Bayes model, the other ML models have shown more than a 93% chance that those models will be able to differentiate between positive and negative classes.



    #Defying the figure size
    plt.figure(figsize=(8,6))
    #define metrics
    #Predict probabilities for each ml model
    y_pred_proba_dt = tree.predict_proba(X_test)[::,1]
    y_pred_proba_mlp = mlp.predict_proba(X_test)[::,1]
    y_pred_proba_xgb = xgb.predict_proba(X_test)[::,1]
    y_pred_proba_knn = knn.predict_proba(X_test)[::,1]
    #y_pred_proba_svm = svm.predict_proba(X_test)[::,1]
    y_pred_proba_forest = forest.predict_proba(X_test)[::,1]
    y_pred_proba_nb = nb.predict_proba(X_test)[::,1]
    #Calculate the ROC curve and AUC for each model
    fpr_dt, tpr_dt, threshold_dt = metrics.roc_curve(y_test,  y_pred_proba_dt)
    fpr_mlp, tpr_mlp, threshold_mlp = metrics.roc_curve(y_test,  y_pred_proba_mlp)
    fpr_xgb, tpr_xgb, threshold_xgb = metrics.roc_curve(y_test,  y_pred_proba_xgb)
    fpr_knn, tpr_knn, threshold_knn = metrics.roc_curve(y_test,  y_pred_proba_knn)
    #fpr_svm, tpr_svm, threshold_svm = metrics.roc_curve(y_test,  y_pred_proba_svm)
    fpr_forest, tpr_forest, threshold_forest = metrics.roc_curve(y_test,  y_pred_proba_forest)
    fpr_nb, tpr_nb, threshold_nb = metrics.roc_curve(y_test,  y_pred_proba_nb)
    auc_dt = metrics.roc_auc_score(y_test, y_pred_proba_dt)
    auc_mlp = metrics.roc_auc_score(y_test, y_pred_proba_mlp)
    auc_xgb = metrics.roc_auc_score(y_test, y_pred_proba_xgb)
    auc_knn = metrics.roc_auc_score(y_test, y_pred_proba_knn)
    #auc_svm = metrics.roc_auc_score(y_test, y_pred_proba_svm)
    auc_forest = metrics.roc_auc_score(y_test, y_pred_proba_forest)
    auc_nb = metrics.roc_auc_score(y_test, y_pred_proba_nb)
    #Visualising AUC accuracy in the ROC graph
    plt.plot(fpr_dt,tpr_dt,color='b', label="AUC_dt="+str(np.float16(auc_dt)))
    plt.plot(fpr_mlp,tpr_mlp,color='r', label="AUC_mlp="+str(np.float16(auc_mlp)))
    plt.plot(fpr_xgb,tpr_xgb,color='g', label="AUC_xgb="+str(np.float16(auc_xgb)))
    plt.plot(fpr_knn,tpr_knn,color='y', label="AUC_knn="+str(np.float16(auc_knn)))
    #plt.plot(fpr_svm,tpr_svm,color='c', label="AUC_svm="+str(np.float16(auc_svm)))
    plt.plot(fpr_forest,tpr_forest,color='m', label="AUC_forest="+str(np.float16(auc_forest)))
    plt.plot(fpr_nb,tpr_nb,color='#EDB120', label="AUC_nb="+str(np.float16(auc_nb)))
    #Visualises the ROC analysis graph
    plt.plot([0,1],[0,1],color='gray', linestyle='--', label="Reference Line")
    plt.title('ROC Analysis')
    plt.ylabel('True Positive Rate')
    plt.xlabel('False Positive Rate')
    plt.legend(loc='lower right')
    plt.show()

<figure>

<img decoding="async" style="width: 454px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/aucrocphish.png" alt="" /> 

<figcaption>AUC-ROC analysis for Phishing</figcaption> </figure> 



All machine learning models have given more than 85% accuracy except the Naïve Bayes model. The XGBoost model&#8217;s training accuracy hits 86.86%, and the precision is 93.6%. The k-Nearest Neighbour model has a slightly lower accuracy of 85.88% and a precision of 94.32%. The other machine learning models, except the Naïve Bayes, hang on similar accuracy and precision range. The Naïve Bayes model gives a noticeably lower accuracy, as 46.47% and 96.11% precision rate.



As it gives considerable accuracy for the pre-labelled dataset, the coded program has given the confidence of work, and a test with a limited feature extraction dataset had given the question of accuracy that dataset could reach. Then, in the second phase, this research&#8217;s labelled and balanced dataset was loaded into the model accuracy testing. The Phishing dataset generated with feature extraction methods in this research has given considerably higher accuracy for just eight features compared to the 111 features extracted dataset. The ideal testing to identify new Phishing URLs with the discovered machine learning algorithm will be used in the Testing chapter to check the usefulness of this Phishing detection research.



## Saving the best model for future work



With the help of the pickle package, the best model will be serialised and saved as a binary format.



    pickle.dump(xgb, open("xgb2.pickle.dat", "wb"))



The serialised data is deserialised and loaded into the memory.



    loaded_model = pickle.load(open("xgb2.pickle.dat", "rb"))
    loaded_model



## Testing



The ML model saved earlier will be used for the predictions for testing data.



    model = loaded_model



The feature extracted testing data loaded into a new DataFrame for testing.



    test_data = pd.read_csv('mix_new_ext.csv')



This removes the Label column from the original dataset and loads it into a new variable. The original remains unchanged with&#8217; test_data.&#8217;



    test_pred = test_data.drop('Label', axis=1)



The trained machine learning model is used for the predictions for testing data.



    predictions = model.predict(test_pred)



Make a Numpy array from predictions.



    prd = predictions
    pred_array = np.array([prd])



Get the count of negatives(0) and positives(1) from the Numpy array.



    negative = np.count_nonzero(pred_array == 0)
    positive = np.count_nonzero(pred_array == 1)
    math_array = ([negative, positive])



Naming the labels of the Pie Chart for Phishing



    chart_labels = ['Legitimate', 'Phishing']
    chart_explode = [0.2, 0]



Phishing testing has been conducted using numerous new data methods. The Phishing URL prediction accuracy was 86.86% for the Phishing dataset. Therefore, the testing accuracies will vary on testing data. The latest data from the sources used to generate the final Phishing detection dataset will be used here for testing. A custom-made Phishing URL has been used as a unique experiment to check accuracy. All the testing data were run through the feature extraction methods for Phishing before testing.



A phishing attack has been generated using Kali Linux tools. A login form has been  
cloned to make the Phishing seem legitimate from the&#8221; Vazdefense.com&#8221; cybersecurity blog. (Vishwa Vasu, I own all the rights to this blog) Furthermore, the link is prepared for work over the Internet. The phishing link has mixed legitimate URLs, phishing URLs, and a mix of both for prediction tests. The original link is long; therefore, a tiny URL service is used to shorten the URL and make it more legitimate.



### Generated Phishing with legitimate URLs: Test 1



The prepared Phishing and legitimate URLs have been mixed and submitted to the feature extraction methods. As per the extracted features, the functions have identified unique characteristics. Even though the tiny URL service shortens the URL, that URL is parsed by &#8220;HTTP&#8221;, and the status code of the link is&#8221; 302&#8243; since it is redirected to the attacker&#8217;s machine. Therefore, those two characteristics were enough for the algorithm to identify the link as Phishing. The test was conducted with 10 URLs. The generated Phishing URL has input as the last URL. The machine learning model gave 81.8% prediction for legitimate data and 18.2% for Phishing data. It means that 2 URLs from that dataset have been predicted as Phishing, including the generated Phishing URL.



Generating a Pie Chart.



    plt.pie(math_array, labels = chart_labels, explode=chart_explode, autopct='%1.1f%%')
    plt.legend(title = "Predictions:")
    plt.show()

<figure>

<img decoding="async" style="width: 246px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest8.png" alt="" /> 

<figcaption>Predicted accuracy as a percentage of the Test 1</figcaption> </figure> 



### The prediction for each URL in Test 1



The results that the trained model returns as&#8217; 0&#8242; and&#8217; 1&#8242; are converted into human-readable labels.



    predictions = ['Negative' if pred == 0 else 'Positive' for pred in predictions]



The following loop iterates through predictions and prints out each prediction.



    for i, pred in enumerate(predictions):
        print(f"Prediction for data point {i+1}: {pred}")

<figure>

<img decoding="async" style="width: 474px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest9.jpg" alt="" /> 

<figcaption>Predictions for each data input in Test 1</figcaption> </figure> 



### Generated Phishing with Phishing URLs: Test 2



This test was conducted by mixing the generated Phishing URL with other verified Phishing URLs from the PhishTank dataset. It has significantly predicted that dataset by providing 100% accurate results.

<figure>

<img decoding="async" style="width: 247px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest10.png" alt="" /> 

<figcaption>Predicted accuracy as a percentage for Test 2</figcaption> </figure> 



### The prediction for each URL in Test 2

<figure>

<img decoding="async" style="width: 468px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest11.jpg" alt="" /> 

<figcaption>Predictions for each data input in Test 2</figcaption> </figure> 



### Generated Phishing with a mix of legitimate and Phishing URLs: Test 3

<figure>

<img decoding="async" style="width: 247px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest12.png" alt="" /> 

<figcaption>Predicted accuracy as a percentage for Test 3</figcaption> </figure> 



### The prediction for each URL in Test 3

<figure>

<img decoding="async" style="width: 485px; height: auto;" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest13.jpg" alt="" /> 

<figcaption>Predictions for each data input in Test 3</figcaption> </figure> 



## Conclusion:



The primitive methods used to identify Phishing websites seem outdated since most of the Features used to extract the characteristics of website links do not show a progressive benefit to the accuracy of the predictions. Apart from that, a dataset&#8217;s high number of features can also cause excessive time-consuming for detection. Also, the performance of some machine learning methods gets depressed if the dataset is noisy and large. Therefore, this research focused on making a justifiable machine learning operational program with explicit features that could produce a high prediction accuracy. The Phishing website detection features rely more on domain characteristics than the classic representation/optical features. After a few experiments with feature extraction, it reached 86% predicted accuracy only with eight features. The tests for Phishing also showed a precise outcome with the machine learning model discovered in this research.