
## Liste de passerelles publiques

* Demandez sur un des salons suivants: #mautrix_yunohost:matrix.fdn.fr or #googlechat:maunium.net

## Usages de la passerelle
** Notez que plusieurs comptes Google Chat et Matrix peuvent être relayés, chaque compte Google Chat connecté a son propre Salon d'Administration. Si plusieurs utilisateur.ice.s du Robot sont dans un même groupe Google Chat, seul un Salon Matrix sera créé par la passerelle. **

### Relayer TOUTES les conversations entre UN compte Google Chat et UN compte Matrix
* Prérequis : votre compte Matrix ou le serveur sur lequel il est hébergé doit être autorisé dans la configuration de la passerelle (voir ci-dessous)
* Invitez le Robot (par défaut @googlechatbot:synapse.votredomaine) à une nouvelle conversation.
* Ce nouveau salon d'administration du Robot Mautrix-Google Chat est appelé "Administration Room".
* Envoyez ``help`` au Robot dans le "Administration Room" pour une liste des commandes d'administration de la passerelle.
Voir aussi [upstream wiki Authentication page](https://docs.mau.fi/bridges/python/googlechat/authentication.html)

#### Relier la passerelle comme un appareil secondaire
* Tapez ``!gc link``
* Ouvrez l'application Google Chat de votre appareil principal
* Ouvrez Paramètres => Appareils reliés => + => filmer le QR
* Par défaut, seules les conversations avec des messages très récents seront mises-en-miroir
* Acceptez les invitations aux salons

#### Enregistrer la passerelle comme appareil principal
* Tapez ``!gc register <phone>``, où ``<phone>`` est votre numéro de téléphone au format international sans espace, p.ex. ``!gc register +33612345678``
* Répondez dans le salon d'administration avec le code de vérification reçu par SMS.
* Définissez une nom de profil ``!gc set-profile-name <name>``

### Robot-Relai "Relaybot": Relayer les conversations de TOUS les comptes Matrix et TOUS les comptes Google Chat présents dans UN groupe/salon
* Pas implémenté pour l'instant

## Configuration de la passerelle

La passerelle est [configurée avec les paramètres standards adaptés pour votre YunoHost et l'instance Matrix-Synapse sélectionnée](https://github.com/YunoHost-Apps/mautrix_googlechat_ynh/blob/master/conf/config.yaml). Vous pouvez par exemple ajouter des administrateurs et utilisateurs du Robot autorisés en modifiant le fichier de configuration par liaison SSH: 
``` sudo nano /opt/yunohost/mautrix_googlechat/config.yaml```
puis en redémarrant le service: 
``` sudo yunohost service restart mautrix_googlechat```

## Documentation

 * Documentation officielle "Mautrix-Google Chat": https://docs.mau.fi/bridges/python/googlechat/index.html
 * Salon Matrix sur les Passerelles dans Yunohost): #mautrix_yunohost:matrix.fdn.fr
 * Salon Matrix (application principale): #googlechat:maunium.net
Si vous devez téléverser vos fichiers log quelque-part, soyez avertis qu'ils contiennent des informations sur vos contacts et vos numéros de téléphone. Effacez-les avec 
``| sed -r 's/[0-9]{10,}/📞/g' ``
 * Documentation YunoHost: Si une documentation spécifique est nécessaire, n'hésitez pas à contribuer.

## Caractéristiques spécifiques YunoHost

#### Support multi-comptes
* Les utilisateur.ice.s du Robot ne sont pas liés aux comptes Yunohost. N'importe quel compte Matrix ou serveur Synapse autorisés dans la configuration de la passerelle peut inviter/utiliser le Robot. 
* Le robot Google Chat est un utilisateur Matrix-Synapse local, mais accessible via la fédération (Synapse public ou privé).
* Plusieurs comptes Google Chat et Matrix peuvent être liés avec une seule passerelle, chaque compte a son propre salon d'administration. 
* Si plusieurs utilisateur.ice.s du Robot sont dans un même groupe Google Chat, seul un Salon Matrix sera créé par la passerelle. Autrement dit, la passerelle construit un seul miroir du réseau de discussion existant sur Google Chat (utilisateurs et salons).
* Voir https://github.com/YunoHost-Apps/synapse_ynh#multi-users-support

#### Support multi-instance

* L'installation multi-instance devrait fonctionner. Plusieurs instances de passerelles pourraient être installées pour une instance de Matrix-Synapse. Cela permet à un compte matrix de se relier à plusieurs comptes Google Chat. 
* Plusieurs instances de passerelles pourraient être installées pour que chaque instance de Matrix-Synapse puisse en bénéficier. Mais une passerelle peut être utilisée par les comptes de plusieurs instances Matrix-Synapse.

## Limitations

* Les appels Audio/Video ne sont pas relayés. Seule une notification apparait. 
