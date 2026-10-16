---
name: absence
description: Déclare, consulte ou retire une absence dans iparapheur Neo, avec délégation des dossiers à un autre bureau. À utiliser quand l'utilisateur dit « je suis en congé du 3 au 14 », « délègue mon bureau à Martine pendant mon absence », « quelles sont mes absences ? », « annule mon absence ».
argument-hint: "[dates et bureau suppléant]"
---

# Absences

Demande : $ARGUMENTS

1. `contexte_lister` pour la structure et les bureaux de l'utilisateur. S'il en a plusieurs et
   que la demande ne précise pas lequel s'absente, demandez.
2. `absence_lister` pour voir les absences existantes et éviter un doublon ou un chevauchement.
3. Le bureau suppléant est souvent nommé par une personne ou un service : trouvez-le avec
   `bureau_lister` ; plusieurs bureaux portent ce nom, demandez lequel.
4. Récapitulez avant d'agir : bureau absent, suppléant, date de début et de fin (dates
   `AAAA-MM-JJ`, interprétées dans le fuseau de la structure), périmètre éventuel. Attendez
   l'accord explicite.
5. `absence_declarer` (ou `absence_retirer` pour annuler), puis confirmez ce que le serveur a
   enregistré.

Pendant l'absence, les dossiers du bureau arrivent dans la bannette `DELEGUES` du suppléant.
