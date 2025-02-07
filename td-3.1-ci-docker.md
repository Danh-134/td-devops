
## TD DevOps 3 (2h)  

### Thème : Déploiement Continu (CD) et Conteneurisation avec Docker

**Objectifs :**  

- Créer et pousser une image Docker de l’application Java.  
- Mettre en place la publication automatique (CD) via GitHub Actions.

---

### Étapes détaillées JAR

1. **Créer un jar exécutable**  
    - Dans `demo-app/pom.xml`, assurez-vous d’avoir le plugin `maven-assembly-plugin` ou `maven-shade-plugin` pour créer un fat jar (toutes dépendances incluses).  

    Exemple pour `maven-assembly-plugin` :

      ```xml
        <plugin>
          <artifactId>maven-assembly-plugin</artifactId>
          <version>3.3.0</version>
          <configuration>
            <archive>
              <manifest>
                <mainClass>com.example.App</mainClass>
              </manifest>
            </archive>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
          </configuration>
          <executions>
            <execution>
              <id>make-assembly</id>
              <phase>package</phase>
              <goals>
                <goal>single</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
      ```

    Lancez :  
        ```bash
        mvn clean package -f demo-app/pom.xml
        ```
    Vous obtiendrez un fichier `demo-app-1.0-SNAPSHOT-jar-with-dependencies.jar` dans `target/`.

2. **Créer un Dockerfile**  
   - Dans la racine du projet (ou dans `demo-app/`), créez un fichier `Dockerfile` :

     ```dockerfile
     FROM openjdk:11-jre-slim
     COPY target/demo-app-1.0-SNAPSHOT-jar-with-dependencies.jar /app/demo-app.jar
     WORKDIR /app
     ENTRYPOINT ["java", "-jar", "demo-app.jar"]
     ```

3. **Build local de l’image**  
    - Assurez-vous d’avoir Docker en service (`docker --version`).  
    - Dans le dossier contenant le Dockerfile :

      ```bash
      docker build -t votreuser/demo-app:latest .
      ```

    Testez l’image :
        ```bash
        docker run --rm votreuser/demo-app:latest
        ```
    Vous devriez voir la sortie “Hello World!” ou autre, selon votre `App.java`.

4. **Pousser l’image vers Docker Hub ou GitHub Container Registry**  
   - [Créer un compte Docker Hub](https://hub.docker.com/) si besoin.  
   - Connectez-vous via CLI :  

     ```bash
     docker login
     ```

   - Poussez l’image :

     ```bash
     docker push votreuser/demo-app:latest
     ```

5. **Automatiser dans GitHub Actions**  
   - Mettez à jour `.github/workflows/ci.yml` pour ajouter un job de build/push Docker **après** le succès des tests.  
   - Exemple (étapes clés) :

     ```yaml
     - name: Build JAR
       run: mvn clean package -f demo-app/pom.xml
     - name: Build Docker Image
       run: docker build -t votreuser/demo-app:latest .
     - name: Login to Docker Hub
       run: echo "${{ secrets.DOCKERHUB_PASSWORD }}" | docker login -u "${{ secrets.DOCKERHUB_USERNAME }}" --password-stdin
     - name: Push Docker Image
       run: docker push votreuser/demo-app:latest
     ```

   - Dans **Settings > Secrets** de GitHub, ajoutez `DOCKERHUB_USERNAME` et `DOCKERHUB_PASSWORD` (cf. [doc GitHub sur les Secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)).

**À la fin de cette séance**, vous avez un pipeline qui build, teste, et publie l’image Docker de votre app Java.

---
