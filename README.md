# Classification automatique de biens de consommation


# 1. Le contexte

Une entreprise souhaite lancer une marketplace e-commerce. Sur la place de marché, des vendeurs proposent des articles à des acheteurs en postant une photo et une description.

Pour l'instant, l'attribution de la catégorie d'un article est effectuée manuellement par les vendeurs. Pour rendre l’expérience utilisateur des vendeurs (faciliter la mise en ligne de nouveaux articles) et des acheteurs (faciliter la recherche de produits) la plus fluide possible, et dans l'optique d'un passage à l'échelle, il devient nécessaire d'automatiser cette tâche.

Ce notebook a pour but de réaliser une étude de faisabilité d'un moteur de classification d'articles, basé sur une image et une description, pour l'automatisation de l'attribution de la catégorie de l'article.

Ainsi il est réalisé un prétraitement des descriptions des produits et des images, une réduction de dimension, puis un clustering. Les résultats de la réduction de dimension et du clustering sont présentés sous la forme de graphiques en deux dimensions, et confirmés par un calcul de similarité entre les catégories réelles et les clusters afin d'illustrer le fait que les caractéristiques extraites permettent de regrouper des produits de même catégorie.


# 2. Les données

![image](https://user-images.githubusercontent.com/108366684/195922110-3bbd390e-d180-4806-9579-8cfa820db935.png)

![image](https://user-images.githubusercontent.com/108366684/195922911-4036861e-2d4f-4334-afb3-7e212c31fe60.png)


# 3. Clustering du texte des descriptions

![image](https://user-images.githubusercontent.com/108366684/195923626-fdfc19fc-e80d-4d88-8276-7974d31086ee.png)

Analyse des erreurs du modèle MPNET:
Il apparait qu'un certain nombres d' "erreurs" n'en sont pas. Il conviendrait donc de corriger les erreurs de catégorie provenant des vendeurs avant d'exécuter les algorithmes de clustering.
![image](https://user-images.githubusercontent.com/108366684/195923958-617e4ce0-53f0-4b12-9ba8-15505574ad5f.png)


# 4. Clustering des images

![image](https://user-images.githubusercontent.com/108366684/195924586-842c31e1-32a3-4ee2-afbb-f84ded540de6.png)

![image](https://user-images.githubusercontent.com/108366684/195928187-8b1a357c-4f20-48eb-a969-576602b43bec.png)

Analyse des erreurs du modèle Xception:
![image](https://user-images.githubusercontent.com/108366684/195928895-00156af3-820e-4914-806a-ac6dfc63fbb6.png)


# 5. Classifieur d'images

Sur la base du modèle Xception, on crée un classifieur en ajoutant une couche dense à 7 cellules avec softmax à la sortie de l’Xception et en entraînant les 8 dernières couches (fine-tuning). Les scores sont les suivants:
accuracy de 0.76 sur le jeu de validation (1.00 sur le jeu d’entraînement) et ARI de 0.83.

![image](https://user-images.githubusercontent.com/108366684/195926071-8ab11034-a873-4f22-9d4a-8f8a60ec1d27.png)


# 6. Clustering textes & images combinés

![image](https://user-images.githubusercontent.com/108366684/195926741-7e0515b9-59bc-4670-8b56-2ab8452ecf45.png)
![image](https://user-images.githubusercontent.com/108366684/195926843-c09f04d6-4a39-48a7-816b-332032d615cd.png)


# 7. Conclusion

Les résultats de la présente étude de clustering (ARI>=0.7) sur seulement 1050 produits montrent la faisabilité d’un moteur de classification automatique des produits sur la base d’une description et/ou d’une photo.

Pour le classifieur final, il conviendra d’utiliser beaucoup plus de produits (voire aussi de vérifier manuellement les catégories fournies pour corriger les erreurs) afin d’obtenir de meilleurs scores.


