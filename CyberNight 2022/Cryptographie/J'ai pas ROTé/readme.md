# J'ai pas ROTé

> 25 points
> Easy
> 
> votre collègue, adepte de blagues plus que de cryptographie, vous envoie la phrase suivante dans la conversation d'équipe: "j'vous promets les gars, cette fois, j'ai pas ROTé: 871 1157 858 1014 1599 1287 507 663 1508 1261 1365 1508 1235 1456 676 1495 1235 637 1235 1287 663 1495 1261 1482 1625"
> 
> Auteur : Lmeaou
>
> Flag : CYBN{c'3tait_p4s_1_c3sar}

## Les bases

On va commencé par définir le rotationel. Cela consiste à intervertir les symboles en faisant une rotation. Par exemple, un rotationnel 13 donne pour bonjour le mot rkrzcyr.

**image alphabet.png**

Chaque lettre est inversé avec la 13e lettre plus loin. Les plus attentifs y veront un chiffrement de César de clé = 13.

## Notre challenge maintenant

Qu'avons nous ? Des chiffres. 

```python
data = [871, 1157, 858, 1014, 1599, 1287, 507, 663, 1508, 1261, 1365, 1508,
        1235, 1456, 676, 1495, 1235, 637, 1235, 1287, 663, 1495, 1261, 1482, 1625]
```

Si on prend les premiers chiffres et qu'on mesure leurs écarts, on trouve :
- 1157 - 871 = 286
- 1014 - 858 = 156

On va supposer que le début est "CYBN". Nous allons donc tester des valeurs de décalage pour i jusqu'à trouver les mêmes valeurs qu'au dessus.

```python
import string
alphabet = string.ascii_uppercase

for i in range(1, 30):
    print("i =", i)
    print("Y - C = ", (alphabet.index('Y') - alphabet.index('C')) * i)
    print("N - B = ", (alphabet.index('N') - alphabet.index('B')) * i)
    print()
```

```
Output :
i = 1
Y - C =  22
N - B =  12

i = 2
Y - C =  44
N - B =  24

i = 3
Y - C =  66
N - B =  36

i = 4
Y - C =  88
N - B =  48

i = 5
Y - C =  110
N - B =  60

i = 6
Y - C =  132
N - B =  72

i = 7
Y - C =  154
N - B =  84

i = 8
Y - C =  176
N - B =  96

i = 9
Y - C =  198
N - B =  108

i = 10
Y - C =  220
N - B =  120

i = 11
Y - C =  242
N - B =  132

i = 12
Y - C =  264
N - B =  144

i = 13
Y - C =  286
N - B =  156

i = 14
Y - C =  308
N - B =  168

i = 15
Y - C =  330
N - B =  180

i = 16
Y - C =  352
N - B =  192

i = 17
Y - C =  374
N - B =  204

i = 18
Y - C =  396
N - B =  216

i = 19
Y - C =  418
N - B =  228

i = 20
Y - C =  440
N - B =  240

i = 21
Y - C =  462
N - B =  252

i = 22
Y - C =  484
N - B =  264

i = 23
Y - C =  506
N - B =  276

i = 24
Y - C =  528
N - B =  288

i = 25
Y - C =  550
N - B =  300
```

En fait lol c'est 13.

Pour i = 13, on trouve comme valeur les mêmes qu'avant : 
- 1157 - 871 = 286
- 1014 - 858 = 156

```
i = 13
Y - C =  286
N - B =  156
```

Il suffit de diviser par 13 les chiffres du message, puis de les transformer en caractères.

```python
newdata = []
for x in data:
    newdata.append(
        chr(int(x / 13))
    )

print(list(newdata))
```

```
Output :
['C', 'Y', 'B', 'N', '{', 'c', "'", '3', 't', 'a', 'i', 't', '_', 'p', '4', 's', '_', '1', '_', 'c', '3', 's', 'a', 'r', '}']
```

Puis on transforme ça en string.

```python
flag = ""
for i in newdata:
    flag += i
print(flag)
```

```
Output :
CYBN{c'3tait_p4s_1_c3sar}
```

## Le beau oneliner

```python
print(''.join(list(map(lambda a: chr(int(a/13)), [871, 1157, 858, 1014, 1599, 1287, 507, 663, 1508, 1261, 1365, 1508,
                                                                       1235, 1456, 676, 1495, 1235, 637, 1235, 1287, 663, 1495, 1261, 1482, 1625]))))  # trivial non
```

```
Output :
CYBN{c'3tait_p4s_1_c3sar}
```

Et voilà le flag UwU !