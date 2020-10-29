#Info-h-500
-------
##Module 1
=========
La fonction principale est la fonction watermark()

###Arguments
------------
  - 'image', L'adresse d'une image de base
  - 'watermark', L'adresse d'une image qui servira de watermark
  - 'pos', la position à laquelle le watermark doit être placé. Elle peut être exprimé par une pair de nombre, ou par une position relative
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
