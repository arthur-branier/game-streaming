[README-game-streaming.md](https://github.com/user-attachments/files/25813419/README-game-streaming.md)
# Game Streaming — Sunshine + Moonlight sur Linux

Mise en place d'un setup de game streaming depuis mon PC sous EndeavourOS vers mon Samsung Galaxy Z Fold 6,
sur réseau local. Projet perso — juste pour voir si c'était faisable et m'amuser un peu.

> La latence est correcte pour un usage casual, quelques déconnexions occasionnelles,
> mais rien de bloquant. C'est pas du niveau compétitif, mais ça fonctionne.

---

## Matériel

| Rôle | Appareil |
|---|---|
| Serveur (host) | ASUS TUF Gaming A17 — EndeavourOS |
| GPU | NVIDIA GeForce RTX 3050 Mobile |
| Client | Samsung Galaxy Z Fold 6 |
| Réseau | Wi-Fi local |

---

## Comment ça marche

**Sunshine** tourne sur le PC et capture le flux vidéo (encodage GPU via NVENC).
**Moonlight** tourne sur le téléphone et reçoit + décode ce flux.
Les deux communiquent sur le réseau local — pas besoin d'internet.

```
[PC Linux / Sunshine] ──── réseau local ────► [Galaxy Z Fold 6 / Moonlight]
      encodage NVENC                               décodage + affichage
```

---

## Installation

### Sunshine (serveur, côté PC)

Disponible sur AUR :

```bash
yay -S sunshine
```

Démarrage du service :

```bash
systemctl --user enable --now sunshine
```

L'interface de configuration est accessible via navigateur sur `https://localhost:47990`.

### Moonlight (client, côté téléphone)

Installé depuis le Play Store — Moonlight Game Streaming.

---

## Configuration

- Encoder : **NVENC** (NVIDIA) — meilleure qualité, encodage matériel
- Résolution / FPS : selon le jeu, ajusté depuis l'interface Moonlight
- Jeux streamés : bibliothèque Steam détectée automatiquement par Sunshine

---

## Ce que j'ai rencontré

- **Quelques déconnexions** ponctuelles — probablement liées au Wi-Fi, pas encore investigué
- **Latence** : correcte pour jouer casual, perceptible sur des jeux rapides
- Pas de problème majeur à la configuration initiale

---

## Ce que j'ai appris

- Comment fonctionne l'encodage vidéo matériel (NVENC) et pourquoi c'est important pour le streaming
- La différence entre encodage côté serveur et décodage côté client
- Que Linux peut tout à fait servir de plateforme de streaming gaming, même avec un GPU hybride
- Les bases du streaming réseau local — ports, protocoles RTP/RTSP

---

## État actuel

| Fonctionnalité | État |
|---|---|
| Streaming Steam | ✅ Fonctionnel |
| Encodage NVENC | ✅ Fonctionnel |
| Connexion Moonlight | ✅ Fonctionnel |
| Stabilité réseau | ⚠️ Quelques déconnexions occasionnelles |
