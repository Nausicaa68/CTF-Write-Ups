# Tinder

> 50 points
>
> Easy
> 
> Ca va être compliqué de match la :
>
> CYBN{([^[^a-z0-9A-X]|[^Z]])0{0}1{0}0{1}u{1}_(?#Ab^[1-4][5555-7-8-9-2]).(?<=4)[r-r]((((3_))))(?#[a-z]|[3-4]|[1-2])([t](h)[3](_))(?#.[a-Z0-5]...)t[r-r]u{1}((((3_))))r3g3x_(?#[a-z]|[3-4]|[1-2])([^[a-l]|[^n-z0-9A-X])0{0}1{0}4{1}st.(?<=3)r{1,10}}
>
> Auteur : Maestran
>
> Flag : CYBN{Y0u_4r3_th3_tru3_r3g3x_m4st3r}

Ô calisse, v'là un sacré Regex

## Un Regex ?

Un Regex, ou Expression Régulière, est un outil utilisé en programmation pour trouver des correspondances dans des chaînes de caractères. Les expressions régulières peuvent être utilisées pour vérifier si une chaîne de caractères contient un certain motif, ou pour extraire des parties spécifiques d'une chaîne de caractères. Les expressions régulières sont très utiles pour des tâches de traitement de texte, telles que la validation de formulaires, la recherche et le remplacement de sous-chaînes dans un texte, et bien d'autres.

## Comment on décode ce truc ?

Pas à la main, on est pas fou. On va utiliser *[exrex](https://pypi.org/project/exrex/)* (mais d'autres libs existent).
```
pip install exrex
```

```python
import exrex

data = '([^[^a-z0-9A-X]|[^Z]])0{0}1{0}0{1}u{1}_(?#Ab^[1-4][5555-7-8-9-2]).(?<=4)[r-r]((((3_))))(?#[a-z]|[3-4]|[1-2])([t](h)[3](_))(?#.[a-Z0-5]...)t[r-r]u{1}((((3_))))r3g3x_(?#[a-z]|[3-4]|[1-2])([^[a-l]|[^n-z0-9A-X])0{0}1{0}4{1}st.(?<=3)r{1,10}'

print(exrex.getone(data))
```
```
Output :
5]0u_A4r3_th3_tru3_r3g3x_R4st\3rrrrrrrrrr
```

Ah, il y a des paramètres fixes, mais certains sont variables. Pas le choix, va falloir y aller à tâtons.

Bon, on peut y deviner la phrase en leet : You are the true regex master. On peut donc deviner que le flag est :
```
CYBN{Y0u_4r3_th3_tru3_r3g3x_m4st3r}

Et voilà le flag UwU !
