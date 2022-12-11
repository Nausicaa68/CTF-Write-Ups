# class4

> 50 points
> Medium
> 
> ce challenge se base sur le langage gcode.
>
>Auteur : Langley
>
> Flag : CYBN{mU17Y_14y3r}

## A l'intérieur du fichier

Bah, comme dit, c'est du G-code.

## Mais dis moi Jamy, qu'est-ce que le G-code ?

Le G-code, Fred, est un langage de programmation de commande numérique permettant de définir des séquences d'instructions afin de piloter des machines-outil à commande numérique.

L'article Wikipedia détaillant le G-code est très bien fait. (https://fr.wikipedia.org/wiki/Programmation_de_commande_num%C3%A9rique)

Pour voir ce que ce G-code construit, on peut utiliser le site web [NCviewer](https://ncviewer.com/) (à ajouter d'urgence dans votre liste de liens utiles pour CTF !)

Voilà ce qu'on obtient : 

![image](https://user-images.githubusercontent.com/58084848/206909407-0eac85f8-8ebc-4486-8c5e-6aa09f6bd0d8.png)

![image](https://user-images.githubusercontent.com/58084848/206909464-130f1b3a-75f0-427a-8659-01a60a7ad41f.png)


## Fouillons !

En cherchant un peu dans le code, on se rend compte, qu'il y a 4 couches différentes. La première et la troisième semble être très localisé sur un endroit. 

On va donc séparer les quatre couches, peut-être que quelque chose se cache en dessous.

```python
f = open("class4.gcode", "r")

files = ["begin.txt", "layer1.txt", "layer2.txt", "layer3.txt", "layer4.txt"]
numberfile = 0

layerFile = open(files[numberfile], "w")

for line in f:
    if "Layer" in line:
        layerFile.close()
        numberfile += 1
        layerFile = open(files[numberfile], "w")
    layerFile.write(line)

layerFile.close()
f.close()
```

On obtient un fichier par couche. 

Voici ce que donne la première :

![image](https://user-images.githubusercontent.com/58084848/206909525-8ca0ae07-6b4d-4062-8af6-5dcc92b75a68.png)

Voilà qui semble intrigant. En activant le "show rapid movement", on peut voir les mouvements de la tête. Et là, elle dessine CYBN.

![image](https://user-images.githubusercontent.com/58084848/206909573-7019a4d1-1011-4201-b714-841469bbe0df.png)

![image](https://user-images.githubusercontent.com/58084848/206909583-ef3ba637-f399-4f31-aaa0-7a3e9bc6a9fb.png)


## Le flag, le flag !

En regardant la couche 3, on obtient : 

![image](https://user-images.githubusercontent.com/58084848/206909610-da8110ef-93c5-4970-bb05-4e855af6c669.png)

Et voilà le flag UwU !
