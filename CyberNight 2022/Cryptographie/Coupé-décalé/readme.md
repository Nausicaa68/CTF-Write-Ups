# Coupé-décalé

> 25 points
>
> Easy
> 
> J'espère que vous avez une bonne vue.
>
> Auteur : Marie-Jeanne
>
> Flag : CYBN{NOW-YOU-SEE-ME}

Avec un peu de tâtonnement, on finit partrouver qu'il faut faire un décalage de César sur chaque lettre, en augmenter le décalage de 1 par ligne. 

En gros, la première ligne subit un décalage de -1, le C devient B. La deuxième ligne subit un décalage de -2, le T devient R et le C devient A. 

```python
import string
alphabet = string.ascii_uppercase

data = ["C", "TC", "YRO", "IJPE", "LJXYS", "UCEUAY",
        "LLTLPSM", "ICBIRWCB", "NAMNBCRA", "ODCOXDBO", "NLSBFPXZE"]

print(''.join(
    [alphabet[
        (alphabet.index(letter) + 26-i-1) % len(alphabet)
    ] for i in range(len(data)) for letter in data[i]]
))
```

```
Output :
BRAVOLEFLAGESTNOWYOUSEEMEILFAUTAJOUTERDESTIRETSENTRECAHQUEMOT
```

Ce qui donne BRAVO LE FLAG EST NOW YOU SEE ME IL FAUT AJOUTER DES TIRETS ENTRE CAHQUE MOT. Pas foutu de faire un flag sans fautes d'orthographe.
