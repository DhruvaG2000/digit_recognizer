# digit_recognizer

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Tech Stack](#tech-stack)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
* [Usage](#usage)
* [Results and Demo](#results-and-demo)
* [Future Work](#future-work)
* [Troubleshooting](#troubleshooting)
* [Acknowledgements and Resources](#acknowledgements-and-resources)



<!-- ABOUT THE PROJECT -->
## About The Project
This project aims to identify handwritten numbers using computer vision.  


### Tech Stack
This section should list the technologies you used for this project. Leave any add-ons/plugins for the prerequisite section. Here are a few examples.
* [tensorflow](https://www.tensorflow.org/)
* [OpenCV](https://opencv.org/)
* [mnist dataset](http://yann.lecun.com/exdb/mnist/)  


<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

* Install these particular python packages using pip install (or pip3 if python2 is your default)
```sh
pip install image==1.5.20
pip install numpy==1.14.3
pip install tensorflow==1.4.0
```

### Installation
1. Clone the repo
```sh
git clone https://github.com/DhruvaG2000/digit_recognizer
```


<!-- USAGE EXAMPLES -->
## Usage
Refer [notebook](https://github.com/DhruvaG2000/digit_recognizer/blob/master/train_and_detect_digits.ipynb) 


<!-- RESULTS AND DEMO -->
## Results and Demo
After training you can load your own images as follows:
```
img = cv2.imread('6.jpeg', 1)
plt.imshow(img) 

#-----Converting image to LAB Color model----------------------------------- 
lab= cv2.cvtColor(img, cv2.COLOR_BGR2LAB)
plt.imshow(lab)

#-----Splitting the LAB image to different channels-------------------------
l, a, b = cv2.split(lab)
plt.imshow( l)
plt.imshow( a)
plt.imshow( b)

#-----Applying CLAHE to L-channel-------------------------------------------
clahe = cv2.createCLAHE(clipLimit=5.0, tileGridSize=(8,8))
cl = clahe.apply(l)
plt.imshow(cl)

#-----Merge the CLAHE enhanced L-channel with the a and b channel-----------
limg = cv2.merge((cl,a,b))
plt.imshow( limg)

#-----Converting image from LAB Color model to RGB model--------------------
final = cv2.cvtColor(limg, cv2.COLOR_LAB2BGR)
plt.imshow( final)
cv_img = cv2.resize(final,(28,28))
cv2.imwrite("final.png",cv_img)
```
Once the image has been processed, you can apply your detections by:
```
img = np.invert(Image.open("final.png").convert('L')).ravel()

prediction = sess.run(tf.argmax(output_layer, 1), feed_dict={X: [img]})
print ("Prediction for test image:", np.squeeze(prediction))
```

<!-- FUTURE WORK -->
## Future Work
- [x] Task 1: Basic one digit number recognition
- [ ] Task 2: multiple digit number recognition 
- [ ] Task 3: detect numbers with bounding boxes
- [ ] Task 4: apply mathematical operations to the detected numbers


<!-- TROUBLESHOOTING -->
## Troubleshooting
* It is possible that your trained model will incorrectly recognize the digits. Inorder to combat this try tweaking with the contrast, brightness and the size of your digit in the frame.



<!-- ACKNOWLEDGEMENTS AND REFERENCES -->
## Acknowledgements and Resources
* [digital ocean](https://www.digitalocean.com/community/tutorials/how-to-build-a-neural-network-to-recognize-handwritten-digits-with-tensorflow)   
...


