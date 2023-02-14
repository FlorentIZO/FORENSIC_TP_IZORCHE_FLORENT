----- RAPPORT D'ANALYSE DU SUPPORT EXTERNE  ----

Contexte :

Une clé USB suspecte a été identifiée à proximité du commissariat par un agent de police.
Il nous a été demandé d'analyser ce support amovible afin de déterminer si l'appareil était sans risque et ne comportait aucun fichier suspect.



Tests effectués  : 

Les analyses du périphérique ont été réalisés dans un environnement de test dédié et à partir d'une copie du support afin de garantir l'intégrité des données.


Après analyse du format du support (via la commande xxd), nous avons constaté que le format de l'image était sous MS-DOS, aussi appelé FAT.
Il s'agit d'un vieux format de disque peu utilisé à ce jour.
Il est possible que cette clé soit relativement agée.
![Format du disque](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP01/IMG/Format.PNG "Format du disque")


Après avoir pris compte des informations donnés ci-dessus :
Nous avons tenté de restaurer les fichiers de la clé USb :

Nous avons d'abord utilisé la commande testdisk pour tenter la récupération des fichiers mais les tests n'ont pas été concluants.
![alt text] (testdisk.png)

Toutefois, avec la commande PhotoRec, nous avons pu récupérer plusieurs fichiers contenu dans le support amovible.
Parmis ces fichiers, se trouvait deux fichiers nommés Hash.PNG, deux fihciers potentiellements dangereux. 
![alt text] (dossier.jpg)

Autre information  relevée :

Un formatage de la clé a été effectué le 10 Février 2023 à 21h51.


Conclusion : 

L'analyse du support nous a permis de constater que la clé est infectée par deux fichiers :
- f0016520.png
- f0040392.png
[Ces deux fichiers contiennent le flag attendu (bosch {1MAG3}.]
![alt text] (Hash.png)

Il est fortement déconseillé de connecter ce périphérique à un quelconque appareil.
Vous trouverez, ci joint au rapport d'analyse, les captures d'écran associées aux informations relevées lors du rapport.

Cordialement
Le laboraotire d'analyse 

