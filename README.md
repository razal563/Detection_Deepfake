# Détection de Deepfake

Bienvenue dans notre projet de détection de deepfake.  
Ce référentiel contient des outils et des ressources pour aider à détecter les deepfakes, qui sont des contenus manipulés générés par des techniques d'intelligence artificielle.

## Contenu du Référentiel

- Modèles de détection de deepfake pré-entraînés : **Resnet101**
- Scripts d'évaluation de la détection de deepfake : **Dossier Fine-Tunning et Fine-Tunning + Retinex**
- Données d'entraînement pour les modèles : **Dataset LAION et Dataset DiffusionDB** 

## Modèle

Le modèle ResNet-101 fait partie de la famille des architectures de réseaux de neurones profonds appelées ResNets,  
introduites par Kaiming He et al. en 2015. Ces réseaux sont célèbres pour leur capacité à former des modèles profonds avec une stabilité et une facilité accrues, grâce à l'introduction de connexions résiduelles.  
Ils permettent de résoudre le problème de la disparition du gradient dans les réseaux très profonds.  
Le modèle a été pré-entraîné sur ImageNet avec environ 1 million d’images réparties sur 1000 classes.   
J'ai donc modifié la couche fully connected pour renvoyer 2 classes au lieu de 1000 classes.

**Architecture du modèle**

![Capture d’écran 2024-01-24 172801](https://github.com/razal563/Detection_Deepfake/assets/119457644/04db15d0-f38f-4853-ace2-31add8525f16)

## Ensemble de données

**Données**
- 1000 images réelles (LAION)
- 1000 images deepfake
(DiffusionDB est le premier ensemble de données de prompts texte-vers-image à grande échelle.  
Il contient 14 millions d'images générées par Stable Diffusion en utilisant des prompts et des hyperparamètres spécifiés par de vrais utilisateurs.)  
Voici le lien des images deepfake dont l'auteur à supprimer les droits: [Consulter le lien](https://huggingface.co/datasets/poloclub/diffusiondb)  

**Répartition des données**
- Entrainement ~1600 images  
- Validation ~200 images    
- Test ~200 images    

**Traitement des images**
- Redimensionner en 224x224 pixel  
- Normaliser

## Dossier Fine-Tunning

J'ai entrainé mon modèle pré-entrainé sur plusieurs couches.   
Sur la couches Fc, la 3ème couche et la 4ème couche. 

## Dossier Fine-Tunning + Retinex

Dans ce code je m'inspire de l'article suivant: [Consulter le document PDF](http://staff.ustc.edu.cn/~zhangwm/Paper/2022_26.pdf)  
Sauf que j'utilise Retinex qui est un modèle de traitement d'image qui vise à améliorer la qualité et la perception des couleurs dans les images en corrigeant l'équilibre des couleurs et en augmentant la dynamique du contraste.   
L'idée fondamentale du Retinex est basée sur la façon dont le système visuel humain perçoit les couleurs en fonction de la lumière incidente.  
Et donc, mon modèle prend deux images en entrée : l'image de base sans pré-traitement et l'image avec pré-traitement, en utilisant la différence absolue entre l'image de base et l'image obtenue après avoir appliqué Retinex. 
<br><br>
![Capture d’écran 2024-01-24 172024](https://github.com/razal563/Detection_Deepfake/assets/119457644/62923164-aa37-4a9f-bee0-37ffe5c4e81a)  

## Résultat 

**Sans Pré-traitement**

| Fc + couche 3 + couche 4  | Fc + couche 4 |
|---------------------------|---------------|
|            91%            |     90,5%     |  

**Avec Pré-traitement et capture de l'incohérence de la réflexion de la lumière**

| Fc + couche 3 + couche 4  | Fc + couche 4 |
|---------------------------|---------------|
|          85,5%            |      83%      |  

## Conclusion

L'importance des choix des couches lors de l'entraînement d'un modèle peut avoir des conséquences significatives.   
Fine-tuner un modèle pré-entraîné peut considérablement améliorer les scores de performance, offrant ainsi une solution efficace pour des tâches spécifiques tout en capitalisant sur les connaissances préalables du modèle.   
L'information lumineuse dans les images renferme des caractéristiques sémantiques plus riches. Exploiter ces caractéristiques de manière appropriée peut grandement contribuer à l'amélioration des performances de notre modèle de classification,   
soulignant l'importance d'une préparation minutieuse des données.
Dans le contexte de la détection de deepfake, un jeu de données peu diversifié peut entraîner une mauvaise généralisation, notamment sur des images générées par des modèles inconnus.   
Cela souligne l'importance cruciale de la diversité des données dans de telles tâches.   
Bien que la détection de deepfake soit une considération très importante, il est intéressant de noter que les modèles ResNet50 et ResNet101 présentent des performances similaires dans ce contexte spécifique.

**Perspectives**  

Augmenter l'ensemble de données pourrait être une approche pour améliorer les performances, en introduisant une plus grande diversité d'images pour favoriser une meilleure généralisation.   
L'intégration d'images générées par des GAN (Generative Adversarial Networks) dans l'ensemble de données pourrait être explorée pour rendre le modèle plus robuste aux diverses méthodes de création de contenu falsifié.   
Pour optimiser davantage les performances, il serait judicieux d'explorer des techniques plus avancées pour tirer parti des informations lumineuses présentes dans les images, afin d'améliorer la capacité du modèle à discerner les caractéristiques importantes.  
