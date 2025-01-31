# TD Git : Gestion des tâches avec un scénario réaliste

## **Contexte**

Vous êtes une équipe de développement de 4 dévelopeur travaillant sur une application **"Gestion des tâches"**. Votre client demande :

1. Une **fonctionnalité d'ajout de tâches**.  
2. Une **fonctionnalité de suppression de tâches**.  

L'objectif est de collaborer efficacement en utilisant Git pour gérer le code source de ce projet.

---

## **Étapes du TD**

### 1. Initialisation

- Démarrez un nouveau projet Git pour l'application "Gestion des tâches".
- Créez un fichier `README.md` et ajoutez une description initiale.

### 2. Création des branches

- Suivez une stratégie de branches
  - Branche principale : `main`.
  - Branche de développement : `develop`.
  - Branche pour chaque fonctionnalité, par exemple `feature/ajout-taches`.

### 3. Développement des fonctionnalités

- Sur une branche dédiée, ajoutez la description de la fonctionnalité d'ajout de tâches dans le fichier `README.md`.
- Répétez pour la fonctionnalité de suppression de tâches sur une autre branche.

### 4. Fusion et intégration

- Fusionnez chaque branche de fonctionnalité dans `develop` après validation.
- Une fois toutes les fonctionnalités terminées, fusionnez `develop` dans `main` pour préparer une version stable.

---

## **Objectifs pédagogiques**

1. Comprendre l'importance des branches pour isoler le travail.
2. S'initier aux bonnes pratiques :
   - Messages de commit clairs.
   - Gestion collaborative.
   - Stratégie de fusion pour un code propre.
3. Résoudre des conflits si des modifications simultanées sont faites sur le même fichier.

---
