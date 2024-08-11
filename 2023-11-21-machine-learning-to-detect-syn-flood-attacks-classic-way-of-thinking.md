---
title: 'SYN Flood Attacks: Classic Opinion'
author: Vishwa Vasu
type: post
date: 2023-11-21T10:14:09+00:00
url: /machine-learning-to-detect-syn-flood-attacks-classic-way-of-thinking/
featured_image: /wp-content/uploads/2023/11/syn-flood-high-resolution-logo-480x360.png
categories:
  - Machine Learning
tags:
  - AI
  - dos
  - machinelearning
  - ML
  - synflood

---
Well, this is a classic idea. Let&#8217;s see how we can use machine learning to detect SYN Flood attacks.

## Introduction of SYN Flood Attack: {.wp-block-heading.has-medium-font-size}

There should be a three-way handshake to establish a TCP connection.

<ol class="wp-block-list">
  <li>
    The client that needs to start a communication sends a TCP (synchronise) SYN packet to the destination.
  </li>
  <li>
    The server then sends a (synchronise-acknowledgement) SYN-ACK packet to the host.
  </li>
  <li>
    Finally, the client sends an (acknowledgement) ACK packet to the server to conclude<br />the three-way handshake.
  </li>
</ol><figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="391" height="382" src="https://vazdefense.com/wp-content/uploads/2023/11/tcp.png" alt="" class="wp-image-724" srcset="https://vazdefense.com/wp-content/uploads/2023/11/tcp.png 391w, https://vazdefense.com/wp-content/uploads/2023/11/tcp-300x293.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/tcp-200x195.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/tcp-30x30.png 30w" sizes="(max-width: 391px) 100vw, 391px" /> <figcaption class="wp-element-caption">TCP 3-Way Handshake</figcaption></figure> 

As mentioned earlier, there should be a three-way handshake to communicate TCP between two parties. A transmission control block (TCB) stores the connection information when the client sends a packet to the server. It keeps the half-open (second step of the three-way handshake) connection information. It ques the half-open connections until it receives the ACK packets from the client. If the client does not receive the ACK, the server resends the SYN-ACK packet to the client again. TCB records will be deleted once it gets the ACK from the client. This mechanism is used for the SYN-Flood attack.

SYN-Flood uses random IP addresses which do not exist on the Internet. These random  
IP addresses initiate half-opened connections with the server. However, the server will  
not receive the final ACK packet since the SYN-Flood attack does not finish the three-way  
handshake. TCB records will stay in the queue since it could not obtain the last acknowledgement packet to conclude the three-way handshake.<figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="471" height="351" src="https://vazdefense.com/wp-content/uploads/2023/11/sflood.png" alt="" class="wp-image-725" style="width:369px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/sflood.png 471w, https://vazdefense.com/wp-content/uploads/2023/11/sflood-300x224.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/sflood-200x149.png 200w" sizes="(max-width: 471px) 100vw, 471px" /> <figcaption class="wp-element-caption">TCP 3-Way Handshake</figcaption></figure> 

## Feature Extraction: {.wp-block-heading}

The SYN-Flood test was conducted in a lab environment. Datasets for the SYN-Flood have  
been generated to make a balanced dataset. A docker setup built with a custom setup and a customised lab environment has caused the SYN-Flood traffic. That traffic consists of telnet, SSH and web server traffic.

  
A &#8220;C&#8221; programme has been used to initiate SYN Flood traffic since the &#8220;C&#8221; language is  
faster than other computing languages. It continuously sends SYN packets where the victim OS cannot send Reset packets to the network at that speed.

  
The docker setup consists of 3 images: the Attacker, the Victim, and another image for  
testing the legitimate connectivity. When the attack is conducted, the SYN cookie countermeasure is turned off to make the attack work.

### Docker Setup: {.wp-block-heading}<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="511" height="263" src="https://vazdefense.com/wp-content/uploads/2023/11/docker.png" alt="" class="wp-image-726" srcset="https://vazdefense.com/wp-content/uploads/2023/11/docker.png 511w, https://vazdefense.com/wp-content/uploads/2023/11/docker-300x154.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/docker-200x103.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/docker-480x247.png 480w" sizes="(max-width: 511px) 100vw, 511px" /> <figcaption class="wp-element-caption">Lab Setup-1 for SYN Flood</figcaption></figure> 

Another lab setup has been used to create the attack beyond the docker setup to make it  
more realistic. It has an attacker machine, the victim machine, and another machine to test the legitimate connectivity as in the docker setup.

### Custom Lab Setup: {.wp-block-heading}<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="329" height="329" src="https://vazdefense.com/wp-content/uploads/2023/11/lab.png" alt="" class="wp-image-727" srcset="https://vazdefense.com/wp-content/uploads/2023/11/lab.png 329w, https://vazdefense.com/wp-content/uploads/2023/11/lab-300x300.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/lab-200x200.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/lab-30x30.png 30w" sizes="(max-width: 329px) 100vw, 329px" /> <figcaption class="wp-element-caption">Lab Setup-2 for SYN Flood</figcaption></figure> 

The flooding traffic has collected over 150,000 TCP Wireshark packet captures from the  
docker and the Lab setup. The regular traffic has been collected from two different machines and has over 150,000 TCP traffic. The duplicates have been removed from both datasets, and 150,000 from each dataset have been finalised for feature extraction.

## Coding: {.wp-block-heading.has-medium-font-size}

<pre class="wp-block-code"><code>import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

import os
import re

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

#XGBoost Classification model
from xgboost import XGBClassifier

#Package for store data
import pickle</code></pre>

Loading the test dataset.

<pre class="wp-block-code"><code>df = pd.read_csv('raw_synflooded_data.csv')</code></pre>

## Proposed feature extraction methods for SYN Flood: {.wp-block-heading}

Five features are considered to test the SYN-Flood attack for machine learning. The  
Wireshark packet captures can be saved as a CSV dataset. This dataset has information on ping status on destination IP addresses, packet length, protocol information, and packet status information.

<ul class="wp-block-list">
  <li>
    Ping responses in Destination IP addresses
  </li>
  <li>
    Protocol check
  </li>
  <li>
    Length check
  </li>
  <li>
    Packet information &#8211; Half-opened connections
  </li>
</ul>

There are two stages in feature extraction for SYN-Flood. In the first stage, it checks for  
the ping responses.

### Phase 1: {.wp-block-heading}

#### Ping responses in Destination IP addresses {.wp-block-heading}

This function checks for the ping responses in the destination addresses. The IP addresses  
that exploit the legitimate connection do not respond to ping since all IP addresses are not  
in use, which is used to create the half-opened connections. If IP does not reply or respond,  
this function returns as&#8221; 1&#8243;.

The results of the first stage of testing and other information in the CSV are used in the  
second stage of testing. This stage checks for repetitive events on every ten batches.

<pre class="wp-block-code"><code>def ping_check(Destination):
    response = os.system("ping -c 1 -w 1 -n 1 " + Destination)

    if response == 0:
        return 0
    else:
        return 1 </code></pre>

The feature mentioned above extraction function compiles and joins with the following columns.

<pre class="wp-block-code"><code>def featureExtraction():
    features = &#91;]
    features.append(Destination)
    features.append(ping_check(Destination))
    features.append(Protocol)
    features.append(Length)
    features.append(Info)

    return features</code></pre>

The following loop goes through each function and joins the results together.

<pre class="wp-block-code"><code>traffic_features = &#91;]
for i in range(0, len(df)):
    Source = df&#91;'Source']&#91;i]
    Destination = df&#91;'Destination']&#91;i]
    Protocol = df&#91;'Protocol']&#91;i]
    Length = df&#91;'Length']&#91;i]
    Info = df&#91;'Info']&#91;i]

    print(i)

    traffic_features.append(featureExtraction())</code></pre>

I am specifying the column names of the test dataset.

<pre class="wp-block-code"><code>feature_names = &#91;'Destination', 'Ping', 'Protocol', 'Length', 'Info' ]</code></pre>

This creates a DataFrame with the provided&#8217; traffic\_features&#8217; and assigns the column names specified in the&#8217; feature\_names.&#8217;

<pre class="wp-block-code"><code>df = pd.DataFrame(traffic_features, columns = feature_names)
</code></pre>

The newly created data frame is saved to a CSV.

<pre class="wp-block-code"><code>df.to_csv('flood_ping.csv', index=False)</code></pre>

The feature extracted testing data loaded into a new DataFrame for PHASE 2.

<pre class="wp-block-code"><code>df = pd.read_csv('flood_ping.csv')</code></pre>

### Phase 2: {.wp-block-heading}

#### Same Ping responses for Destination IP addresses {.wp-block-heading}

This function checks for the responses of the ping. If the response average equals or exceeds 0.5 in each following ten records by ten records, it returns&#8221; 1&#8243;.

<pre class="wp-block-code"><code>#According to the results given by the ’ping_check’ function, this #function creates a list from it and converts it to an array.
#Then it checks for the mean value of each batches.

def ping_avg():
    ping = batch&#91;'Ping'].to_list()
    ping_list = np.array(ping)
    ping_mean = ping_list.mean()
    
    
    if ping_mean &gt;= 0.5:
        return 1
    else:
        return 0</code></pre>

#### Protocol check {.wp-block-heading}

This function checks for the protocol. If all the protocol label is identical for each following  
ten records by ten records, it returns&#8221; 1&#8243;.

<pre class="wp-block-code"><code>#This function checks the Protocol column to find the identical #information. It works by the loop specified at the end and 
checks for #every 10 batch inputs until the end of the dataset. If every values #are identical, it returns the number 1 for the batch #input.

def protocol_check():
     
    proto_info = batch&#91;'Protocol'].nunique() == 1
    if proto_info == True:
        return 1
    elif proto_info == False:
        return 0</code></pre>

#### Length check {.wp-block-heading}

This function checks for the size of the length of a packet. An SYN-flooded traffic usually has the same length, and some packets have different values. It relies upon the filter  
in the Wireshark analysis. The SYN request from the outside packet has an extra length  
than the outgoing&#8221; SYN, ACK&#8221; packet has a different length. Like other functions, this checks  
for the packet&#8217;s length analyses the following ten records by ten records, checks that the set has one unique value or two values and returns &#8220;1&#8221; if all the values are the same.

<pre class="wp-block-code"><code>#This function converts all the length information to a list and makes #it an array of 10 values for each. 
#Then check the length of the array, whether it is equal to or less #than ’2’.

def len_check():
    
    length_info = batch&#91;'Length'].to_list()
    leninfo_array = np.array(length_info)
    len_array = len(np.unique(leninfo_array))
    
    if len_array &lt;= 2:
        return 1
    else:
        return 0</code></pre>

#### Half-opened connections {.wp-block-heading}

This function checks for the packet information regarding the half-opened connections. This is also like the other functions. It contains the following ten records by ten records and returns &#8220;1&#8221; if all the records are the same in ten records.

<pre class="wp-block-code"><code>#This function checks the Info column and analysis it with regex #pattern to find the mentioned patterns. 
#This creates 10 batch inputs until the end of the dataset. It returns #output according to the findings.

def syn_check(Info):
    regex_pattern = r'\&#91;(SYN, ACK|TCP Retransmission|SYN)\]'

    match1 = re.search(regex_pattern, Info)
    match2 = re.search(regex_pattern, Info)
    match3 = re.search(regex_pattern, Info)

    if match1 or match2 or match3:
        return 1
    else:
        return 0</code></pre>

All the features mentioned in phase 2 execute, compile and join the results by this function.

<pre class="wp-block-code"><code>def featureExtraction2():
    features2 = &#91;]
    features2.append(ping_avg())
    features2.append(protocol_check())
    features2.append(len_check())
    features2.append(syn_check(Info))
    features2.append(Label)
    
    return features2</code></pre>

This research labels the regular traffic as&#8217; 0&#8242; and SYN Flood traffic as&#8217; 1&#8242;. This loop goes through each data and compiles the functions mentioned above. Finally, join all extracting features results.

<pre class="wp-block-code"><code>flood_features = &#91;]
#Label '1' if SYN Flood
Label = 0
for i in range(0, len(df),10):
    batch = df.iloc&#91;i:i+10]
    Info = df&#91;'Info']&#91;i]
    print(i)

    flood_features.append(featureExtraction2())</code></pre>

I am specifying the column names of the test dataset.

<pre class="wp-block-code"><code>feature_names = &#91;'Ping_avg', 'Protocol_check', 'Len_check', 'SYN_check', 'Label']</code></pre>

This creates a data frame with the provided&#8217; flood\_features&#8217; and assigns the column names specified in the&#8217; feature\_names.&#8217;

<pre class="wp-block-code"><code>df_test = pd.DataFrame(flood_features, columns = feature_names)
</code></pre>

The newly created data frame is saved to a CSV file.

<pre class="wp-block-code"><code>df_test.to_csv('flooded_labeled.csv', index=False)</code></pre>

## The final feature extracted dataset for SYN Flood detection: {.wp-block-heading.has-medium-font-size}

<pre class="wp-block-code"><code>data.head()</code></pre><figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="515" height="304" src="https://vazdefense.com/wp-content/uploads/2023/11/fextsynflood.png" alt="" class="wp-image-732" style="width:472px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/fextsynflood.png 515w, https://vazdefense.com/wp-content/uploads/2023/11/fextsynflood-300x177.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/fextsynflood-200x118.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/fextsynflood-480x283.png 480w" sizes="(max-width: 515px) 100vw, 515px" /> <figcaption class="wp-element-caption">Last Feature Extracted Dataset for SYN Flood</figcaption></figure> 

### Assumptions in SYN Flood Data Classification {.wp-block-heading}

The SYN Flood attack was performed by turning off the SYN Cookies countermeasure.

### Statistical and Visual Analysis: {.wp-block-heading.has-small-font-size}

<pre class="wp-block-code"><code>data.hist(bins = 50, color = 'Blue', lw=10, figsize = (15,15))
plt.show()</code></pre><figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="587" height="581" src="https://vazdefense.com/wp-content/uploads/2023/11/syngrstat.png" alt="" class="wp-image-733" style="width:471px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/syngrstat.png 587w, https://vazdefense.com/wp-content/uploads/2023/11/syngrstat-300x297.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/syngrstat-200x198.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/syngrstat-30x30.png 30w, https://vazdefense.com/wp-content/uploads/2023/11/syngrstat-480x475.png 480w" sizes="(max-width: 587px) 100vw, 587px" /> <figcaption class="wp-element-caption">Visualisation of data circulation in SYN Flood Dataset</figcaption></figure> 

The following figure shows how the feature extracted dataset has distributed its features in  
statistical form. According to that data, the SPF availability and count of the subdomains  
show a nearly balanced feature.

<pre class="wp-block-code"><code>data.describe()</code></pre>

The previously feature-extracted dataset for SYN Flood attack detection will be used here for this section&#8217;s accuracy analysis. Preceding that a statistical and graphical analysis demonstrates the constructed dataset similar to the Phishing dataset to assess how binary classification is distributed through the dataset and how it impacts the accuracy of the results. The statistical distribution of features for SYN Flood is shown in the following figure. Analysing the mean value of almost all features shows that each has a partly distributed form.<figure class="wp-block-image size-large is-resized">

<img loading="lazy" decoding="async" width="1024" height="449" src="https://vazdefense.com/wp-content/uploads/2023/11/synstat-1024x449.jpg" alt="" class="wp-image-734" style="width:512px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/synstat-1024x449.jpg 1024w, https://vazdefense.com/wp-content/uploads/2023/11/synstat-300x132.jpg 300w, https://vazdefense.com/wp-content/uploads/2023/11/synstat-200x88.jpg 200w, https://vazdefense.com/wp-content/uploads/2023/11/synstat-768x337.jpg 768w, https://vazdefense.com/wp-content/uploads/2023/11/synstat-480x210.jpg 480w, https://vazdefense.com/wp-content/uploads/2023/11/synstat.jpg 1097w" sizes="(max-width: 1024px) 100vw, 1024px" /> <figcaption class="wp-element-caption">Mathematical description/statistic of the SYN Flood dataset</figcaption></figure> 

<pre class="wp-block-code"><code>correlation_matrix_sns = data.corr()</code></pre>

I created the Seaborn Heatmap and defined the feature relations&#8217; chart size, visualisation colours, width, and roundup values.

<pre class="wp-block-code"><code>plt.figure(figsize=(10,8))
sns.heatmap(correlation_matrix_sns, annot=True, cmap='Blues', fmt='.2f', linewidths=0.5)
plt.title('Correlation Heatmap')
plt.show()</code></pre><figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="634" height="566" src="https://vazdefense.com/wp-content/uploads/2023/11/hmsyn.png" alt="" class="wp-image-735" style="width:488px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/hmsyn.png 634w, https://vazdefense.com/wp-content/uploads/2023/11/hmsyn-300x268.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/hmsyn-200x179.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/hmsyn-480x429.png 480w" sizes="(max-width: 634px) 100vw, 634px" /> <figcaption class="wp-element-caption">Correlation HeatMap of SYN Flood Dataset</figcaption></figure> 

I am defining&#8217; X&#8217; and&#8217; y&#8217;. Extract the&#8217; Label&#8217; column and store it in the variable&#8217; y&#8217;. Drop the&#8217; Label&#8217; column and keep the data frame variable&#8217; X&#8217;.

<pre class="wp-block-code"><code>y = data&#91;'Label']
X = data.drop('Label',axis=1)
X.shape, y.shape</code></pre>

I am separating the labelled dataset into train and test sets: 80-20 split ratio and getting the shape of training and test feature arrays. X\_train : (80% ratio, eight features), X\_test (20% ratio, eight features)importing the required packages.

<pre class="wp-block-code"><code>X_train, X_test, y_train, y_test = train_test_split(X, y,test_size = 0.2, random_state = 12)
X_train.shape, X_test.shape</code></pre>

I am creating holders to store the model performance results and make a function to call for storing the results of classification report data.

<pre class="wp-block-code"><code>ML_Model = &#91;]
acc = &#91;]
prec = &#91;]
rec = &#91;]
f1 = &#91;]

def storeResults(model, a,b,c,d):
    ML_Model.append(model)
    acc.append(a)
    prec.append(b)
    rec.append(c)
    f1.append(d)</code></pre>

### Machine Learning: {.wp-block-heading.has-medium-font-size}

In the research, I used seven different machine-learning algorithms. But in this blog, I will use only one machine learning algorithm for the demonstration for simplification purposes. 

_XGBoost  
Random Forest  
Decision Tree  
MLP  
KNN  
Naïve Bayes  
SVM_

#### XGBoost ML Model {.wp-block-heading.has-medium-font-size}

Instantiate and train the model.

<pre class="wp-block-code"><code>xgb = XGBClassifier(learning_rate=0.4,max_depth=7)
xgb.fit(X_train, y_train)</code></pre>

I am predicting the target value from the model for the test.

<pre class="wp-block-code"><code>y_test_xgb = xgb.predict(X_test)</code></pre>

Create a confusion matrix for the XGBoost Model and name the value labels.

<pre class="wp-block-code"><code>cm_xgb = confusion_matrix(y_test, y_test_xgb)
cm_xgb = pd.DataFrame(cm_xgb, index=&#91;'Actual Negatives', 'Actual Positives'], columns=&#91;'Predicted Negative', 'Predicted Positive'])</code></pre>

I am generating the classification report and naming the target names.

<pre class="wp-block-code"><code>target_names = &#91;'Legitimate', 'Phishing']

cl_report = classification_report(y_test, y_test_xgb, target_names = target_names)
</code></pre>

Plot the confusion matrices and define the attributes of the figure.

<pre class="wp-block-code"><code>plt.figure(figsize=(12,6))
plt.subplot(1,2,1)
sns.heatmap(cm_xgb, annot=True, fmt='d', cmap='Blues')
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('XGBoost Confusion Matrix')

plt.tight_layout()
plt.show()</code></pre>

The XGBoost machine learning algorithm showed the best accuracy. Unlike Phishing, the SYN Flood has zero False Positives and False Negatives. The testing data is only divided between True Positives and True Negatives.<figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="467" height="456" src="https://vazdefense.com/wp-content/uploads/2023/11/xgbsyn.png" alt="" class="wp-image-736" style="width:412px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/xgbsyn.png 467w, https://vazdefense.com/wp-content/uploads/2023/11/xgbsyn-300x293.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/xgbsyn-200x195.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/xgbsyn-30x30.png 30w" sizes="(max-width: 467px) 100vw, 467px" /> <figcaption class="wp-element-caption">Highest accuracy given model for SYN Flood Detection</figcaption></figure> 

Extracting classification report data for evaluation.

<pre class="wp-block-code"><code>rs = recall_score(y_test,y_test_xgb)*100
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
fs = np.float64(fs)</code></pre>

I am storing the results for evaluation.

<pre class="wp-block-code"><code>storeResults('XGBoost', rs,ps,asc,fs)</code></pre>

<mark style="background-color:rgba(0, 0, 0, 0)" class="has-inline-color has-accent-color">Other ML algorithms have not been mentioned here.</mark>

## Summarising the accuracies {.wp-block-heading.has-medium-font-size}

<pre class="wp-block-code"><code>results = pd.DataFrame({ 'ML Model': ML_Model,'Accuracy %': acc, 'Precision %' : prec, 'Recall %' : rec, 'F1 Score %' : f1})
results</code></pre>

Sorting the data frame by the accuracy.

<pre class="wp-block-code"><code>results.sort_values(by=&#91;'Accuracy %', 'Precision %'], ascending=False)</code></pre>

As assured, the SYN Flood test has given an exceptionally outstanding result for machine  
learning accuracy. All seven machine learning models have given almost or indeed 100%  
accuracy and precision.<figure class="wp-block-image size-large is-resized">

<img loading="lazy" decoding="async" width="1024" height="454" src="https://vazdefense.com/wp-content/uploads/2023/11/synacc-1024x454.jpg" alt="" class="wp-image-737" style="width:497px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/synacc-1024x454.jpg 1024w, https://vazdefense.com/wp-content/uploads/2023/11/synacc-300x133.jpg 300w, https://vazdefense.com/wp-content/uploads/2023/11/synacc-200x89.jpg 200w, https://vazdefense.com/wp-content/uploads/2023/11/synacc-768x341.jpg 768w, https://vazdefense.com/wp-content/uploads/2023/11/synacc-480x213.jpg 480w, https://vazdefense.com/wp-content/uploads/2023/11/synacc.jpg 1228w" sizes="(max-width: 1024px) 100vw, 1024px" /> <figcaption class="wp-element-caption">Summary of ML Performance for SYN Flood</figcaption></figure> 

### ROC Analysis {.wp-block-heading.has-medium-font-size}

The ROC curve is a figure that shows the sensitivity on the y-axis as the True Positive.  
Rate against the specificity on the x-axis as the False Positive Rate. The 45-degree diagonal line corresponds to the random chance. The AUC(Area Under the Curve) represent all the ML models used in this research. 

All the ML models show an ideal ROC curve for the SYN Flood. It means there is a 100%  
chance that the ML models distinguish the positive and negative classes.

<pre class="wp-block-code"><code>#Defying the figure size
plt.figure(figsize=(8,6))
#define metrics
#Predict probabilities for each ml model
y_pred_proba_dt = tree.predict_proba(X_test)&#91;::,1]
y_pred_proba_mlp = mlp.predict_proba(X_test)&#91;::,1]
y_pred_proba_xgb = xgb.predict_proba(X_test)&#91;::,1]
y_pred_proba_knn = knn.predict_proba(X_test)&#91;::,1]
#y_pred_proba_svm = svm.predict_proba(X_test)&#91;::,1]
y_pred_proba_forest = forest.predict_proba(X_test)&#91;::,1]
y_pred_proba_nb = nb.predict_proba(X_test)&#91;::,1]

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

plt.plot(&#91;0,1],&#91;0,1],color='gray', linestyle='--', label="Reference Line")


plt.title('ROC Analysis')
plt.ylabel('True Positive Rate')
plt.xlabel('False Positive Rate')
plt.legend(loc='lower right')
plt.show()</code></pre><figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="494" height="392" src="https://vazdefense.com/wp-content/uploads/2023/11/aucrocsyn.png" alt="" class="wp-image-738" srcset="https://vazdefense.com/wp-content/uploads/2023/11/aucrocsyn.png 494w, https://vazdefense.com/wp-content/uploads/2023/11/aucrocsyn-300x238.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/aucrocsyn-200x159.png 200w, https://vazdefense.com/wp-content/uploads/2023/11/aucrocsyn-480x381.png 480w" sizes="(max-width: 494px) 100vw, 494px" /> <figcaption class="wp-element-caption">AUC-ROC analysis for SYN Flood</figcaption></figure> 

The SYN Flood dataset has given all the machine learning models top-notch accuracy.

## Saving the best model for future work {.wp-block-heading.has-medium-font-size}

With the help of the pickle package, the best model will be serialised and saved as a binary format.

<pre class="wp-block-code"><code>pickle.dump(xgb, open("xgb2.pickle.dat", "wb"))</code></pre>

The serialised data is deserialised and loaded into the memory.

<pre class="wp-block-code"><code>loaded_model = pickle.load(open("xgb2.pickle.dat", "rb"))
loaded_model</code></pre>

## Testing: {.wp-block-heading.has-medium-font-size}

The ML model saved earlier will be used for the predictions for testing data.

<pre class="wp-block-code"><code>model = loaded_model</code></pre>

The feature extracted testing data loaded into a new DataFrame for testing.

<pre class="wp-block-code"><code>test_data = pd.read_csv('mix_new_ext.csv')</code></pre>

This removes the Label column from the original dataset and loads it into a new variable. The original remains unchanged with&#8217; test_data.&#8217;

<pre class="wp-block-code"><code>test_pred = test_data.drop('Label', axis=1)</code></pre>

The trained machine learning model is used for the predictions for testing data.

<pre class="wp-block-code"><code>predictions = model.predict(test_pred)</code></pre>

Make a Numpy array from predictions.

<pre class="wp-block-code"><code>prd = predictions
pred_array = np.array(&#91;prd])</code></pre>

Get the count of negatives(0) and positives(1) from the Numpy array.

<pre class="wp-block-code"><code>negative = np.count_nonzero(pred_array == 0)
positive = np.count_nonzero(pred_array == 1)
math_array = (&#91;negative, positive])</code></pre>

Naming the labels of the Pie Chart for Phishing

<pre class="wp-block-code"><code>chart_labels = &#91;'Normal', 'SYN_Flood']
chart_explode = &#91;0.2, 0]</code></pre>

Since the machine learning algorithms have given a significant accuracy for the SYN Flood  
attack, the new data evaluation should meet the expected decisive outcome. The traffic for tests is also generated using the lab setup and regular traffic via Wireshark captures. The collected CSVs have run through the feature extraction methods used by the SYN Flood feature extraction.

The first feature extraction is performed to identify the ping responses. The second feature  
extraction was executed with those results to find the mean of the Ping responses, protocol,  
Length and Half-opened connection. The mean value was identified for each of the ten sequence values. Then, the final CSVs were tested with the machine-learning model with the highest predicted score.

### Traffic identified as SYN Flood from the Internet: [Mazebolt][1] {.wp-block-heading}

Traffic identified as a SYN Flood attack commenced on the Internet has been executed  
through the feature extraction and the machine learning model. The constructed machine  
learning algorithm has identified that traffic is a 100% SYN Flood attack by the prediction.

Generating a Pie Chart.

<pre class="wp-block-code"><code>plt.pie(math_array, labels = chart_labels, explode=chart_explode, autopct='%1.1f%%')
plt.legend(title = "Predictions:")
plt.show()</code></pre><figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="422" height="332" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest28.png" alt="" class="wp-image-739" style="width:293px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/ptest28.png 422w, https://vazdefense.com/wp-content/uploads/2023/11/ptest28-300x236.png 300w, https://vazdefense.com/wp-content/uploads/2023/11/ptest28-200x157.png 200w" sizes="(max-width: 422px) 100vw, 422px" /> <figcaption class="wp-element-caption">Predicted accuracy as a percentage</figcaption></figure> 

#### The prediction for each URL in Test 1 {.wp-block-heading}

The results that the trained model returns as&#8217; 0&#8242; and&#8217; 1&#8242; are converted into human-readable labels.

<pre class="wp-block-code"><code>predictions = &#91;'Negative' if pred == 0 else 'Positive' for pred in predictions]</code></pre>

The following loop iterates through predictions and prints out each prediction.

<pre class="wp-block-code"><code>for i, pred in enumerate(predictions):
    print(f"Prediction for data point {i+1}: {pred}")</code></pre><figure class="wp-block-image size-full is-resized">

<img loading="lazy" decoding="async" width="926" height="609" src="https://vazdefense.com/wp-content/uploads/2023/11/ptest29.jpg" alt="" class="wp-image-740" style="width:417px;height:auto" srcset="https://vazdefense.com/wp-content/uploads/2023/11/ptest29.jpg 926w, https://vazdefense.com/wp-content/uploads/2023/11/ptest29-300x197.jpg 300w, https://vazdefense.com/wp-content/uploads/2023/11/ptest29-200x132.jpg 200w, https://vazdefense.com/wp-content/uploads/2023/11/ptest29-768x505.jpg 768w, https://vazdefense.com/wp-content/uploads/2023/11/ptest29-480x316.jpg 480w" sizes="(max-width: 926px) 100vw, 926px" /> <figcaption class="wp-element-caption">Predictions for each data input</figcaption></figure> 

## Conclusion: {.wp-block-heading.has-medium-font-size}

Since the SYN Flood traffic has repetitive occurrences, feature extraction was the best  
interpretation to make a dynamic dataset. The invented dataset has given 100% precision.  
For detecting SYN Flood attacks. The dataset has been primarily generated from the minor possible features that could be extracted to detect and characterise the dataset. It has used five features to make the dataset. Therefore, the efficiency of the application is excessive when triggering a SYN Flood attack from network traffic.

 [1]: https: //kb.mazebolt.com/knowledgebase/syn-flood/