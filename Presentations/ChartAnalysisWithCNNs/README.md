# Object Detection with CNNs -- and automatic chart analysis 

The inital goal of the presentation was to introduce a pair of research topics: object detection and automatic chart analysis; the subsequent objective was the exploration of the influence of the latter in the former. In this context, the [slides](./rcnn.pdf) contain a historical summary and the current state-of-the-art for addressing the detection of objects in images; correlatively, an implementation with PyTorch is available in the [Jupyter Notebook](./RCNN.ipynb). 

However, the slides are possibly overfilled with quotes and references; then, we aim, with this README.md, to provide a more appropriate description of each paper, explicitly writing their objectives and how they influenced the current shape of this awesome branch of science! For this, we will sort the documents according to the date of publication. 

+ [Efficient graph-based image segmentation](https://link.springer.com/article/10.1023/B:VISI.0000022288.19776.77) (2004). There isn't a panacea to science, nor to anything; in particular, algorithms to segment images (that is, to partition the image, which is a set of pixels, attributing to each pixel a label according to a set of predefined labels) existed way before way before deep learning, and they were pretty okay. In this paper, for instance, Felzenszwalb and Huttenlocher propose an graph-based procedure that (1) instantiates a weighed graph in which the vertices are the pixels (the weights are a measure of dissimilarity between the pixels) and (2) searchs for connected components whose internal similarity is substantially discrepant from the external dissimlarity; those connected components compose the segmentation. 

+ [Imagenet classification with deep convolutional neural networks](https://papers.nips.cc/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html) (2012). This is THE paper for image classification with CNNs; historically, it presented to the world the strength of deep learning to classify images in a time in which heruristic procedures were the rulers of this branch of science. Also, it proposed the famous and actually known as AlexNet's architecture (named after [Alex Krizvhesky](https://www.cs.toronto.edu/~kriz/)) for CNNs; yet the paper was published in 2012, it is still important and used today, being the foundation of [Caffe](https://caffe.berkeleyvision.org/) framework. 

+ [Selective search for object recognition](https://link.springer.com/article/10.1007/s11263-013-0620-5) (2013). The graph-based algorithm designed in Felzenswalb's 2004 paper was an important piece in the duel with object detection; but it proposed many regions, way more than was semantically plausible. In this scenario, Uijlings and his partners designed a greedy algorithm to merge the regions computed by Felzenswalb's procedure (it used some heuristic methods; for instance, it should conveniently merge regions in which one is the boundary of the other); this would posteriorly be the main component of deep learning based methods for object classification. 

+ [Rich feature hierarchies for accurate object detection and semantic segmentation](https://arxiv.org/abs/1311.2524) (2014). We already have papers that aim to partition an image in semantically convenient regions, which are images themselves; we also have methods for addressing the classification of figures in general (for instance, Alex seminal work). What is the next step? You know it! Join everything in a unified system that starts with a set of some thousands of regions and then classify them using the feature vector extracted with a convolutional neural network; that is exactly what was designed in Girshick's (and partners') paper. Precisely, the framework started with the computations of auspicious regions with Selective Search's algorithm; with this, a feature vector was, with a deep convolutional neural network, extracted for each region and subjected to classification with an SVM: the whole framework was called RCNN ("Regions with CNN"). 

+ [Spatial pyramid pooling in deep convolutional networks for visual recognition](https://arxiv.org/abs/1406.4729) (2014). We are well informed that the convolutional neural networks are the game changer of, oh, possibly (almost) everything? However, they have a inappropriate property: their inputs must be of fixed sizes; that is, the image must have a adequate quantity of pixels and those pixels must be arranged in a adequate grid with adequate dimensions. Those adequations, however, are strong; we usually, for instance, need to reshape the input image to feed forward it to in a CNN, generating an conveniently sized feature vector. In this context, He, Zhang, Ren and Sun proposed a framework that aimed to accept arbitrarily shaped images; for this, they inserted an adaptative pooling layer (more accurately, a layer whose architecture is conditinal to the structure of the input image) that would culminante in a feature vector of appropriate size. It was OK for the time; but the training was excessively cumbersome. 

+ [Very deep convolutional networks for large-scale image recognition](https://arxiv.org/abs/1409.1556) (2015). When we design a CNN, we must be careful in the choice of hyperparameters; importantly, we must decide whether it should be deep or shallow. In this paper, Simonyan and Zisserman designed a deep learning framework with more than 15 layers for image classification and recognition; and it was awesome. Currently, we call it the VGG-16 architecture; VGG is the name of the research group that studied it (Visual Geometry Group, in the University of Oxford) and 16 was, in the time of its publication, the next year. 

+ [Fast R-CNN](https://arxiv.org/abs/1504.08083) (2015). [Ross Girshick](https://www.rossgirshick.info/) proposed, in 2014, the RCNN framework; albeit its historical importance -- as it is written in the slides, it was the spark that lightened the path for the design of more appropriate procedures --, it doesn't appropriately share the computation between pixels. Precisely, RCNN independently classify each region; in particular, it must feed forward a CNN (VGG!) for each proposal, which is computationally exhaustive. Girshick, then, proposed modifying RCNN's architecure: in Fast RCNN, the image is initially feed forwarded in the convolutional neural network, generating a feature map; then, we project the proposals computed with the Selective Search algorithm and classify those projections using a fully connected layer neural network. Therefore, the proposals are still computed with a heuristic procedure, but we have an complete procedure that can be jointly trained to label objects in images; the current state-of-the-art, however, would unfold with the next RCNN. 

+ [Faster R-CNN: Towards real-time object detections with regions proposal networks](https://arxiv.org/abs/1506.01497) (2016). Ren, He and Sun, the designers of the Spatial Pyramid Pooling architecture for arbitrarily shaped inputs in CNNs, and Girshick, the computer scientist that introduced RCNN and Fast RCNN, joined, in 2016, to delineate a fully trainable and completely deep learning based system for object recognition and classification; precisely, they designed a Region Proposal Network (RPN), whose objective is to generate the regions to be classified with Fast RCNN. The culmination of this was, so, the Faster RCNN; it is still a robust lightsaber that computer vision scientists use to duel with the dark side of the semantic description of images. 

+ [Lecture 11: Detection and segmentation](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture11.pdf) (2017). In the University of Standford, they have a course specifcally designed for the applications of convolutional neural networks in visual recognition tasks; it is named criptically for foreigners -- [CS231n](http://cs231n.stanford.edu/) --, but you can watch their classes with lovely professors on [YouTube](https://www.youtube.com/playlist?list=PL3FW7Lu3i5JvHM8ljYj-zLfQRF3EO8sYv). 

+ [Chart mining: A survey of methods for automated chart analysis](https://ieeexplore.ieee.org/document/9085944) (2021). In our presentation, there was a duality: on the one hand, we should introduce the wide topic of object detection; on the other hand, we needed to provide some aspects of the possibly esoteric area of automatic chart analysis. For this task, we described what are our intentions when we write about automatically describing charts, and why it is worth researching about it; but we didn't write about the actual methods that people use in this instance of semantic description of images. However, if your objects contemplate the profound exploration of this topic, Davila and his partners provide a structured and recent review of the main methods for extracting information of charts; in particular, they explore the extraction of data from bitmap chart images and the generation of publicly annotated data sets. 

Also, other references didn't directly shape the slides nor the presentation, but possibly it is worth writing about them: [Mask RCNN](https://arxiv.org/abs/1703.06870), for instance, is a deep learning method for image segmentation (that is, it aims to assign to each pixel in a image a label, in opposition to the computation of a bounding box that covers an object which we desire to detect); [this](https://idl.cs.washington.edu/papers/reverse-engineering-vis/) paper, on the other hand, proposed a complete system to generate the specification (that is, the visual encondings, specifically the textual visual encondings) of bitmap chart images; and [this](https://ieeexplore.ieee.org/document/8017646) designed a system to extract and update the color mappings in bitmap image visualizations (but the pipeline required a human intervation to label the region in which the legend with the color mapping was; our implementation aims to automate this step). 
 
