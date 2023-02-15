#							----- RAPPORT D'ANALYSE -----


##1 - Introduction :

L'entreprise bosch-cyber nous a contacté suite a une attaque informatique impactant son site Web.
Un individu a été en mesure d'installer des outils dangereux sur la machine ciblée.
Pour l'heure la machine n'est plus en production et est isolée.

Notre analyse s'est uniquement concentrée sur la machine touchée par l'attaque . 
Il s'agit d'un serveur Ubuntu 2.04.5.
Aucune donnée n'a été modifiée ou supprimée durant l'analyse.


##2 - Méthodologie : 


La commande "history" nous a permis de lister toutes les commandes exécutées préédemment.
![history](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP03/IMG/tp03-1.PNG "history")

Plusieures actions suspectes ont pu être identifiées : 


L'indiviu a contacté un serveur distant (138.66.89.12), possiblement l'un de ses serveurs.

L'individu a tenté de récupérer les mots de passe chiffrés des utilisateurs en ouvrant le fichier "shadow" du système linux. (Commande : cat /etc/shadow)
La tentative a échoué par manque de droit.


L'individu a programmé une tâche planifiée à partir de la commande "crontab -e", il a ensuite compressé le fichier dans une archive .zip et a stocké le mot de passe de cette archive dans le fichier /tmp/mypassword.
Enfin, il a déplacé son fichier d'exécution compressé vers le répertoire "/opt/leak", puis il a supprimé le fichier de mots de passe (/tmp/mypassword) du fichier compressé.


En ouvrant le fichier contrab, nous pouvons constater que la modificaiton a été apportée par l'adresse ip 138.66.89.12, l'adresse qu'il a lui même contacté précédemment.
Le port utilisé (4444) est souvent utilisé pour déployer un Malware nommé CrackDown, son utilisation est donc douteuse.


Tentative de récupération du mot de passe à partir du fichier /tmp/mypassword :

La commande grep -r /mypassword nous confirme qu'il ne reste aucune trace du fichier.
![grep](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP03/IMG/grep.PNG "grep")

Nous allons orienter notre grep vers l'ip récupérée precédemment avec la commande suivante : 

Nous ciblons le fichier access.log car il liste l'ensemble des accès Apache (via des reqûetes HTTP).
La requête récupère cible le mot "password" pour limiter la recherche. 
![password](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP03/IMG/password.PNG "passwword")
De cette façon, nous somme en mesure de récupérer le mot de passe de l'archive.

Il ne nous reste plus qu'à lire le contenu du fichier all_tools.txt contenu dans l'archive :
![unzip](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP03/IMG/unzip.PNG "unzip")


##3 - Résultats et conlusion de l'nanalyse : 

Un individu s'est connecté sur votre serveur est a programme un programme/outil.
Il a compressé son fichier et l'a protégé avec un mot de passe qu'il a stocké dans un second fichier.
Il a ensuite déplacé son archive dans un dossier qu'il a lui même créé (/opt/leak).
Enfin, il a supprimé le fichier contenant le mot de passe de l'archive. 

L'outil malveillant  a été déposé le Samedi 24 Janvier.
![date](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP03/IMG/date_att.PNG "date")

En parallèle, il a programmé une tâche planifiée qui exécute un fichier bash et envoie une réponse vers son serveur (138.66.89.12).

L'attaquant est certaienement parvenu à s'introduire par le biais du port 4444.
Il a profité de l'ouverture de ce port pour y introduire un cheval de troie.


##4 - Recommandations : 

Nous vous recommandons vivement de bloquer l'utilisation du port 4444.
En effet, ce port est souvent utilisé par des attaquants pour injecter des chevaux de Troie et autres Malwares.
Si ce n'est pas le cas, nous vous conseillons d'utiliser le protcole HTTPS et de bloquer toutes les requêtes HTTP.
Vous pouvez également forcer les authentification via SSL en utilisant des protocoles sécurisés (Privilégiez TLS 1.2).
 

##5 - Conclusion générale :

Ce rapport avait pour but d'identifier les causes et les conséquences de l'attaque informatique subie sur le serveur Web Apache.
L'analyse nous permet d'affirmer que l'attaquant s'est introduit sur le serveur par le biais d'un port réseau non sécurisé.
Il a ensuite déployé un cheval de troie et une tâche planifiée pour garder un contrôle régulier sur le serveur.

Des mesures correctives doivent être apportées, elles sont détaillées dans la quatrième partie de ce dossier.

Toutes les informations personelles recueillis dans ce rapport appartiennent à la société Bosch-cyber et ne doivent, en aucun cas être divulguées.
