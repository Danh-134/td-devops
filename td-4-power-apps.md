# Partie 2 : Power Apps (5h TD : 2h + 2h + 1h)

## Pré-requis pour Power Apps

1. **Compte Office 365 / Power Platform**  
   - Accéder à [https://make.powerapps.com](https://make.powerapps.com).  
   - Avoir les droits pour créer des applications (Canvas apps).

2. **Navigateur Web** (Edge, Chrome, ou Firefox recommandé).

   *(Aucun outil à installer localement pour Power Apps, tout est en ligne.)*

---

## TD Power Apps 1 (2h)

### Thème : Prise en main (Canvas App)

**Objectifs :**  

- Créer une Canvas App.  
- Ajouter des contrôles de base et se connecter à une source de données simple (Excel, SharePoint).

---

### Étapes détaillées Platform

1. **Connexion à la Power Platform**  
   - Ouvrez [https://make.powerapps.com](https://make.powerapps.com).  
   - Identifiez-vous avec votre compte Office 365 fourni.

2. **Créer une Canvas App from blank**  
   - Cliquez sur **Create** > **Canvas app from blank**.  
   - Nommez l’application “DemoCanvasApp”.  
   - Sélectionnez un format (Tablet ou Phone).

3. **Éditeur Power Apps**  
   - Familiarisez-vous avec l’interface :  
     - **Tree view** (composants)  
     - **Insert** (Label, Button, Gallery…)  
     - **Data** (connecteurs)
   - Ajoutez un **Label** avec le texte “Hello Power Apps”.

4. **Connexion à une source de données**  
   - Dans le menu **Data**, cliquez sur **Add data**.  
   - Sélectionnez par exemple **Excel Online (Business)** ou **SharePoint** ou **SQL**.
   - Choisissez un fichier ou une liste existante.  
   - Insérez une **Gallery** et liez-la à cette source.

5. **Test de l’app**  
   - Cliquez sur le bouton **Play** (►) en haut à droite.  
   - Parcourez la galerie, vérifiez que les données s’affichent.  
   - Enregistrez l’application (File > Save > Publish).

**À la fin de cette séance**, vous avez une Canvas App basique connectée à une source de données.

## TD Power Apps 2 (2h)  

### Thème : Fonctionnalités avancées & Power Automate

**Objectifs :**

- Personnaliser l’application avec des formules.  
- Créer un flux Power Automate et l’appeler depuis l’app.

---

### Étapes détaillées (Exemple)

1. **Utilisation de Formules (Style Excel)**  
   - Sélectionnez votre galerie ou un label.  
   - Dans la barre de formules, essayez un filtre, par ex. :  

     ```plaintext
     Filter(MyDataSource, Status = "Active")
     ```

   - Ajoutez un **Text input** et un **Button** pour faire un filtrage dynamique :

     ```plaintext
     Filter(MyDataSource, Name StartsWith TextInput1.Text)
     ```

2. **Power Automate**  
   - Ouvrez un second onglet : [https://make.powerautomate.com](https://make.powerautomate.com).  
   - Créez un **Flow** “Instant cloud flow” déclenché par Power Apps.  
   - Ajoutez une action “Send an email” ou “Create an item in SharePoint”.  
   - Dans Power Apps, dans l’éditeur, sélectionnez **Action** > **Power Automate** > **+ Create Flow** ou connectez le Flow existant.  
   - Dans votre bouton, appelez le flow :

     ```plaintext
     OnSelect = MyFlow.Run("Param1", "Param2")
     ```

3. **Tester le flux**  
   - En mode Play de l’app, cliquez sur le bouton.  
   - Vérifiez que l’action (email, insertion en base, etc.) est déclenchée.  

4. **Autres connecteurs**  
   - Essayez d’ajouter un connecteur “HTTP” ou d’autres connecteurs standards (Teams, Outlook, etc.).  
   - Intégrez une petite logique conditionnelle (If…).

---

**À la fin de cette séance**, vous avez une application plus riche, utilisant Power Automate pour automatiser des tâches.
