## Pré-requis pour tous les TD DevOps

1. **Java (JDK) 11 ou supérieur**  
   - [Installation OpenJDK 11](https://openjdk.org/install/)  
   - Vérifier l’installation :

     ```bash
     java -version
     ```

2. **Maven**  
   - [Téléchargement et installation Maven](https://maven.apache.org/download.cgi)  
   - Vérifier l’installation :  

     ```bash
     mvn -v
     ```

3. **Git**  
   - [Installation de Git](https://git-scm.com/downloads)  
   - Vérifier l’installation :  

     ```bash
     git --version
     ```

4. **Docker**  
   - [Installer Docker Desktop (Windows/Mac)](https://www.docker.com/products/docker-desktop/) ou [Docker Engine (Linux)](https://docs.docker.com/engine/install/)  
   - Vérifier l’installation :  

     ```bash
     docker --version
     ```

5. **Compte GitHub** (ou GitLab)  
   - [Créer un compte GitHub](https://github.com/join)

    *(Les étapes ci-après sont illustrées pour GitHub et GitHub Actions, mais vous pouvez adapter pour GitLab et GitLab CI.)*

---

## TD DevOps 1 (2h)  

### Thème : Prise en main de Git & Mise en place d’un pipeline CI basique

**Objectifs :**  

- Créer un dépôt Git pour un projet Java/Maven.  
- Mettre en place une première GitHub Action (CI) qui se déclenche à chaque push.

---

### Étapes détaillées Git

1. **Installer/Configurer Git**  
   - Suivre le lien d’installation plus haut.  
   - Configurer votre nom d’utilisateur et e-mail (pour les commits) :  

     ```bash
     git config --global user.name "VotreNom"
     git config --global user.email "votre_email@example.com"
     ```

2. **Créer un compte GitHub** *(si ce n’est pas déjà fait)*  
   - Allez sur [https://github.com/join](https://github.com/join)  
   - Remplissez le formulaire pour vous inscrire.

3. **Création d’un nouveau dépôt sur GitHub**  
   - Connectez-vous à votre compte.  
   - Cliquez sur **New** ou accédez à [https://github.com/new](https://github.com/new).  
   - Donnez un nom à votre dépôt, ex. `demo-devops-java`.  
   - Laissez-le en **Public** ou **Privé** (selon votre préférence).  
   - Cochez l’option “Add a README file” si vous le souhaitez.

4. **Clonage du dépôt en local**  
   - Copiez l’URL HTTPS de votre dépôt (ex. `https://github.com/VotreUser/demo-devops-java.git`).  
   - Dans un terminal, exécutez :  

     ```bash
     git clone https://github.com/VotreUser/demo-devops-java.git
     cd demo-devops-java
     ```

5. **Initialisation d’un projet Maven**  
   - Dans le dossier cloné, exécutez la commande Maven pour générer un squelette de projet :  

     ```bash
     mvn archetype:generate \
       -DgroupId=com.example \
       -DartifactId=demo-app \
       -DarchetypeArtifactId=maven-archetype-quickstart \
       -DarchetypeVersion=1.4 \
       -DinteractiveMode=false
     ```

   - Cette commande crée un dossier `demo-app` contenant `pom.xml`, `src/main/java/...`, etc.

6. **Premier commit & push**  
   - Ajoutez tous les fichiers :  

     ```bash
     git add .
     git commit -m "Initial Maven project"
     git push origin main
     ```

   - Vérifiez sur GitHub que votre code est bien en ligne.

7. **Mise en place d’un pipeline CI basique (GitHub Actions)**  
   - Dans votre dépôt GitHub, cliquez sur l’onglet **Actions**.  
   - Choisissez **Set up a workflow yourself** (ou un template “Java with Maven”).  
   - Créez un fichier (par exemple) `.github/workflows/ci.yml` avec le contenu minimal suivant :

     ```yaml
     name: CI

     on:
       push:
         branches: [ "main" ]
       pull_request:
         branches: [ "main" ]

     jobs:
       build:
         runs-on: ubuntu-latest
         steps:
           - uses: actions/checkout@v2
           - name: Set up JDK 11
             uses: actions/setup-java@v3
             with:
               java-version: '11'
               distribution : temurin
           - name: Build with Maven
             run: mvn -B package --file demo-app/pom.xml
     ```

   - Commitez ce fichier.  
   - Rendez-vous dans l’onglet **Actions**, vous verrez votre workflow se lancer.

**À la fin de cette séance**, vous avez un dépôt Java/Maven avec un pipeline CI qui build le projet à chaque push.

---
