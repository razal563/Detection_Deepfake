# Détection de Deepfake

Bienvenue dans notre projet de détection de deepfake.  
Ce référentiel contient des outils et des ressources pour aider à détecter les deepfakes, qui sont des contenus manipulés générés par des techniques d'intelligence artificielle.

## Contenu du Référentiel

- Modèles de détection de deepfake pré-entraînés : **Resnet101**
- Scripts d'évaluation de la détection de deepfake : **Dossier Fine-Tunning et Fine-Tunning + Retinex**
- Données d'entraînement pour les modèles : **Dossier Dataset et Dataset_généralisation** 

## Modèle

Le modèle ResNet-101 fait partie de la famille des architectures de réseaux de neurones profonds appelés ResNets,  
introduits par Kaiming He et al. en 2015. Ces réseaux sont célèbres pour leur capacité à former des modèles profonds avec une stabilité et une facilité accrues, grâce à l'introduction de connexions résiduelles.
Ils permettent de résoudre le problème de la rétropropagation du gradient dans les réseaux très profonds. 
Le modèle a été pré-entraîné sur ImageNet 1K ~ 1 Million d’images avec 1000 classes.
J'ai donc modifier la couche fully connected pour renvoyer 2 classes au lieu de 1000 classes. 
