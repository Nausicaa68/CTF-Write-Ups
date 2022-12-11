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

## Mais dis moi Jamy, qu'est que le G-code ?

Le G-code, Fred, est un langage de programmation de commande numérique permettant de définir des séquences d'instructions afin de piloter des machines-outil à commande numérique.

L'article Wikipedia détaillant le G-code est très bien fait. (https://fr.wikipedia.org/wiki/Programmation_de_commande_num%C3%A9rique)

Pour voir ce que ce G-code construit, on peut utiliser le site web [NCviewer](https://ncviewer.com/) (à ajouter d'urgence dans votre liste de liens utiles pour CTF !)

Voilà ce qu'on obtient : 

**image truc complet**

**image AH! denis**

## Fouillons

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

**image layer1 sans rap mouv**

Voilà qui semble intrigant. En activant le "show rapid movement", on peut voir les mouvements de la tête. Et là, magie, elle dessine CYBN.

**image cybn**

## Le flag, le flag !

En regardant la couche 3, on obtient : 

**image chouche3**

Et voilà le flag UwU !