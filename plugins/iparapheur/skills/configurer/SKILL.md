---
name: configurer
description: Aide à brancher et dépanner le plugin iparapheur Neo (activation du serveur MCP dans la structure, jeton d'API et portées, adresse de l'instance, certificat, erreurs 401 ou rôle manquant). À utiliser quand les outils neo n'apparaissent pas, échouent, ou quand l'utilisateur demande comment configurer l'assistant iparapheur.
---

# Configurer le plugin iparapheur

Le plugin déclare un serveur MCP HTTP `neo` sur `<adresse de l'instance>/mcp`, authentifié par le
jeton personnel de l'utilisateur. L'adresse et le jeton sont demandés à l'activation du plugin ; on
les modifie depuis `/plugin` (onglet *Installed*, plugin `iparapheur`, *Configure*). Le jeton est
rangé dans le trousseau du système, pas dans un fichier.

## Vérifier dans l'ordre

1. **Le serveur répond-il ?** `/mcp` doit montrer `neo` connecté. Sinon, voir plus bas.
2. **Le serveur est-il activé pour la structure ?** Il est éteint par défaut. Un administrateur
   l'ouvre dans *Administration › Configuration*, section *Assistant conversationnel*, élément
   *Serveur MCP* (clé `assistant_mcp`). Sans activation, la structure n'apparaît pas ou les outils
   refusent.
3. **Le jeton** : *Préférences › Mes jetons d'API › Créer*. Le secret (`ipn_…`) n'est affiché
   qu'une fois. Portées :
   - **Lecture** : consulter, rechercher, sélections et filtres ;
   - **Actions sur les dossiers** : annoter, viser, rejeter, transférer, avis.
   Les portées ne s'impliquent pas : un assistant qui agit a besoin des deux. Elles restreignent
   sans rien accorder : le serveur n'en fait jamais plus que l'utilisateur à l'écran.

## Erreurs courantes

| Symptôme | Cause probable |
| --- | --- |
| `401` | jeton absent, faux, révoqué ou expiré : en recréer un et reconfigurer le plugin |
| erreur citant `ROLE_API_LECTURE` / `ROLE_API_ACTION` | portée manquante sur le jeton |
| structure absente de `contexte_lister` | serveur MCP non activé pour cette structure, ou utilisateur non membre |
| `neo` en échec dans `/mcp`, erreur de certificat | instance avec certificat interne ou autosigné : lancer Claude Code avec `NODE_EXTRA_CA_CERTS=<chemin de l'AC>` (variable lue au démarrage seulement ; une AC doit être `CA:TRUE`) |
| délai dépassé sur un nom en `.local` (macOS) | résolution mDNS IPv6 lente : ajouter aussi `::1 <nom>` dans `/etc/hosts` |

Les outils `aide_lister` et `aide_lire` donnent accès à l'aide en ligne de l'application : utilisez-les
pour les questions de fonctionnement d'iparapheur Neo plutôt que de supposer.
