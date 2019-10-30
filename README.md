# Identification of Handwritten Letters Using Persistent Homology

This project uses methods from Topology to classify handwritten letters. Using Persistent Homology we're able to...

## Introduction

### Persistent Homology

### Scans

## Getting Started

This is a standalone project, to get started all you need to do is downloade the Jupyter Notebook and run it on a Python 2 kernel. Functions in the notebook should be well documented enough to understand what they do.

### Prerequisites

To run the Jupyter Notebook you will need to install persim and ripser. This repository also contains a copy of our dataset, so we clone the repository as well. On top of installations, you'll need to import a number of libraries. Here's the code we currently use at the beginning of our program.

```
%%capture
!pip install ripser
!pip install persim
!git clone https://github.com/SWHulbert/TDA-Project.git
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import random as rnd
from scipy import ndimage
import PIL
from persim import plot_diagrams
from ripser import ripser, lower_star_img
```

## Running the tests

Our program tests on data called dataT, (dataT is dataTest for short), dataT is an exact copy of our original data, but 'noise' is added by flipping bits, either from 0 to 1, or 1 to 0, with a certain probability (the percentage can be specified). Empirically, we've found 4% noise to be a good test case, where the original letters are still recognizable, but also clearly distinct from our original data.

Our program further 'denoises' the data, by removing any bit or 1, that is not connected to any other 1. It does this by simply checking all values around a specific bit and summing them, if the sum is > 0, then our bit is connected, otherwise it is unconnected and removed from the data.

To see how accurate our program is for a specific letter, you can run the perCorrect() function. This function require a letterIndex = a, noisePercent = b, numberofGuesses = c, and denoiser = TRUE or FALSE, by default noisePercent = 0.04, numberofGuesses = 10, denoiser = TRUE. After running, the perCorrect function will spit out a 2-tuple, (letterIndex, percent correct guesses/total number of guess)

To see how our model does on all capital letters in the English Alphabet, you can run code like this:

```
for y in range(26):
  print(y, perCorrect(y, 0.02, 50))
```

Here you can see we specificed the noisePercent = 0.02, and numberofGuesses = 50.

## Optimization of the Model

Originally, our model ran with 8 scans, and record the values of total number of classes, and average length of classes. However, as we added more scans, we noticed that accuracy, especially for specific letters such as A, D, O, and Y went down. Through the simple gumshoe move of testing each scan individually, then each pair of scans individually, each 3-tuple of scans, etc. we removed scans that were not contributing to our model.

To do this, we compared a model with scan X, to a model without scan X, and calculated average accuracy over all letters in the alphabet. If average accuracy went up by a significant ammount (we used "Did average accuracy increase by 3% or more" as a cutoff question for our model). After running this test, we removed 2 scans that were below the cutoff, decreasing the overall runtime of our program.



```
Give an example
```

## A Comparison to Neural Networks

Add additional notes about how to deploy this on a live system

## Built With

* [Google Colab](https://colab.research.google.com/notebooks/welcome.ipynb) - The web framework used
* [Maven]() - Dependency Management
* [ROME]() - Used to generate RSS Feeds

## Authors

* **Seth Hulbert**
* **Yajun Fu**
* **Vinitha Elangovan**
* **Keerthi Padamata**
* **Nitheen Jammula**
* **Alexis Fiddemon**

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
