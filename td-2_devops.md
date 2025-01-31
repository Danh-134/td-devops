
# TD DevOps 2 (2h)  

## Thème : Intégration Continue avancée (Tests JUnit, Qualité du code)

**Objectifs :**  

- Ajouter des tests unitaires JUnit.  
- Automatiser leur exécution dans GitHub Actions.  
- Intégrer un outil de qualité de code (Checkstyle ou SpotBugs).

### Étapes détaillées JUnit

1. **Ajouter des tests JUnit 5**  
  Dans `demo-app/src/test/java/com/example/AppTest.java`, ajoutez :

     ```java
     package com.example;

     import org.junit.jupiter.api.Test;
     import static org.junit.jupiter.api.Assertions.*;

     public class AppTest {

       @Test
       public void testSum() {
         int result = App.sum(2, 3);
         assertEquals(5, result, "2 + 3 should be 5");
       }
     }

  Dans `App.java` (dans `src/main/java/com/example`), créez la méthode sum :
        ```java
          public static int sum(int a, int b) {
            return a + b;
          }
          ```
2. **Test en local**  

- À la racine du projet, exécutez :

     ```bash
     mvn test -f demo-app/pom.xml
     ```

- Vous devriez voir un test réussi.

3. **Mettre à jour le workflow CI pour exécuter les tests**  
   - Dans `.github/workflows/ci.yml`, remplacez la commande de build par :

     ```yaml
     - name: Build and Test with Maven
       run: mvn clean install --file demo-app/pom.xml
     ```

   - Commitez, poussez.  
   - Dans l’onglet Actions, vérifiez que le job exécute bien les tests.

4. **Intégrer Checkstyle (exemple)**  
    - Dans `demo-app/pom.xml`, ajoutez la dépendance Checkstyle dans la section `<build>` -> `<plugins>` :

      ```xml
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-checkstyle-plugin</artifactId>
        <version>3.2.2</version>
        <configuration>
          <configLocation>google_checks.xml</configLocation>
          <encoding>UTF-8</encoding>
          <consoleOutput>true</consoleOutput>
          <failsOnError>true</failsOnError>
        </configuration>
        <executions>
          <execution>
            <phase>verify</phase>
            <goals>
              <goal>check</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
      ```

  Téléchargez [google_checks.xml](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml) et placez-le dans `demo-app/`.  
  Lancer les commandes :
    ```bash
     mvn clean verify -f demo-app/pom.xml
     ```
  Si vous avez des soucis de style, le build échouera.

5. **Automatisation avec GitHub Actions**  
   - Les étapes `mvn clean install` incluront la phase `verify`, donc Checkstyle sera exécuté.  
   - Commitez, poussez, observez le résultat.

**À la fin de cette séance**, la CI exécute tests + checkstyle, et échoue si la qualité du code n’est pas respectée.

---