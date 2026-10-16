# Sonotone sur Gno.land — état du projet (15 octobre 2026)

Jeu de mémoire musicale. Les joueurs se connectent avec leur wallet **Adena**,
choisissent un pseudo relié à leur adresse, et leurs records sont inscrits sur
la blockchain **Gno.land** (testnet Onyx).

```
sonotone/
├── index.html          ← le jeu complet (anglais, mode Mélomane, bouton PLAY, bouton Stop)
├── deploy.html         ← page pour déployer le contrat v2 avec Adena
├── realm2/
│   └── sonotone2.gno   ← contrat v2 (2 classements : Classic + Mélomane) — À DÉPLOYER
├── realm/              ← contrat v1 (archive, déjà déployé, n'est plus utilisé par le jeu)
│   ├── sonotone.gno
│   └── gnomod.toml
└── LISEZMOI.md
```

## Réglages

| | |
|---|---|
| Réseau | testnet **Onyx** (`onyx-1`) — RPC `https://rpc.onyx.testnets.gno.land` |
| Faucet (GNOT de test) | https://onyx.testnets.gno.land/faucet |
| Ton adresse | `g18nke2hpu3zue0da9yudzxeugfyxuk3edjj4w79` |
| Contrat v1 (en ligne) | `gno.land/r/g18nke2hpu3zue0da9yudzxeugfyxuk3edjj4w79/sonotone` |
| Contrat v2 (utilisé par le jeu) | `gno.land/r/g18nke2hpu3zue0da9yudzxeugfyxuk3edjj4w79/sonotone2` |

## Ce que fait le jeu

- Accueil : « Connect my wallet » ou « Play without wallet ».
- Première connexion : choix du pseudo (3–20 caractères : lettres sans accent,
  chiffres, `_`, `-`) → transaction `Register`.
- Ensuite : reconnexion automatique, même après « Play Again ».
- Fin de partie (vies perdues, temps écoulé ou bouton **⏹ Stop**) : une
  transaction n'est demandée **que pour un nouveau record**.
- Deux classements : **Classic** et **Mélomane** (12 notes avec dièses).
- Le mode Mélomane se débloque à **135 points en Classic** — vérifié par le
  contrat lui-même (impossible de tricher via le navigateur).

## Reprendre : les étapes

1. Installe **VS Code** + l'extension **Live Server**, et l'extension **Adena**
   dans ton navigateur (restaure ton compte avec ta phrase secrète :
   ton adresse `g1nmhpk…` et ton contrat v1 sont toujours sur la blockchain).
2. Dans Adena, choisis le réseau **Onyx**. Si ton solde est vide, passe par le faucet.
3. Ouvre `deploy.html` avec Live Server → vérifie les deux ✔ → « Déployer avec Adena ».
4. Attends que la page du contrat ne soit plus « Not Yet Enabled » (approbation
   automatique d'Onyx, quelques minutes) :
   https://onyx.testnets.gno.land/r/g18nke2hpu3zue0da9yudzxeugfyxuk3edjj4w79/sonotone2
5. Ouvre `index.html` avec Live Server, connecte ton wallet, réinscris
   ton pseudo (nouveau contrat = nouveau classement) et joue.

## ⚠️ Sauvegarde

Mets ce dossier sur **GitHub** (dépôt privé ou public) et pousse après chaque
modification : c'est ta sauvegarde, et GitHub Pages pourra héberger le jeu.

## À savoir avant le mainnet

- Chaque inscription et chaque record coûte un peu de GNOT au joueur ; sur le
  mainnet il n'y a pas de faucet.
- Un contrat déployé ne se modifie pas : une nouvelle version = un nouveau
  chemin (`sonotone3`…) et on met à jour `GNO.realmPath` dans le jeu.
- Le score vient du navigateur : un joueur malin pourrait envoyer un faux
  score. Acceptable pour un jeu « fun », pas pour des récompenses de valeur.
