# CMI-SleepState-Detection
## Child Mind Institute - Detect Sleep States
### Detect sleep onset and wake from wrist-worn accelerometer data
_______________________________________________________________________
# [Kaggle Competition](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/overview)
________________________________________________________________________
# Author Details:
### Name: Najeeb Haider Zaidi
### Email: zaidi.nh@gmail.com
### Profiles: [Github](https://github.com/snajeebz)  [LinkedIn](https://www.linkedin.com/in/najeebz) [Kaggle](https://www.kaggle.com/najeebz)
### License: Private, Unlicensed, All the files in this repository under any branch are Prohibited to be used commercially or for personally, communally or privately unless permitted by author in writing.
### Copyrights 2023-2024 (c) are reserved only by the author: Najeeb Haider Zaidi
________________________________________________________________________
# Attributions:
## The Dataset has been provided by Child Mind Institute. in [Kaggle Competition](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/overview) which the author is participating in and authorized to use the dataset solely for the competition purposes.
________________________________________________________________________
# Overview
This work will improve researchers' ability to analyze accelerometer data for sleep monitoring and enable them to conduct large-scale studies of sleep. Ultimately, the work of this competition could improve awareness and guidance surrounding the importance of sleep. The valuable insights into how environmental factors impact sleep, mood, and behavior can inform the development of personalized interventions and support systems tailored to the unique needs of each child.
________________________________________________________________________
# Description
## Goal of the Competition
The goal of this competition is to detect sleep onset and wake. We will develop a model trained on wrist-worn accelerometer data in order to determine a person's sleep state.

Our work could make it possible for researchers to conduct more reliable, larger-scale sleep studies across a range of populations and contexts. The results of such studies could provide even more information about sleep.

The successful outcome of this competition can also have significant implications for children and youth, especially those with mood and behavior difficulties. Sleep is crucial in regulating mood, emotions, and behavior in individuals of all ages, particularly children. By accurately detecting periods of sleep and wakefulness from wrist-worn accelerometer data, researchers can gain a deeper understanding of sleep patterns and better understand disturbances in children.

____________________________________________________________________
# Dataset:
Dataset provided comprises of two files, one includes 277 unique time series of multiple nights. This is actually the sesor reading(accelerometer) contains one column 'anglez' which is the angle of motion and another is Enmo which is eucleadian normalized distance between two readings. each recorded timestep is 5 seconds apart. Another file is the events csv which provides step numbers and timestamps of monitored data when the subject onset(go to sleep) and when the subject wakesup. There are some recorded steps in which the device was not worn so we need to delete those steps.
____________________________________________________________________
# Observations:

1. Series is a huge dataset with 127,946,340 rows and at times is difficult to perform operations like pandas.apply or training the model due to RAM (30GB) limitations and time constraints (12hour/execution).
2. Device is not worn includes the consecutive rows with zero enmo and anglez unchanged. There are 16,180,231 such rows.
3. During EDA it was observed that 30 mins before and after events (onset/wakeup), enmo, anglez varries quicker and more, and after that, majority of the times it is minor. So a window 60min before and 60 min after the event provides the reasonable and relevant dataset to perform training operations.

## Features Engineering:

1. Since the change in enmo and anglez leads to the event so all the features shall be relevant to the change in these two.
2. Feature 1,2: Rolling Standard Deviation (1 min window : 12 timesteps)
3. Feature 2,3: Rolling Mean(2 min window : 24 timesteps)
4. Clustering the enmo and anglez into 4 clusters.
5. Windows Creation to delete all rows apart of 1hr before and after the events.

_____________________________________________________________________
# Machine Learning:
1. Random Forest classifier is used to classify onset and wakeup states.
2. As per the requirement if onset stays for 30 mins the status is onset, between onset events; wakeup events less that 30mins will not change the state and considered as disturbances.
3. Sleep score is the mean classification score.

