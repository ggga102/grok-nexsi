# NEXSI — Demo PWA v1.1

Application compagnon des **Étudiants en Soins Infirmiers (ESI)** de France.

> **Cahier des charges / mémoire produit** : [`docs/NEXSI_Vision_produit_v1.md`](docs/NEXSI_Vision_produit_v1.md)

## Live demo

Déployer sur Vercel (static) → pointer la racine du repo.

## Features (demo)

| Zone | Contenu |
|------|---------|
| **Accueil** | Priorités (max 3), évaluations, tâches, quick actions, tip Drive |
| **Fiches** | Perso / Groupe / Bibliothèque, CRUD documents |
| **Terrain** | Stage simulé, journal anonymisé, objectifs, checklist fournitures |
| **Soins** | Catalogue + carnet de gestes (6 statuts), calculateur entraînement |
| **IA** | FAB chat mock (APP, priorités, stage, pharmaco) |
| **Connecteurs** | Google Drive (coffre) + ENT/MyKomunoté (mock) |
| **Recherche** | Overlay global (soins, tâches, docs, évaluations) |
| **Réglages** | Profil, toggles, reset démo |
| **PWA** | Manifest, Service Worker, offline, install prompt |

## Stack

- Vanilla HTML / CSS / JS (zéro dépendance)
- localStorage
- PWA installable

## Lancer en local

```bash
python3 -m http.server 8080
# http://localhost:8080
```

## Principes (vision produit)

- Données de l'étudiant au centre (mode manuel complet)
- Max 3 priorités, un CTA par carte
- Pédagogique, jamais per-soin (hors dispositifs médicaux)
- Sync ENT = bonus, pas une dépendance

---

NEXSI — s'organiser pendant les 3 ans d'IFSI.
