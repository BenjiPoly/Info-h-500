#Info-h-500
-------
##Module 1
=========
La fonction principale est la fonction watermark()

###Arguments
------------
  - 'image', L'adresse d'une image de base
  - 'watermark', L'adresse d'une image qui servira de watermark
  - 'pos', la position à laquelle le watermark doit être placé. Elle peut être exprimée par une paire de nombre, ou par une position relative
    - 'M', au milieu de l'image
    - 'TL', dans le coin supérieur gauche
    - 'TM', au milieu du bord supérieur de l'image
    - 'TR', dans le coin supérieur droit
    - 'ML', au milieu du bord gauche de l'image
    - 'MR', au milieu du bord droit de l'image
    - 'BL', dans le coin inférieur gauche
    - 'BM', au milieu du bord inférieur de l'image
    - 'BL', dans le coin inférieur droit
  - 'intensity', la force avec laquelle on souhaite voir le watermark, entre 0 et 255
  - 'color', permettant de donner une couleur au watermark à l'aide d'un tuple de 3 valeur donnant la couleur en code RGB
  - 'rotation', une valeur de l'angle de rotation que l'on souhaite appliquer au watermark
  
###Les fonctions
----------
- setPos(), permet de définir la position du pixel du coin supérieur gauche servant de référence au placement du watermark. 
- wm2bin, transforme l'image servant de watermark en une image binaire composée uniquement de 0 et de 1
- getLocalLuminosity(), renvoie la valeur moyenne de l'ensemble des pixels, sur l'ensemble des canaux de couleur si il y en a plusieurs
- applyWatermark(), soustrait ou additionne le watermark multiplié par un facteur aux pixels d'une zone de l'image d'origine. Le facteur est dépendant de la couleur et de l'intensité demandée. Dans le cas ou un pixel serait déjà trop sombre ou trop clair, le pixel est simplement mis à sa valeur maximale ou minimale


-------
##Module 2
=========
The first bloc is the "enhancement". It's divided in many small steps.
  - Histogram stretching, finding the thresholds automatically based on each histograms (I kept 95% of the original histogram)
  - Small value modification in HSV
  - Enhancement of borders, unsing a canny edge detector and marking lightly the edges
  - Equalization of the histograms

###Bonuses
------------
Trying to find some ideas and techniques, I found some filters I implemented
  - A painting like transformation using a sobel filter
  - A sepia transformation (A simple mathematical operation)
  - A Black&White transformation
  - A drawing like transformation. It uses a Look-Up Table to reverse the image, a gaussian filter to blur it, and a "dodging" operation
  - A pencil sketch like transformation. It is a sobel filter, followed by a LUT to reverse it.
  - A bigger pencil sketch like transformation. It is the same as the previous transformation, with a dilation before the LUT.
 
-------
##Module 3
=========
The goal is to segment the tumour region. I used two different approach to do so.

The first approach is very basic : 
  - Transform the image in a one canal image (black and white)
  - Filter the image using a median filter to remove artefact from JPG compression, but keeping the borders
  - As we can see in the image, the tumour region is pretty obvious and is much clearer than the rest. Looking at the histogram, I manually pu a threshold at the 175 gray value
  - The result fit pretty good the tumour shape
  
The second approach is a bit more automatic : 
  - I first compute the gradient on the median filtered image
  - At first I choose 3 markers, one in the tumour, one in the backgroud, and the last one in the sain brain
  - I applied the watershed transform on the gradient image using those markers, and the tumor is segmented
  - To improve a bit, I used the minimum gradient points to find automaticaly some markers
  
---------------
Tumour surface

The manual method and the automatic method give pretty similar result for the tumour surface
  - Manual surface : 44.77 cm²
  - Watershed transform with manual markers : 45.92 cm²
  - Watershed transform with automatic markers : 45.92 cm²
