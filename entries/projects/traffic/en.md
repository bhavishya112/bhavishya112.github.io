---
title: "Traffic Sign Classification with CNN"
type: project
layout: case-study
lang: en
slug: traffic
permalink: /entries/traffic/
date: 2025-04-15
year: 2025
image: "/images/projects/example-project/cover.svg"
thumbnail: "/images/projects/traffic/confusion_matrix.png"
cover: "/images/projects/traffic/architecture.png"
cover_alt: "Placeholder cover image for the example project"
thumbnail_alt: "Placeholder thumbnail for the example project"
label: "PROJECT"
role: "ML Developement and Data Science"
technologies: [CNN, Computer Vision, Tensorflow, OpenCV, Python ]
code: "https://github.com/bhavishya112/GoogLeNet-IMAGE-CLASSIFICATION"
demo: ""
paper: ""
excerpt: "A CNN based solution to classify traffic images across 43 different categories."
---

<!-- This is an example project entry. Duplicate this folder (`entries/projects/example-project/`) to add a real project, or edit this file in place. -->

## Problem

<!-- Describe the problem you were solving and why it mattered. -->
I was at Deep Learning, and i thought why not come up with something that can runs on edge computing, and helps autonomous vehicles detect traffic signal, since that's one of the most important parts of driving, So i started making a Neural Network for this very reason.

## Approach

<!-- Describe what you built and the key decisions along the way. This is a good place for a diagram, a code snippet, or a short list of the technologies involved. -->

Initially, i was following a 4-5 layers CNN architecutre as that sort of resembles VGGNet[but was not that], but i didn't give it much of an importance.

Then i started reading some research papers so that i follow more structured approach to this : like VGGNet, LeNet, and GoogLeNet Inception, then i came across their major findings.

VGGNet : This paper was explaining how you could improve your model's performance by increasing more CNN Layers and making it more deep.<br><br>
LeNet : This paper was explaining how 1x1 convolutional bottlenecks are really good for performance & more fuller representations.<br><br>
GoogLeNet : This paper was sort of Competing with VGGNet, saying that Deeper the NN goes, the more computation-heavy it becomes. It very extensively used the findings from LeNet paper, owing to its performance benifits.
The paper introduced parallel representations of the same Feature Map/Image, representations from different perspectives : sort of looking at finer details and looking at larger details at the same time.

So i just took their findings as my railings and started building one of my own, and 60% of the times it was just experimentation, what works, what doesn't, and reasoning behind it. I had to do a lot of Tensorboard logs just to see what wents which way.

I Started Building the project in Step by Step manner : <br>
First i took GTSRB Dataset, Downloaded it. Then as usual, I made a logic to read the repository of dataset, and load it in my device.


Then **i moved to preprocessing and augmentation part**, since the dataset was highly skewed - there were 7-8 categories having as low as 100-200 images and **i didn't recommend myself augmentation, since either that would make some categories tolerant to variations like rotations, random crop, lighting up and down, while other categories would remain same OR the whole model recieves less quality - less diverse dataset.**
So i just did preprocessing of images like normalizing pixel values, or some images were over-exposed, i reduced their alpha and vice-versa.
And the dataset didn't require much preprocessing.


Then **about balancing dataset** : i used scikit-learn weight calculation, so basically you calculate the ratio w<sub>c</sub> = N/(N<sub>c</sub>*k).<br>
where <br>
w<sub>c</sub> = weight of class c <br>
N = total number of training examples<br>
N<sub>c</sub> = Number of examples in category c<br>
k = number of categories<br>
so that classes with less examples are weighed more, consequently its almost the same as increasing learning rate of that particular category by the same ratio, so since you have less training examples, so you'd take longer jumps but in a constrained manner limited by the weight.

Then came **building the architecture**, during this phase 
**I did changes to batch sizes, learning rates, dataset augmentations, Train-Eval-Test sets partitioning, number of layers, convolutional filters, wider[not deeper] architecture and more.**
so i verified the findings of those researchers through my own experimentation.


Then I went on to getting the results.


## Result

<!-- Describe the outcome: what changed, what you measured, or what you learned. -->
MY KEY FINDINGS THROUGH EXPERIMENTATION :<br>
(1) Too Large Batch size worsens learning<br>
(2) 1x1 convolutions increase performance[reduced time/step], when they are used inside Inception Layers, and in that specified way.<br>
(3) Through Dataset augmentation, NN can be made invariant to many things like rotate image, colors, lightings, or many things.<br>
(4) You increase more filters in the middle layers, so that we get more abstract representations and classification becomes better.<br>
(5) Keep learning Rate low [but not too much] to keep it easy going [so that it doesn't wobble in the end].<br>
(6) Increasing Image Dimensions drastically increases computational requirements, i was at 80x80 and the time/step was around 100ms [or so, i don't remember].


HERE ARE SOME RESULTING METRICS :<br>
### F1 Score

<img src="/images/projects/traffic/tensorboard/f1.png"
     alt="F1 Score"
     style="width: 500px; height: auto;">

### Top-5 Score

<img src="/images/projects/traffic/tensorboard/top5.png"
     alt="Top-5 Score"
     style="width: 500px; height: auto;">

### Precision Score
<img src="/images/projects/traffic/tensorboard/precision.png"
     alt="Precision Score"
     style="width: 500px; height: auto;">

### Recall Score

<img src="/images/projects/traffic/tensorboard/recall.png"
     alt="Recall Score"
     style="width: 500px; height: auto;">

### Accuracy

<img src="/images/projects/traffic/tensorboard/accuracy.png"
     alt="Accuracy"
     style="width: 500px; height: auto;">

Note:<br>
**1.** I didn't give much importance to accuracy since the dataset was imbalanced [although i was doing weighing of different categories].<br>
**2.** The model isn't converged because this project was meant only for learning, not Deploying, with better dataset, i'd love to converge it.

INSIGHT : <br>
Since we have good precision and less recall, it means if model predicts an image to have a category C, then its highly probable that it belongs to C. But it can't correctly predict all images of the category C in the same category.
So the model is like a sharpshooter with short-term-memory loss haha :)

---

<!-- Delete this file (and its `it.md` translation) once you've added your own projects, or keep it around as a reference for the front matter fields. -->
