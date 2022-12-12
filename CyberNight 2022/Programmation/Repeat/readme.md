# Repeat

> 25 points
>
> Easy
> 
> Timon : Il te faut peut-être une autre méthode, répète après moi : Hakuna Matata. Simba : Quoi ?! Pumba: Ha-ku-na Ma-ta-ta ! ça veut dire: pas de soucis !!
>
> nc 10.242.0.1 10002
>
> Auteur : Maestran
>
> Flag : CYBN{S0m3t1m3s_1t's_34s13r_t0_4ut0m4t3_n0?}

En se connectant à l'adresse donnée, on nous demande de recopier, en un temps très cours, les chaines de caractères qui nous sont soumises. On ne va pas pouvoir faire ça manuellement.

**image**

## Socket

Nous allons utilisé la librairie *socket*. Le but de notre algorithme va être de se connecter, puis, en boucle, de :
- recevoir les chaines de caractères : 
```python
receipt = s.recv(2048).strip().decode()
```
- construire notre réponse : on va séparer les lignes de receipt dans une liste. La première ligne est toujours une ligne d'instruction, nous demandant d'écrire. Il y a parfois plusieurs lignes à copier, parfois il n'y a rien
```python
partition = receipt.splitlines()
answer = ""
for i in range(1, len(partition)):
    answer += str(partition[i])
answer += "\n"
```
Lorsque toutes les lignes reçues sont ajoutées dans la chaine *answer*, on ajouter un retour à la ligne "\n", *Enter*, pour valider la réponse dans le terminal.

- attendre un peu et renvoyer notre réponse : 
```python
sleep(0.5)
s.send((answer).encode())
```

Maintenant, on attend. Beaucoup de chaine vont être envoyé, jusqu'à un moment avoir le flag. 

**image du terminal avec le flag**

Et voilà le flag UwU !

## Le code en entier

```python
import socket
from time import sleep

host = "10.242.0.1"
port = 10002

print("Trying to connect ...")
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((host, port))
print("Connected")

for i in range(1, 1000):
    receipt = s.recv(2048).strip().decode()
    print("Receipt :", receipt)

    partition = receipt.splitlines()
    print("Partition :", partition, "len =", len(partition))

    answer = ""
    for i in range(1, len(partition)):
        answer += str(partition[i])
    answer += "\n"

    sleep(0.5)
    print("Sending :", answer)
    s.send((answer).encode())

s.close()
```

