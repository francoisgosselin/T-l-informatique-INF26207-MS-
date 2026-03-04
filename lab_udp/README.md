# Labo UDP
## OLYMPIO MARIEN

## Partie 2 - Question : pourquoi len(s) peut etre different de len(b) ?

En Python, len(s) compte le nombre de caracteres Unicode  **utf-8 pour être précis** , tandis que len(b)
compte le nombre d'octets. En UTF-8, certains caracteres comme les accents (e, a, c),
les lettres speciales (o, -) ou les emojis sont encodes sur 2, 3 ou 4 octets.
Ainsi, un seul caractere peut occuper plusieurs octets, ce qui fait que len(b) >= len(s)
des qu'il y a des caracteres non-ASCII.

## Partie 3 - Question : pourquoi les sockets envoient-elles des bytes plutot que des str ?

Les reseaux transportent des donnees binaires brutes (octets), sans notion de texte.
De plus, une meme chaine peut avoir des representations binaires differentes selon
l'encodage choisi (UTF-8, Latin-1, UTF-16). Envoyer des bytes force l'application
a choisir explicitement l'encodage, garantissant que l'emetteur et le recepteur
interpretent les memes octets de la meme facon.

## Partie 4 - Question : quelle difference entre digest() et hexdigest() ?

digest() retourne le hash sous forme binaire brute (bytes), soit 32 octets
pour SHA-256. C'est compact et ideal pour la transmission reseau.
hexdigest() retourne la meme valeur encodee en hexadecimal lisible (str),
soit 64 caracteres ASCII. C'est pratique pour l'affichage ou les comparaisons textuelles.

## Partie 7 - Question : a quoi sert un nonce dans un echange reseau ?

Un nonce (number used once) est une valeur aleatoire generee a chaque envoi.
Il garantit l'unicite de chaque message : deux envois du meme texte produisent
deux payloads differents. Cela protege contre les attaques par rejeu (replay attacks),
ou un attaquant intercepterait un message valide pour le renvoyer plus tard.
Le serveur peut detecter et rejeter un nonce deja utilise.
