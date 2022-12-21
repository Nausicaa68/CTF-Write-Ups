# Auth 2

> 25 points
>
> Easy
> 
> Bon en vrai au début j'étais naze, je retente ! 
> Le flag n'est pas au format cybn{}
>
> Auteur: m00n
>
> Flag : CYBN{b3773r_4u7h_m4yb3}

En regardant le code, on constate que la condition d'obtention du flag est que a == b.

Or a et b sont donnés dans le code source, mais sont encodé en base64. On le sait en regardant le code. Les deux premières phrases de consignes sont également encodés de la même manière, mais sont décodé comme suit lors de l'affichage : 

```python
print(base64.b85decode(wlcm.decode()).decode())
b = input(base64.b85decode(prmt.decode()).decode())
```

Ainsi, b est notre entrée, et va devoir être égale à a pour être validé. a = 'Vly{4Gjd-vbvI~VZ8UjeGX' en base 64. On va décoder "a" de la même manière : 

```python
print("a = ", base64.b85decode(a.decode()).decode())
```

```
Output :
a =  b3773r_4u7h_m4yb3
```

On obtient notre flag.