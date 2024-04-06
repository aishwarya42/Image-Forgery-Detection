# Image Forgery Detection
Digital images play important roles in many fields such as medical, journalism,
scientific publication, digital forensic etc [15]. An image can be manipulated easily by
the means of an image editing tool such as Photoshop. Tampering of images is done
often executed with the aim of concealing significant or relevant characteristics, to
create fallacious or forged images. The goal is to affect the semantic meaning of the
image to trick the viewers by changing some major areas of image.
Incredible misrepresentations are so deceptive that the human eye would not see
anything and there are no proofs of forgery to old and trusted image tamper detection
procedures. Hence authenticity is also lost. Integrity and authenticity verification of
digital images are one of the latest research topics in the sector of image processing.
##  Problem Statement
Impeccable deceptions are so manipulative that they're not readily visible and
therefore do not report any evidence of fraud to outdated protocols. Machine
learning-based tools are used to cope with this challenge of image forgery to
immediately draw a distinction between pictures that are actual and distorted. Several
approaches of tracking image forgery have been explored to locate altered sectors in
images.
## Objective
Our aim is to produce a system that can tell whether copy-move image forgery
technique has been used to play with an image that has been provided to us as input.
The process below for detecting copy-move forgery in input images makes use of the
Scale Invariant Feature Transformation (SIFT) algorithm. This algorithm has
proven to be successful in extracting rich features from an image to tell when some
region of that image is copy and moved.
## Methodology
### INPUT IMAGE PROCESSING
Procedure begins by taking an image as input and converting it into a numpy array for
easy representation and manipulation. Numpy is a python library that provides
excellent support for all array-based operations. OpenCV provides a method for
converting a given image into a numpy array representation.
```
image = cv2.imread(image_path)
The input image in numpy array representation is also converted to gray tone.
gr_img = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
### FEATURE EXTRACTION
Feature extraction is done to reduce an initial set of raw data i.e. input image in our
case, to a more manageable form for easy processing. This is performed with the help
of the SIFT algorithm. This algorithm is proprietary, which ensures that it is used in
the OpenCV non-free module.
```
st = cv2.SIFT_create()
keypoints, descriptors = st.detectAndCompute(gr_img,
None)
```
Here,
keypoints : list of keypoints (length = n), and
descriptors : numpy array of shape n×128.
### FEATURE MATCHING
This is achieved with the aid of Brute-Force Matcher, which uses some distance
estimation to take the descriptor of one function in the first set and matches it with all
the other functions in the second set [20]. All this is done to return the nearest match.
Since here we are trying to find regions of an image that have been copy-pasted to
some other area in the same image, the keypoint descriptors obtained in the previous
step will be passed as parameters in this step.
```
matches =
cv2.BFMatcher(cv2.NORM_L2).knnMatch(descriptors,
descriptors, k = 10)
```
Here,
cv2.BFMatcher : Brute-Force Matcher object
cv2.NORM_L2 : specifies the distance measurement type, is also the default
 value
21
knnMatch() : method used to obtain k best matches, takes descriptors and k
 value as parameters
At the end, an image’s authenticity is established when no matches are found. Presence of
matches acts as a proof that copy-move forgery has been predicted.
# Result 
To trace copy-move counterfeit in an image, we have presented a GUI based solution. The
GUI has simple functionalities of selecting an image from the desired folder and scanning it
to locate copy-move fraud.
The application allows users to pick images in JPEG and PNG format. It can further be
extended to BITMAP format as well.
![](https://github.com/aishwarya42/Image-Forgery-Detection/blob/main/result/result_tkinter.png)
## Unit Testing
For efficient performance evaluation of our application, we will be calculating the True Positive Rate, False Positive Rate, Accuracy and Precision of our program.
The genuine images and images forged by the copy-move method present in CASIA 1 dataset used to perform this testing were 800 and 480, respectively. The program generates a text file with the values obtained for True Positive Rate, False Positive Rate, Accuracy and Precision.

#### Formulas used in the calculation of above values:
##### Accuracy = (TP + TN) / (TP + TN + FP + FN)
##### True-positive rate = TP / (TP + FN)
##### False-positive rate = FP / (FP + TN)
##### Precision = TP / (TP + FP)
In these formulas,
##### TP: True positive- 
a "true positive" is the event that the test makes a positive prediction, and the subject has a positive result under the gold standard [21].
##### TN: True negative- 
a "true negative" is the event that the test makes a negative prediction, and the subject has a negative result under the gold standard [21].
##### FN: False negative-
a "false negative" is the event that the test makes a negative prediction, and the subject has a positive result under the gold standard [21].
##### FP: False positive-
a "false positive" is the event that the test makes a positive prediction, and the subject has a negative result under the gold standard.
##### Accuracy: 
Accuracy is a widely used metric for measuring the performance of learning systems [22].
##### Precision: 
In pattern recognition, information retrieval and classification (machine learning), precision (also called positive predictive value) is the fraction of relevant instances among the retrieved instances.
##### True positive rate (TPR): 
It is the proportion of positive instances (ie, feature vectors of malicious applications) classified correctly [22].
##### False positive rate (FPR): 
It is the proportion of negative instances (ie, feature vectors of benign applications) classified incorrectly [22].

