# Classifier-to-detector

# Image Classification vs. Object detection

* IMage Classification:
    * One Image in
    * One class Label out

* Object Detection on the other hand, not only tells us what is in the image(i.e., Class Label) but also where in the image the object is.. via bounding box(x,y).
    * Input one image
    * Obtain multiple bounding boxes and class labels as output.
    
 
* Any object detection alg(regardless of traditional computer vision or state-of-the-art Deep learning), follows the same pattern.
    * **Input**: An image.
    * **Output**: Three values including:
        * 1: A **list of bounding boxes**, or the x,y coordinates of each object in the image.
        * 2: The **Class Label** associated with each of the boundimg boxes.
        * 3: The **probability/confidence score** associated with each bounding box and class label. 
        

# Converting an CNN Image Classifier into an object detectot.

* We'll be borrowing elements from HOG + Linear SVM to convert any deep Learning etwork image classifier into an Object Detector.

    * The first ingredient from HOG + Linear SVM is to use image pyramids.
        * Utilizing an image pyramid allows us to find objects in images at different scales of an image.
    
    * The second ingredient is sliding windows.
        * As the name suggests, a sliding window is a fixed-size rectangle tht slides from left-to-right and top-to-bottom within an image.
        * At each stop of window we would:
            * 1: Extract the ROI
            * 2: Pass it through our classifier
            * 3: Obtain the output predictions.
    
    * combined with image pyramids, sliding windows allow us to localize objects at different locations and multiple scales of the input image.


    * The final key ingredient is Non- max Suppression(NMS).
        * we will use NMS to suppress weak, overlapping bounding boxes in favour of higher confidence predictions.


 
 # Algorithm:

* 1: Input an image.

* 2: Construct an image pyramid.

* 3: For each scale of the image pyramid, run a sliding window.
    * 3a: For each step of sliding window, extract ROI.
    * 3b: Take the ROI and pass it through our CNN originally trained for image classification.
    * 3c: Examine the probability of the top class label of the CNN and if meets the minimum confidence, record (1) the class label and (2) the location of the sliding window.

* 4: Apply class-wise non-maxima suppression to the bounding boxes.

* 5: Return results to calling function.

 
