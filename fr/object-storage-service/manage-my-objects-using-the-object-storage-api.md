---
title: "Gérer mes objets avec l'API de Stockage Objet"
slug: gerer-mes-objets-avec-api-de-stockage-objet
---


Cette article décrit comment utiliser l'API de OpenStack SWIFT pour la gestion de vos objets. Pour effectuer ces appels API, vous devez au préalables avoir obtenu votre authentifiant d'API. [Cette article](https://app.elev.io/articles/edit/4982#) vous expliquera comment y parvenir.



### Jetons

Tout d'abord, vous devez obtenir un jeton (token) provenant de l'autorité d'authentification.

#### POST/v2.0/tokens

##### Authentification

S'authentifier et générer un jeton.

L'API d'identité est un service web REST. Il est le point d'entrée pour le service de Stockage Objet.

**Codes de réponse normale :** 200, 203
**Codes de réponse en erreur :** identityFault (400, 500, …), userDisabled (403), badRequest (400), unauthorized (401), forbidden (403), badMethod (405), overLimit (413), serviceUnavailable (503), itemNotFound (404)

**Donnée JSON :**

```
{
    "auth": {
        "tenantName": "warrenton-Medias",
        "passwordCredentials": {
            "username": "warrenton-user",
            "password": "GhJdhw72pc927"
        }
    }
}
```

**Requête CURL :**

```
curl -X POST -i \
 -H "Content-Type: application/json" \
 -d @test.json \
 https://auth-east.cloud.ca/v2.0/tokens ; echo
```

**Réponse CURL :**

```
HTTP/1.1 200 OK
Vary: X-Auth-Token
X-Distribution: Ubuntu
Content-Type: application/json
Content-Length: 1238
Date: Mon, 16 Mar 2015 23:01:50 GMT
{
   "access":{
      "token":{
         "issued_at":"2015-03-16T23:01:50.129423",
         "expires":"2015-03-17T00:01:50Z",
    -->  "id":"c7436b7a2f1a4c1fb58606fa9b4b0816", <--
         "tenant":{
            "description":"",
            "enabled":true,
            "id":"d6429737322249ac9c60bc5bb659fa28",
            "name":“demo"
         },
         "audit_ids":[
            "mIa_TZf-RX6W5jwEPMR2cg"
         ]
      },
      ... (sortie tronquée)
```


### Récipients

Cette section vous indiquera comment intéragir avec les récipients.

#### PUT/v1/{account}/{bucket}

##### Créer un récipient
Créer un récipient (ou un Bucket)

Vous n'avez pas besoin de vérifier si le récipient existe déja avant de faire une opération PUT car cette opération est idempotente: cela va créer le récipient ou le mettre à jour dépendant du cas.

**Requête CURL :**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads \
  -X PUT -H "Content-Length: 0" -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 201 Created
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx7f6b7fa09bc2443a94df0-0052d58b56
Date: Mon, 16 Mar 2015 23:01:50 GMT
```

#### GET/v1/{account}/{bucket}

##### Détails d'un récipient ou liste d'objets

Voir les détails d'un récipient spécifique et la liste d'objets.

Spécifiez un paramètre de requête pour filtrer la liste et retourner un sous-ensemble d'objet. Sans paramètre, le système va retourner la liste complète des objets d'un récipient, jusqu'à concurrence de 10 000 items. Le maximum de 10 000 est configurable.

**Code de réponse normale :** 200,204
Code de réponse en erreur :**** NotFound(404)

**Requête CURL :**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/Pictures \
  -X GET -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 200 OK
Content-Length: 179
X-Container-Object-Count: 7
Accept-Ranges: bytes
X-Storage-Policy: Policy-0
X-Container-Bytes-Used: 1661152
X-Timestamp: 1424957110.29889
Content-Type: text/plain; charset=utf-8
X-Trans-Id: tx7c235b898f534704a8505-0055084060
Date: Tue, 17 Mar 2015 14:55:28 GMT
Apache CloudStack Logo With Cloud Monkey.ai
cloudops_logo.eps
cloudops_logo_150.png
cloudops_logo_300.png
cloudops_logo_cloud-01.png
cloudops_logo_square.jpg
firefighter-tarp.jpg
```

#### DELETE/v1/{account}/{bucket}

##### Supprimer un récipient

Supprimer un récipient vide.

Cette opération échoue sauf si le récipient est vide. Un récipient est vide lorsqu'il ne contient plus aucun objet.

**Code de réponse normale :** 204
**Code de réponse en erreur :** NotFound(404), Conflict(209)

**Requête CURL :**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads \
  -X DELETE -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 204 No Content
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx7f6b7fa09bc2443a94df0-0052d58b56
Date: Mon, 16 Mar 2015 23:01:50 GMT
```

### Objects

Cette section présente comment intéragir avec les objets.

#### PUT/v1/{account}/{bucket}/{object}

##### Créer ou remplacer un objet

Créer un nouvel objet avec des données et métadonnées spécifiques.

L'opération PUT créer toujours un nouvel objet. Si vous utilisez cette opération sur un objet existant, vous remplacerez complètement l'objet existant et ses métadonnées. Conséquemment, cette opération va retourner un code 201. Si vous utilisez cette opération pour copier un objet de manifeste, le nouvel objet sera un objet normal et non une copie du manifeste. Vous ne pouvez pas copier des objets plus gros que 5GB sans utiliser la fonctionnalité de multi-partition.

**Code de réponse normale :** 201
**Code de réponse en erreur :** timeout (408), lengthRequired (411), unprocessableEntity (422)

**Requête CURL:**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/ \
  -T myobject.txt \
  -X PUT \
  -H "Content-Type: text/html"\
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 100 Continue
HTTP/1.1 201 Created
Last-Modified: Tue, 17 Mar 2015 15:08:21 GMT
Content-Length: 0
Etag: d95679752134a2d9eb61dbd7b91c4bcc
Content-Type: text/html
X-Trans-Id: tx02828f7e1367494488e6e-0055084364
Date: Tue, 17 Mar 2015 15:08:20 GMT
```

#### GET/v1/{account}/{bucket}/{object}

##### Obtenir contenu d'un objet

Télécharger le contenu d'un objet et obtention des métadonnées.

Cette opération retourne les métadonnées dans les en-têtes et le contenu de l'objet dans le corp de la réponse. Si c'est un objet large, le corp de la réponse va contenir une concaténation du contenu de chaque segments. Pour obtenir le manifeste, utilisez le paramétre multipart-manifest.

**Codes de réponse normale :** 200
**Codes de réponse en erreur :** NotFound (404)

**Requête CURL :**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/myobject.txt \
  -X GET \
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 200 OK
Content-Length: 12
Accept-Ranges: bytes
Last-Modified: Tue, 17 Mar 2015 15:16:39 GMT
Etag: 9e8bde8ad2d571a03e1c95d0c2ead964
X-Timestamp: 1426605398.84480
Content-Type: text/html
X-Trans-Id: tx2197e9ed2bfd4e458d239-0055084567
Date: Tue, 17 Mar 2015 15:16:55 GMT
Hello Dear!
```

#### DELETE/v1/{account}/{bucket}/{object}

##### Supprimer un objet

Supprimer un objet indéfiniment d'un récipient.

Vous pouvez utiliser la méthode COPY pour copier un objet vers un nouvel emplacement. Ensuite, utilisez ensuite la méthode DELETE pour supprimer l'objet original. La supression de l'objet arrive immédiatement au moment de la requête. Ce qui veut dire que toutes les opérations GET, HEAD, POST, ou DELETE vont retourner une erreur 404 Not Found. Pour les manifests statiques de large objet, vous pouvez ajouter le paramètre ?multipart-manifest=delete à votre requête. Cette opération supprime les segment d'objet et si toutes les suppressions sont un succès, l'opération va aussi supprimer le manifeste.

**Codes de réponse normale :** 204
**Codes de réponse en erreur :** 400, 500, ...

**Requête CURL :**

```
curl -i https://objects-east.cloud.ca/v1/d6429737322249ac9c60bc5bb629fe32/uploads/myobject.txt \
  -X DELETE \
  -H "X-Auth-Token: c7436b7a2f1a4c1fb58606fa9b4b0816"
```

**Réponse CURL :**

```
HTTP/1.1 204 No Content
Content-Length: 0
Content-Type: text/html; charset=UTF-8
X-Trans-Id: tx6fdb2d8ca1334f63b95f9-0055084c04
Date: Tue, 17 Mar 2015 15:45:08 GMT
```

### Plus d'information?

Il existe d'autres appels API possibles. Veuillez visiter la page officielle de OpenStack Swift disponible à cette adresse pour tous les détails.
