---
marp: true
theme: 'default'
header: "MIAGE Aix-Marseille"
footer: "Travaux dirigés"
paginate: true
markdown.marp.enableHtml: true
---

# Partie 1 : DevOps (10h TD en 5 séances de 2h)

## TD DevOps 1 (2h) : Prise en Main de Git et CI basique

**Objectifs :**  

- Apprendre à utiliser Git pour la gestion de versions.  
- Mettre en place un pipeline CI minimal qui exécute des tests à chaque commit.

**Étapes :**  

1. **Création d’un dépôt GitHub :**  
   - Créez un compte GitHub (si ce n’est pas déjà fait).  
   - Créez un nouveau dépôt public ou privé.  
   - Clonez ce dépôt en local sur votre machine (commande `git clone [URL]`).

2. **Gestion des branches :**  
   - Créez une branche nommée `feature-td-miage`.  
   - Ajoutez un fichier `main.py` avec un simple code "Hello World".  
   - Commitez vos modifications (`git add`, `git commit`) et poussez-les vers GitHub (`git push`).

3. **Pull Requests (PR) :**  
   - Sur GitHub, créez une Pull Request de votre branche `feature-td-miage` vers `main`.  
   - Familiarisez-vous avec l’interface des PR, les commentaires, l’approbation.

4. **Pipeline CI basique (GitHub Actions ou GitLab CI) :**  
   - Dans le dépôt, ajoutez un fichier de configuration CI (par ex. `.github/workflows/ci.yml` pour GitHub Actions).  
   - Configurez une action qui s’exécute à chaque push et fait simplement un `echo "CI test running"`.  
   - Commitez et poussez votre workflow pour voir la CI s’activer.

À la fin de cette séance, vous devriez avoir un dépôt Git fonctionnel et un pipeline CI minimaliste.

---

### TD DevOps 2 (2h) : Intégration Continue Avancée avec Tests

**Objectifs :**  

- Ajouter des tests unitaires à un projet.  
- Configurer la CI pour exécuter les tests automatiquement.

**Étapes :**  

1. **Ajout de tests unitaires :**  
   - Dans votre projet (par exemple, un projet Python), créez un répertoire `tests`.  
   - Ajoutez un fichier `test_main.py` qui contient un test simple (ex. utiliser `pytest` ou `unittest` pour vérifier qu’une fonction retourne le résultat attendu).  
   - Exécutez les tests en local (`pytest`).

2. **Intégration des tests dans la CI :**  
   - Modifiez votre fichier CI (`ci.yml`) pour installer les dépendances (ex. `pip install pytest`) et exécuter les tests (`pytest`).  
   - Commitez et poussez. Vérifiez que la CI s’exécute sur GitHub/GitLab et que les tests passent.  
   - Introduisez une petite erreur dans le code puis poussez à nouveau pour observer la CI échouer.

3. **Qualité du code :**  
   - Installez un outil de linting (ex. `flake8` pour Python) et intégrez-le dans le pipeline.  
   - Assurez-vous que la CI échoue si le style de code ne respecte pas les règles.

À la fin de cette séance, vous aurez un pipeline CI qui exécute automatiquement les tests et vérifie la qualité du code.

### TD DevOps 3 (2h) : Déploiement Continu (CD) et Conteneurisation

**Objectifs :**  

- Créer une image Docker de l’application.  
- Intégrer la création et le push d’image Docker dans le pipeline CI/CD.

**Étapes :**  

1. **Dockerisation de l’application :**  
   - Créez un `Dockerfile` à la racine du projet.  
   - Spécifiez l’image de base (ex. `python:3.15-rc-alpine`) et copiez vos fichiers dedans.  
   - Exécutez votre application via `CMD ["python", "main.py"]`.

2. **Build et test de l’image localement :**  
   - Dans votre terminal, lancez `docker build -t votre-utilisateur/mon-app:latest .`  
   - Lancez le conteneur `docker run -it --rm votre-utilisateur/mon-app:latest` pour vérifier qu’il fonctionne.

3. **Intégration du build Docker dans la CI/CD :**  
   - Ajoutez au pipeline CI une étape pour construire l’image Docker et la pousser sur un registre (Docker Hub ou GitHub Container Registry).  
   - Configurez les secrets (login/mot de passe) du registre dans GitHub/GitLab.  
   - Validez que le pipeline crée et pousse l’image après les tests réussis.

4. **Déploiement sur un environnement de test :**  
   - Si vous avez un petit serveur de test (local ou dans le cloud), exécutez `docker pull` puis `docker run` pour déployer l’app.  
   - (Optionnel) Intégrez la commande de déploiement via SSH ou API dans le pipeline pour un déploiement automatisé.

À la fin de cette séance, votre pipeline CI/CD construit et déploie automatiquement votre application.

---

### TD DevOps 4 (2h) : Orchestration avec Kubernetes et Infrastructure as Code

**Objectifs :**  

- Déployer l’application sur un cluster Kubernetes local.  
- Découvrir le concept d’Infrastructure as Code.

**Étapes :**  

1. **Cluster Kubernetes local (kind ou minikube) :**  
   - Installez `kind` ou `minikube` sur votre machine.  
   - Lancez `kind create cluster` ou `minikube start` pour avoir un cluster local.

2. **Manifests Kubernetes :**  
   - Créez un fichier `deployment.yaml` pour déployer le conteneur.  
   - Créez un fichier `service.yaml` pour exposer l’application.  
   - Lancez `kubectl apply -f deployment.yaml -f service.yaml`.

3. **Intégration au pipeline :**  
   - Ajouter une étape dans la CI/CD qui, après build de l’image, met à jour le déploiement sur Kubernetes (par exemple via `kubectl`).
   - Explorez l’Infrastructure as Code (ex. Terraform) :  
     - Rédigez un fichier Terraform simple pour créer une ressource (optionnel selon le temps disponible).

4. **Vérification du déploiement :**  
   - Utilisez `kubectl get pods`, `kubectl get svc` pour vérifier que l’application est en ligne.  
   - Testez l’application via l’URL ou le NodePort fourni par le Service.

À la fin de cette séance, vous aurez un environnement orchestré par Kubernetes et une compréhension basique de l’IaC.

---

### TD DevOps 5 (2h) : Sécurité, Monitoring et Pipeline Complet

**Objectifs :**  

- Ajouter un scan de sécurité dans le pipeline.  
- Mettre en place un outil de monitoring/logging.  
- Valider le pipeline complet (tests, build, security, déploiement).

**Étapes :**  

1. **Scan de vulnérabilités :**  
   - Utilisez un outil comme `trivy` ou `snyk` pour scanner l’image Docker.  
   - Ajoutez une étape dans le pipeline qui lance ce scan.  
   - Configurez la CI pour échouer si des vulnérabilités critiques sont détectées.

2. **Monitoring et Logs :**  
   - Installez `Prometheus` ou `ELK Stack` (ou simplement un `kubectl logs`) pour visualiser les logs.  
   - Décrivez comment on pourrait intégrer des métriques dans l’application (ex. endpoint `/metrics` pour Prometheus).

3. **Vérification du pipeline complet :**  
   - Faites un changement dans le code, push et observez :  
     - Les tests se lancent.  
     - Le build Docker se fait.  
     - Le scan de vulnérabilité se lance.  
     - Le déploiement Kubernetes se met à jour.
   - Vérifiez que tout se passe bien et qu’en cas de problème, la CI échoue.

À la fin de cette séance, vous disposez d’un pipeline CI/CD complet intégrant la sécurité, le déploiement, et le monitoring.

---

## Partie 2 : Power Apps (5h TD : 2h + 2h + 1h)

### TD Power Apps 1 (2h) : Prise en Main de Power Apps (Canvas App)

**Objectifs :**  

- Créer une première Canvas App.  
- Ajouter des composants d’interface et se connecter à une source de données simple.

**Étapes :**  

1. **Connexion à Power Apps :**  
   - Connectez-vous à Office 365/Power Platform (compte fourni).  
   - Accédez à Power Apps : <https://make.powerapps.com>

2. **Création d’une Canvas App :**  
   - Cliquez sur “Create” > “Canvas app from blank”.  
   - Donnez un nom à votre application.  
   - Ajoutez un écran et des contrôles simples (boutons, étiquettes, galeries).

3. **Connexion à une source de données :**  
   - Ajoutez un connecteur (par ex. Excel, SharePoint list).  
   - Affichez les données dans une galerie.  
   - Testez l’application en mode “Play”.

4. **Enregistrement et partage :**  
   - Enregistrez l’app, publiez-la.  
   - Optionnel : partagez-la avec un collègue de la classe (sans droit d’édition, juste consultation).

---

### TD Power Apps 2 (2h) : Fonctionnalités Avancées et Intégration Power Automate

**Objectifs :**  

- Personnaliser l’application avec des formules et des règles.  
- Intégrer un flux Power Automate pour automatiser une tâche.

**Étapes :**  

1. **Personnalisation :**  
   - Ajoutez une condition pour afficher certains éléments (par ex. si un champ est vide, afficher un message).  
   - Utilisez les formules Power Apps (type Excel) pour filtrer, trier les données.

2. **Intégration Power Automate :**  
   - Créez un flux Power Automate simple (par ex. déclenché par un bouton dans Power Apps, envoi d’e-mail).  
   - Liez ce flux à votre application Power Apps.  
   - Testez le déclenchement du flux depuis l’app.

3. **Connecteurs supplémentaires :**  
   - Ajoutez un autre connecteur (ex. une API publique ou un connecteur standard) pour enrichir votre application.  
   - Affichez les données de ce connecteur dans un nouvel écran.

---

### TD Power Apps 3 (1h) : Finalisation et Présentation

**Objectifs :**  

- Finaliser l’application.  
- Préparer une petite présentation de l’application.

**Étapes :**  

1. **Tests et Ajustements :**  
   - Vérifiez chaque écran, chaque bouton, chaque flux.  
   - Corrigez les petits bugs (affichage, formules incorrectes).

2. **Documentation rapide :**  
   - Rédigez un court document (ou sur GitHub) décrivant les fonctionnalités et les connecteurs utilisés.  
   - Ajoutez des captures d’écran.

3. **Présentation :**  
   - Montrez en 5 minutes l’application à votre groupe de TD.  
   - Expliquez la logique, les données utilisées, et le flux automatisé.

À la fin de cette partie Power Apps, vous aurez une application fonctionnelle, connectée à des données externes, et intégrant un flux automatisé.

---

**Évaluation continue :**  

- QCM sur les notions vues en CM.  
- Évaluation de la qualité des TD (commit régulier, respect des bonnes pratiques).  
- Évaluation du projet final (pipeline complet CI/CD + Application Power Apps fonctionnelle).

Ainsi, chaque TD est présenté sous forme de tutoriel concret, orienté vers la pratique, avec des étapes claires. Les étudiants peuvent ainsi suivre pas à pas le cheminement technique pour acquérir des compétences solides en DevOps et en Power Apps.
