# 🧪 TD DataOps – Git & CI DRAFT VERSION

## **Introduction au DataOps**

---

## 🧠 Rappel : qu’est-ce que le DataOps ?

> **DataOps** consiste à appliquer les principes DevOps
> (**versioning, CI/CD, qualité, automatisation**)
> aux **pipelines de données**.

En DataOps :

* les **données sont des artefacts versionnés**
* les **transformations doivent être reproductibles**
* la **qualité des données est testée automatiquement**

---

## 📁 Structure du projet

Vous travaillerez sur le dépôt suivant :

```mermaid
.
├── data/
│   ├── raw/
│   │   └── sales.csv
│   └── processed/
│       └── sales_clean.csv
├── src/
│   └── clean_data.py
├── tests/
│   └── test_data_quality.py
├── .github/
│   └── workflows/
│       └── ci.yml
└── README.md
```

---

## 🧪 Partie 1 – Gitflow version DataOps

### 1️⃣ Initialisation du dépôt

* Créez un dépôt Git
* Ajoutez un fichier `sales.csv` dans `data/raw/`

Exemple de contenu :

```csv
id,product,price
1,keyboard,49.99
2,mouse,
3,screen,199.99
```

📌 **Question**
Pourquoi cette donnée est-elle problématique pour un pipeline data ?

---

### 2️⃣ Gitflow adapté au DataOps

Règles à respecter :

* `main` : données **validées**
* `develop` : données en cours de préparation
* `feature/*` : transformation ou correction data

📌 Exemple :

```bash
git checkout -b feature/clean-sales-data
```

---

### 3️⃣ Bonnes pratiques de commit DataOps

❌ Mauvais commit :

```git
update data
```

✅ Bon commit :

```git
feat(data): clean null prices in sales dataset
```

📌 **Consigne**

> Faites un commit expliquant clairement **ce qui change dans la donnée** et **pourquoi**.

---

## 🧪 Partie 2 – Transformation de données

### 4️⃣ Script de nettoyage (Python)

Dans `src/clean_data.py` :

```python
import pandas as pd

df = pd.read_csv("data/raw/sales.csv")

df_clean = df.dropna()

df_clean.to_csv("data/processed/sales_clean.csv", index=False)
```

📌 Exécutez le script et vérifiez le fichier généré.

---

## 🧪 Partie 3 – Tests de qualité de données

### 5️⃣ Pourquoi tester les données ?

En DataOps, on teste que :

* il n’y a pas de valeurs nulles
* les types sont corrects
* le volume est cohérent

---

### 6️⃣ Test de qualité simple

Dans `tests/test_data_quality.py` :

```python
import pandas as pd

def test_no_null_values():
    df = pd.read_csv("data/processed/sales_clean.csv")
    assert df.isnull().sum().sum() == 0

def test_price_is_positive():
    df = pd.read_csv("data/processed/sales_clean.csv")
    assert (df["price"] > 0).all()
```

📌 **Question**

> En quoi ces tests sont-ils différents de tests unitaires classiques ?

---

## 🧪 Partie 4 – CI DataOps (GitHub Actions)

### 7️⃣ Pipeline CI

Dans `.github/workflows/ci.yml` :

```yaml
name: DataOps CI

on: [push, pull_request]

jobs:
  data-quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Install dependencies
        run: pip install pandas pytest

      - name: Run data transformation
        run: python src/clean_data.py

      - name: Run data quality tests
        run: pytest tests/
```

📌 **Résultat attendu**

* La CI échoue si les données sont invalides
* Une PR avec une mauvaise donnée ne peut pas être mergée

---

## 🧪 Partie 5 – Pull Request DataOps

### 8️⃣ Workflow de PR

1. Travaillez dans une branche `feature/*`
2. Ouvrez une **Pull Request**
3. La CI s’exécute automatiquement
4. La PR n’est mergée que si :

   * les tests passent
   * la modification est justifiée

---

### 9️⃣ Bonnes pratiques de PR DataOps

Dans la description de la PR, indiquez :

* Quelle donnée est modifiée ?
* Pourquoi ?
* Quel impact métier ?

**Ça ne vous rappel rien ? #QQOQCP**  ( Ç == alt+0199 || alt+128)

📌 Exemple :

> Cette PR supprime les lignes avec prix nulls afin d’éviter des erreurs dans les calculs du chiffre d’affaires.

---

## 🏁 Conclusion

> TODO
