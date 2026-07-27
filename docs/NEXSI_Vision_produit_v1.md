# NEXSI — Vision produit v1

**Document de référence produit et architecture**  
Destiné à l’équipe de développement.  
Les diagrammes sont en Mermaid et se rendent nativement sur GitHub.

> **Périmètre design** : ce document ne définit aucune identité visuelle — ni couleurs, ni typographie, ni iconographie, ni thèmes, ni composants graphiques. L’identité visuelle sera conçue par l’équipe design, qui dispose d’une liberté créative totale. Toute mention d’interface décrit une **structure ou un comportement**, jamais une apparence.

---

## 1. Produit

### 1.1 Mission

**NEXSI** est l’application compagnon des Étudiants en Soins Infirmiers (ESI) de France.  
Sa mission tient en un mot : **s’organiser**.

Organiser sa journée, ses travaux, son stage, ses documents et sa progression pendant les trois années de formation.  
Les révisions, l’assistance IA et les outils de préparation servent ce but. Ils ne le remplacent pas.

Les données de l’étudiant sont au centre. Tout le reste (synchronisation ENT, sources externes, contacts, emploi) gravite autour de lui.

### 1.2 Public

Environ **104 000 à 106 000 ESI** en septembre 2026, répartis dans 337 IFSI.

| Promotion              | Estimation centrale | Fourchette          |
|------------------------|---------------------|---------------------|
| 1re année (2026-27)    | 39 000              | 37 500 – 40 500     |
| 2e année (2025-26)     | 33 200              | 32 000 – 34 500     |
| 3e année (2024-25)     | 31 000              | 29 500 – 32 500     |
| **Total**              | **≈ 103 200**       | **99 000 – 107 500**|

Deux référentiels coexistent :
- Compétences C1-C10 (arrêté 2009) pour les promotions déjà en cours.
- Domaines A à E et 13 compétences (arrêté du 20 février 2026) pour les promotions entrantes à partir de septembre 2026.

NEXSI prend en charge les deux.  
Le public est sous forte charge mentale. Réduire cette charge est une fonctionnalité centrale, pas un supplément.

### 1.3 Principes fondateurs

| Principe | Traduction concrète |
|----------|---------------------|
| **Les données de l’étudiant sont au centre** | L’application s’organise autour de ce que l’ESI saisit, photographie, importe ou synchronise. La synchronisation MyKomunoté (ou autre ENT) est un **bonus** très utile, pas un pilier. L’app fonctionne pleinement en mode manuel. |
| **Ouvert et personnalisable** | L’ESI peut créer, modifier, supprimer (CRUD) presque tout ce qui le concerne. NEXSI fournit un cadre, des classements et des outils, pas un contenu fermé. |
| **Réduction de la charge cognitive** | Jamais plus de 3 priorités affichées en même temps. Un seul appel à l’action par carte. Recherche d’abord. Progressive disclosure partout. |
| **Pédagogique, jamais per-soin** | NEXSI prépare et débriefe. Il ne s’utilise pas pendant le geste. Ce positionnement maintient l’application hors du champ des dispositifs médicaux. |
| **Honnêteté** | Pas de fausse capacité. Pas de pastille décorative. Les messages de sécurité et de confidentialité sont clairs, sobres et réalistes. |
| **Les données pour améliorer le produit** | NEXSI est une startup informatique. Les données saisies (hors données strictement personnelles et données patient) alimentent l’amélioration du produit, l’entraînement de l’IA et les analyses agrégées (par promo, par IFSI, etc.). C’est la valeur ajoutée. |

### 1.4 Périmètre

Quatre onglets :
1. **Accueil** — Planning, tâches, dossier IFSI
2. **Fiches** — Travaux personnels, travaux de groupe, bibliothèque
3. **Terrain** — Stage + emploi + catalogue des terrains
4. **Soins** — Catalogue des soins, carnet de gestes, protocoles, préparation

IA intégrée partout via Floating Action Button.  
Coffre Google Drive pour les données irremplaçables.  
PWA installable.

Hors périmètre produit (exclusions par conception) :
- Calcul de dose destiné à un patient réel
- Traitement de données de santé identifiables sur les serveurs NEXSI sans anonymisation préalable
- Publicité intrusive
- Vente de données nominatives

---

## 2. Vue d’ensemble du système

Voir diagramme Mermaid dans le document source complet.

À retenir :
- Les données de l’étudiant sont prioritaires.
- La synchronisation ENT est un accélérateur d’onboarding et de remplissage, pas une dépendance.
- Toute l’IA passe par le proxy serveur (Gemini 3.5 Flash Lite par défaut + possibilité BYOK).
- Les données strictement personnelles et les données patient anonymisées restent sous contrôle de l’étudiant.

---

## 3. Parcours d’entrée (onboarding)

Style conversationnel inspiré des meilleurs parcours modernes (rapide, naturel, humain, sans jargon).

1. Accroche simple
2. Connexion légère (Google recommandé pour le coffre Drive)
3. Première saisie guidée (année, planning photo/import)
4. Coffre Google Drive
5. Première utilité immédiate + invitation PWA

---

## 4. Les quatre onglets

### 4.1 Accueil — Centre de pilotage quotidien
Planning (aujourd’hui max 3 priorités, semaine, évaluations, horaires stage), Tâches, IFSI (dossier, promo, BDE).

### 4.2 Fiches — Espace travaux ouvert
Travaux personnels, travaux en groupe, bibliothèque. Classement par UE. Sources externes labellisées.

### 4.3 Terrain — Stage + emploi
Progression portfolio, journal de bord anonymisé, APP, compétences, préparation de stage, emploi, catalogue terrains.

### 4.4 Soins — Recherche d’abord
Catalogue, carnet de gestes (6 statuts), protocoles, calculateurs entraînement uniquement, bandeau d’avertissement permanent.

---

## 5. IA

FAB sur tous les écrans. Conseil rapide contextuel + chat complet. Gemini 3.5 Flash Lite + BYOK. Proxy serveur obligatoire.

---

## 6. Données & confidentialité

Journal, notes patient, docs personnels → local + coffre Drive. Anonymisation obligatoire. Le reste peut être côté serveur (agrégé).

---

## 7. Acquisition

1. Délégués de promo  2. Instagram/TikTok  3. FNESI  4. BDE d’IFSI

---

## 8. Modèle économique

Pas de vente de contenu aux étudiants. Monétisation : intérim/emploi, partenariats mutuelles/banques, B2B IFSI (long terme).

---

## 9. Stack technique (indicative)

Frontend React+TS+PWA · IndexedDB + coffre AES-GCM Drive · Backend Node · Proxy Gemini · Sync ENT optionnelle fail-safe.

---

## 10. Feuille de route

Phase actuelle : 4 onglets, onboarding, IA, coffre Drive, mode manuel, carnet de gestes, préparation stage, anonymisation.

Ensuite : notifications, groupes, native, partenariats emploi.

---

*Fin du document — NEXSI, Vision produit v1*

> **Note** : version condensée pour le dépôt. Le document source complet (avec diagrammes Mermaid détaillés) est conservé dans l’historique du projet.
