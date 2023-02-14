							----- TP02 -----

Dans cet exercice, vous devez donner le nombre de logements se situant dans la commune de Pibrac.















Résultat attendu : 

![Résultat](https://github.com/FlorentIZO/FORENSIC_TP_IZORCHE_FLORENT/blob/main/TP02/IMG/TP02.PNG "Résultat")

Les commandes grep, cut et awk doivent être utilisées pour obtenir le résultat attendu.

awk -F ";" 'tolower($9) == "pibrac" {sum += $11} END {print sum}' liste.csv

La commande récupère les lignes dont la colonne 9 (nom_commune) est égale à pibrac, la commande ignore la casse avec la variable tolower.
Elle affiche ensuite la somme des valeurs de la colonne 11 (nombre_de_logements) des lignes précédemment récupérées.
