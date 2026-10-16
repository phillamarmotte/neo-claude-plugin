# Plugin Claude Code pour iparapheur Neo

Marketplace Claude Code qui contient le plugin **`iparapheur`** : il branche Claude Code sur le
serveur MCP d'une instance iparapheur Neo et ajoute quelques skills pour s'en servir.

## Ce que fait le plugin

- **Serveur MCP `neo`** : `https://<votre instance>/mcp`, authentifié par votre jeton personnel.
  L'assistant agit en votre nom, avec vos droits et rien de plus. Il ne signe et ne cachette jamais.
- **Skills** (appelées d'elles-mêmes selon la demande, ou à la main) :

  | Commande | Usage |
  | --- | --- |
  | `/iparapheur:a-traiter` | « Qu'ai-je à traiter ? » : bannettes triées par signaux, « À traiter » séparé de « En supervision » |
  | `/iparapheur:rechercher` | recherche multicritère, sélection ou filtre enregistré à rouvrir dans l'application |
  | `/iparapheur:agir` | viser, rejeter, transférer, avis, annoter, toujours confirmé dossier par dossier (ou par lot explicite) |
  | `/iparapheur:absence` | déclarer, consulter ou retirer une absence avec délégation |
  | `/iparapheur:configurer` | activation, jeton, portées, certificats, dépannage |

## Prérequis

1. **Le serveur MCP est activé pour votre structure** (éteint par défaut) : un administrateur l'ouvre
   dans *Administration › Configuration › Assistant conversationnel › Serveur MCP*.
2. **Un jeton d'API** : *Préférences › Mes jetons d'API › Créer*, portée **Lecture**, plus
   **Actions sur les dossiers** pour viser ou rejeter. Le secret `ipn_…` n'est affiché qu'une fois.

## Installation

Dans Claude Code :

```
/plugin marketplace add phillamarmotte/neo-claude-plugin
/plugin install iparapheur@iparapheur-neo
```

À l'activation, Claude Code demande :

- **Adresse de l'instance** : par exemple `https://parapheur.exemple.fr` (sans `/mcp`, sans barre finale) ;
- **Jeton d'API** : votre `ipn_…`, rangé dans le trousseau du système.

Pour les modifier ensuite : `/plugin` › *Installed* › `iparapheur` › *Configure*. Vérifiez la
connexion avec `/mcp`.

### Instance avec un certificat interne

Si l'instance présente un certificat émis par une autorité interne, lancez Claude Code avec
l'autorité :

```bash
NODE_EXTRA_CA_CERTS=/chemin/vers/ac.pem claude
```

ou posez `NODE_EXTRA_CA_CERTS` dans `env` de `~/.claude/settings.json`. La variable n'est lue qu'au
démarrage, et le fichier doit être une autorité (`CA:TRUE`), pas le certificat du serveur.

## Mise à jour

```
/plugin marketplace update iparapheur-neo
```
