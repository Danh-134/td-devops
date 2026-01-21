# Partie 1 : DevOps (10h TD en 5 séances de 2h)

## Pré-requis pour tous les TD DevOps

1. **Java (JDK) 25 ou supérieur**  
   - [Installation OpenJDK 25](https://openjdk.org/projects/jdk/25/)  
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

   - Sur les postes AMU, installer Podman Desktop : [Installer Podman Desktop Windows](https://podman-desktop.io/downloads/windows)
   - Ou avec la commande : `winget install -e --id RedHat.Podman-Desktop`

   - Vérifier l’installation :  

     ```bash
     podman machine init
     ```

5. **Compte GitHub** (ou GitLab)  
   - [Créer un compte GitHub](https://github.com/join)

    *(Les étapes ci-après sont illustrées pour GitHub et GitHub Actions, mais vous pouvez adapter pour GitLab et GitLab CI.)*

---
