Parfait 👍
Voici **les deux livrables**, séparés comme demandé :

1. **TD Docker DataOps – version étudiant (clé en main)**
2. **Fiche enseignant (corrigé + objectifs pédagogiques cachés)**

Tu peux les mettre dans ton repo sous deux fichiers distincts.

---

# 🧪 TD DataOps – Docker & Pipelines de Données

## 🎯 Objectifs du TD

À l’issue de ce TD, vous serez capables de :

* Comprendre le rôle de **Docker en DataOps**
* Construire un **pipeline de données reproductible**
* Séparer **données, code et environnement**
* Comprendre pourquoi Docker est critique pour la fiabilité des pipelines data

---

## 🧠 Rappel : Docker en DataOps

En DataOps, Docker permet de :

* garantir que les pipelines tournent **dans le même environnement**
* éviter les problèmes de versions (Python, librairies)
* exécuter les traitements data **de manière reproductible**

> 💡 Un pipeline DataOps doit produire **le même résultat**, peu importe la machine.

---

## 📁 Structure du projet

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
├── Dockerfile
└── README.md
```

---

## 🧪 Partie 1 – Pipeline de données simple

### 1️⃣ Script de transformation

`src/clean_data.py` :

```python
import pandas as pd

df = pd.read_csv("data/raw/sales.csv")

df_clean = df.dropna()
df_clean = df_clean[df_clean["price"] > 0]

df_clean.to_csv("data/processed/sales_clean.csv", index=False)
```

📌 **Question**
Pourquoi cette transformation doit-elle être déterministe ?

---

## 🧪 Partie 2 – Dockerisation du pipeline DataOps

### 2️⃣ Dockerfile

Créez un fichier `Dockerfile` :

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY src/ src/
COPY tests/ tests/
COPY data/ data/

RUN pip install pandas pytest

CMD ["python", "src/clean_data.py"]
```

📌 **Question**
Pourquoi ne pas copier tout le dépôt sans distinction ?

---

### 3️⃣ Build de l’image

```bash
docker build -t dataops-pipeline .
```

---

### 4️⃣ Exécution du pipeline

```bash
docker run --rm dataops-pipeline
```

📌 Vérifiez que le fichier `sales_clean.csv` est bien généré.

---

## 🧪 Partie 3 – Tests de qualité dans Docker

### 5️⃣ Exécuter les tests dans le conteneur

```bash
docker run --rm dataops-pipeline pytest tests/
```

📌 **Question**
Pourquoi tester les données **dans** le conteneur ?

---

## 🧪 Partie 4 – Volumes Docker (données persistantes)

### 6️⃣ Montage de volume

```bash
docker run --rm \
  -v $(pwd)/data:/app/data \
  dataops-pipeline
```

📌 **Objectif**

* Séparer l’environnement (conteneur)
* des données (volume)

---

## 🧪 Partie 5 – DataOps vs DevOps

| DevOps              | DataOps             |
| ------------------- | ------------------- |
| Image = application | Image = pipeline    |
| Logs applicatifs    | Logs + qualité data |
| Tests unitaires     | Tests data          |

📌 **Question finale**

> Pourquoi Docker est-il encore plus critique en DataOps qu’en DevOps ?

---

## 🏁 Conclusion

## TODO

---
