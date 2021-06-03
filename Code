import cv2     # open cv library
import os      # used for fetching contents from a directory
import matplotlib.pyplot as plt      #  used for plotting 2D arrays
import time    # used for create time delay in an opertaion
import numpy as np  # used for working with arrays
from receiveResponses import *  # we need a list  from receiveResponses file so we imported it 

# creating a list to store images in it
frames = []    
frames.append(cv2.imread('Direction1.jpg'))
frames.append(cv2.imread('Direction2.jpg'))
frames.append(cv2.imread('Direction3.jpg'))
frames.append(cv2.imread('Direction4.jpg'))

# It contains all the configuration related to MobileNet-SSD with COCO DataSet
config = "ssd_mobilenet_v3_large_coco_2020_01_14.pbtxt" 
# we will frozen all the variables to constants
frozen_model = "frozen_inference_graph.pb"


# pre-labeled data is fed into model training in DNN 
model = cv2.dnn_DetectionModel(frozen_model,config)

#MobileNet configuration it is mentioned as input size of image should be as (320,320) 
model.setInputSize(320,320)
model.setInputScale(1.0/127.5)
# setting the input mean as the MobileNet takes input from [-1,1] 
model.setInputMean((127.5,127.5,127.5))
# the MobileNet configuration changes the BGR (gray image) to RGB automaticcally
model.setInputSwapRB(True)


# empty list to store the count of vehicles in each path
count = []


for frame in range(len(frames)):
    # we can change our accurracy using confThreshold
    ClassIndex, confidece ,bbox = model.detect(frames[frame],confThreshold=0.3)
    # the no of vehicles in an image are appending into count list
    count.append(len(ClassIndex))
for i in range(len(l)):
    if l[i] == 1:
        count[i] = 100000
# empty dictionary to store both count of vehicles and their indexs
dict1 = {}
for i in range(len(count)):
    dict1[count[i]] = i;


# sorting the keys in the dictionary and assigning them to count list
count = sorted(dict1.keys())
# reversing the count list
count = count[::-1]

for i in range(len(count)):
    traffic_lights = ["Red","Red","Red","Red"]
    g = dict1.get(count[i])
    print("For turn:",i+1, "path:",g+1,"is allowed")
    traffic_lights[g] = "Yellow"
    print(traffic_lights)
    time.sleep(2)
    traffic_lights[g] = "Green"
    print(traffic_lights)
    # to create time delay of 3 seconds
    time.sleep(3)
    print()
