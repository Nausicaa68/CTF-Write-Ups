# RSA Strong Prime Generator

> 100 points
>
> Hard
> 
> *J'ai trouvé une nouvelle méthode ultra méga sécurisé pour générer des nombres premiers pour mon RSA! *
Aie, encore un qui pense avoir inventé l'eau chaude. Arriverez-vous à lui prouver que son algorithme est mauvais ?
>
>Auteur : Maestran
>
> Flag : CYBN{d0nt_r0ll_y0ur_0wn_crypt0_dammit!!}

## Fuck RSA

Le RSA c'est toujours chiant en CTF. Mais l'avantage, c'est que ça a été retourné par tout le monde. Donc, à l'instar du petit gars du challenge qui pense avoir inventé l'eau chaude, n'essayez pas vous-même de réinventer la roue carré pour cryptanalyser le challenge. D'autres solutions existent en ligne.

## Dcode, un ami qui vous veut du bien. 

Plus de 800 outils pour aider à la résolution de jeux, énigmes, messages codés, mathématiques, etc. Ne chercher pas, vous ne pouvez rivaliser.

https://www.dcode.fr/fr （￣︶￣）↗　

## Le challenge

Pour ce challenge, nous allons utiliser l'outil de [décomposition en nombres premiers](https://www.dcode.fr/decomposition-nombres-premiers) et l'outil de [chiffrement RSA](https://www.dcode.fr/chiffre-rsa) de Dcode.

### Rappel du Rsa : 

- On prend p et q deux nombres premiers
- n = p*q
- on calcule le totient φ(n) = (p-1)(q-1)
- on prend e premier avec φ(n) (on prend souvent 65537)
- on calcule la clé privée d comme étant e^-1 modulo φ(n)

Si le pourquoi du choix de 65537 vous intéresse, un petit paragraphe vous attend tout en bas (non nécessaire pour la résolution du challenge).

### Déterminons p et q

Nous est donné dans ce challenge un fichier avec n et e. n = p*q, et avec p et q, on peut tout déterminer, dont d, la clé de déchiffrement.

Le principe du RSA est qu'avec des nombres premiers p et q suffisamment grands, on ne peut pas factoriser n en un temps raisonnable, et donc déterminer p et q. 

Or là, n semble suffisement petit pour que cela soit possible. On va donc essayer. 

Grâce à [Dcode](https://www.dcode.fr/decomposition-nombres-premiers), on obtient : 

- p = 32317006071311007300714876688669951960444102669715484032130345427524655138867890893197201411522913463688717960921898019494119559150490921095088152386448283120630877367300996091750197750389652106796057638384067568276792218642619756161838094338476170470581645852036305042887575891541065808607552399123930385521914333389668342420684974786564569494856176035326322058077805659331026192708460314150258592864177116725943603718461857357598351152301645904403697613233287231227125684710820209725157101726931323469678542580656697935045997268352998638215525166389437335543602135433229604645318478604952148193555853611059596265937
- q = 32317006071311007300714876688669951960444102669715484032130345427524655138867890893197201411522913463688717960921898019494119559150490921095088152386448283120630877367300996091750197750389652106796057638384067568276792218642619756161838094338476170470581645852036305042887575891541065808607552399123930385521914333389668342420684974786564569494856176035326322058077805659331026192708460314150258592864177116725943603718461857357598351152301645904403697613233287231227125684710820209725157101726931323469678542580656697935045997268352998638215525166389437335543602135433229604645318478604952148193555853628651782312709

On va maintenant déchiffrer le message M.

![firefox_BPqldYYucy](https://user-images.githubusercontent.com/58084848/206912110-a0ef96a9-bea4-449f-a639-7e894333815e.png)

On obtient : Bravo jeune cryptologue en herbe, le flag est CYBN{d0nt_r0ll_y0ur_0wn_crypt0_dammit!!}

Et voilà le flag UwU !


### Pourquoi diable 65537 ?

Le nombre 65537 est souvent utilisé dans le protocole RSA pour plusieurs raisons. Tout d'abord, il est relativement facile à manipuler mathématiquement, ce qui le rend idéal pour une utilisation dans les calculs cryptographiques. De plus, il est connu pour avoir des propriétés qui le rendent particulièrement bien adapté pour la cryptographie.

En particulier, le nombre 65537 est un nombre premier, ce qui signifie qu'il n'est divisible que par 1 et lui-même. Cela le rend idéal pour la cryptographie, car il est difficile de déterminer les propriétés mathématiques d'un nombre premier. En outre, 65537 est un nombre de Fermat, ce qui signifie qu'il satisfait à l'équation a^(p-1) = 1 (mod p), où p est un nombre premier. Cette propriété est utile pour les calculs cryptographiques.

Enfin, le choix de 65537 comme nombre dans le protocole RSA est également motivé par des considérations de sécurité. Comme il s'agit d'un nombre assez grand, il peut fournir une sécurité suffisante dans de nombreuses situations. Cependant, il est important de noter que la sécurité offerte par 65537 peut être compromise si d'autres facteurs ne sont pas pris en compte, comme le choix des autres nombres utilisés dans le protocole RSA.

