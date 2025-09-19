# Comment diagnostiquer un problème réseau

#### Etape 1 - Récupérer les informations du réseau
On commence par récupérer les informations de notre réseau :

```bash
ipconfig
```

**Résultat**
```
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::d22f:e77c:bee7:5eaf%19
   Adresse IPv4. . . . . . . . . . . . . .: 10.21.137.37
   Masque de sous-réseau. . . . . . . . . : 255.255.0.0
   Passerelle par défaut. . . . . . . . . : 10.21.254.254
```

#### Etape 2 - Ping l'adresse IP du Router
L'adresse IP du router correspond à la ligne `Passerelle par défaut`, donc dans notre cas `10.21.254.254`.

Puis faire une requête `ping`:
```bash
ping 10.21.254.254
```

**Résultat**
```
Envoi d’une requête 'Ping'  10.21.254.254 avec 32 octets de données :
Réponse de 10.21.254.254 : octets=32 temps=2 ms TTL=64
Réponse de 10.21.254.254 : octets=32 temps=2 ms TTL=64
Réponse de 10.21.254.254 : octets=32 temps=15 ms TTL=64
Réponse de 10.21.254.254 : octets=32 temps=7 ms TTL=64

Statistiques Ping pour 10.21.254.254:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 2ms, Maximum = 15ms, Moyenne = 6ms
```

**Conclusion**
On reçoit une réponse à nos requêtes, donc on arrive à contacter le Router.

#### Etape 3 - Ping le serveur DNS
Maintenant qu'on arrive à contacter notre Router, il faut réussir à contacter un serveur DNS `8.8.8.8` pour celui de Google, ou `1.1.1.1` pour celui de Cloudfare :

```bash
ping 1.1.1.1
```

**Résultat**
```
Envoi d’une requête 'Ping'  1.1.1.1 avec 32 octets de données :
Réponse de 1.1.1.1 : octets=32 temps=14 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=4 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=13 ms TTL=57
Réponse de 1.1.1.1 : octets=32 temps=16 ms TTL=57

Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 4ms, Maximum = 16ms, Moyenne = 11ms
```

**Conclusion**
On peut également contacter le serveur DNS.

#### Etape 4 (Optionnel) - Si on a encore un problème pour contacter un site web
Si on a encore un problème pour contacter un site web alors que notre voisin y arrive, peut-être que le problème vient du cache DNS.

**Comment vider son cache ?**
```powershell
ipconfig /flushdns
```

Cette commande, si elle réussit on devrait avoir :
```
Configuration IP de Windows

Cache de résolution DNS vidé.
```
