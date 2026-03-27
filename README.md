# 📊 La place des femmes dans l'industrie française — 2017–2024

> *Ce projet est né d'une curiosité : à l'occasion de ma participation à*
> ***L'Industrie C'est Féminin** (Marseille, 30 mars 2026), j'ai voulu*
> *comprendre ce que les données disent vraiment sur la place des femmes*
> *dans l'industrie française.*

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://python.org)
[![Pandas](https://img.shields.io/badge/pandas-2.0-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![Tableau](https://img.shields.io/badge/Tableau-Public-E97627?logo=tableau&logoColor=white)](https://public.tableau.com)
[![INSEE](https://img.shields.io/badge/Source-INSEE-003189)](https://insee.fr)
[![Licence](https://img.shields.io/badge/Licence-Ouverte_2.0-00A86B)](https://www.etalab.gouv.fr/licence-ouverte-open-licence)

---

## 🎯 Objectif

Analyser l'évolution de la part des femmes dans **16 sous-secteurs industriels** en France sur 8 ans (2017–2024), identifier les secteurs qui progressent vers la parité et ceux qui stagnent, et visualiser ces tendances dans un dashboard interactif.

---

## 📈 Insights clés

| Secteur | 2017 | 2024 | Variation | Tendance |
|---------|------|------|-----------|----------|
| 💧 Eau, assainissement, déchets | 18.7% | 28.0% | **+9.3 pts** | ↑ Hausse |
| 💊 Industrie pharmaceutique | 46.5% | 54.8% | **+8.3 pts** | ↑ Hausse |
| 🧪 Industrie chimique | 33.3% | 40.7% | **+7.4 pts** | ↑ Hausse |
| ⚡ Électricité, gaz, vapeur | 26.7% | 32.4% | **+5.7 pts** | ↑ Hausse |
| ✈️ Matériels de transport | 19.9% | 20.3% | **+0.4 pts** | → Stable |
| 🏗️ Métallurgie, produits métalliques | ~16% | ~17% | **~+1 pt** | → Stable |
| 👗 Textile, habillement, cuir | 69.1% | 63.1% | **-6.0 pts** | ↓ Baisse |
| ⚙️ Équipements électriques | 28.5% | 24.1% | **-4.4 pts** | ↓ Baisse |

> **À retenir :** Les secteurs scientifiques et énergétiques progressent régulièrement.
> Les secteurs de fabrication traditionnels (métallurgie, matériels de transport, machines) stagnent.
> Ces tendances montrent une réalité nuancée : l'industrie évolue, lentement mais sûrement.

---

## 🗂️ Structure du projet

```
projet2-parite-industrie-france/
│
├── data/
│   ├── raw/                              # Fichiers bruts INSEE (non modifiés)
│   │   ├── INSEE_CSS02_2017.xls
│   │   ├── INSEE_CSS02_2018.xls
│   │   ├── INSEE_CSS02_2019.csv
│   │   ├── INSEE_CSS02_2020.csv
│   │   ├── INSEE_CSS02_2021.csv
│   │   ├── INSEE_CSS02_2022.csv
│   │   ├── INSEE_CSS02_2023.xlsx
│   │   └── INSEE_CSS02_2024.xlsx
│   │
│   └── processed/                        # Fichiers nettoyés (générés par le script)
│
├── notebooks/
│   ├── 01_data_cleaning_v3.py            # Nettoyage et harmonisation des données
│   └── 02_analysis_parite.ipynb          # Analyse et calcul des indicateurs
│
├── dashboard/
│   └── tableau/
│       └── Projet-parite-industrie-france.twbx  # Dashboard Tableau Public
│
├── README.md
```

---

## 🗃️ Dictionnaire des variables

| Variable | Type | Description |
|----------|------|-------------|
| `annee` | int | Année de l'enquête (2017 à 2024) |
| `secteur` | str | Libellé court du secteur, harmonisé sur toutes les années (nomenclature INSEE NA38) |
| `pop_femmes` | float | Nombre de femmes en emploi dans ce secteur (en milliers) |
| `pop_total` | float | Nombre total de personnes en emploi — hommes + femmes (en milliers) |
| `part_femmes` | float | % de femmes parmi les personnes en emploi — calculé : (pop_femmes / pop_total) × 100 |
| `famille` | str | Catégorie du secteur : `Industrie` ou `Autres secteurs` (fichier étendu uniquement) |

---

## 🛠️ Stack technique

| Outil | Usage |
|-------|-------|
| **Python 3.12** | Nettoyage, transformation, analyse |
| **pandas** | Lecture de 8 formats différents (xls, csv, xlsx), concat, pivot, merge |
| **openpyxl** | Lecture des fichiers Excel (.xlsx) |
| **Jupyter Notebook** | Analyse exploratoire et calcul des indicateurs |
| **Tableau Public** | Dashboard interactif avec filtres dynamiques |

---

## ⚠️ Notes méthodologiques

**Formats hétérogènes selon les années**

Les 8 fichiers bruts INSEE ont des structures différentes selon l'année :

| Années | Format | Particularités |
|--------|--------|----------------|
| 2017–2018 | `.xls` | 3 onglets (Ensemble/Femmes/Hommes) · données ligne 6+ · col 1 = effectif |
| 2019–2020 | `.csv` | SEXE numérique : `1=Hommes`, `2=Femmes`, `3=Ensemble` |
| 2021–2022 | `.csv` | SEXE texte : `FEMMES`, `ENSEMBLE` · décimales avec virgule française |
| 2023–2024 | `.xlsx` | Onglets nommés FEMMES/ENSEMBLE · données ligne 8+ · col 15 = effectif Total |

**Rupture méthodologique 2021**

En 2021, l'INSEE a rénové l'Enquête Emploi en continu. Le terme *actifs occupés* (2017–2020) devient *personnes en emploi* (2021–2024). Les données restent comparables sur `part_femmes`, mais une ligne de référence verticale en 2021 est recommandée dans les graphiques.

**Codes SEXE CSV 2019–2020**

`SEXE=2` correspond aux Femmes (et non `SEXE=1` comme on pourrait l'attendre). Ce point contre-intuitif a été vérifié manuellement sur le secteur Agriculture (~29% de femmes).

---

## 📊 Dashboard interactif

| Outil | Lien |
|-------|------|
| **Tableau Public** | [🔗 Voir le dashboard interactif](https://public.tableau.com/views/Projet-parite-industrie-france/Dashboard?:language=fr-FR&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) |

Le dashboard contient :
- **Vue 1** — Courbes d'évolution par secteur (2017–2024) avec ligne de parité à 50%
- **Vue 2** — Bar chart horizontal des variations 2017→2024, coloré par tendance
- **3 filtres dynamiques** — Famille · Secteur · Tendance (contrôlent les 2 vues simultanément)
- **Panel insights** — Les 3 enseignements clés de l'analyse

---

## 🗃️ Sources de données

**INSEE — Enquête Emploi en continu, tableau CSS02**
*Catégorie socioprofessionnelle des personnes en emploi selon le sexe et le secteur d'activité*

| Année | Format | Lien |
|-------|--------|------|
| 2017 | .xls | [insee.fr](https://www.insee.fr/fr/statistiques/3541402?sommaire=3541412) |
| 2018 | .xls | [insee.fr](https://www.insee.fr/fr/statistiques/3900819?sommaire=3900836) |
| 2019 | .csv | [insee.fr](https://www.insee.fr/fr/statistiques/4498601?sommaire=4498692) |
| 2020 | .csv | [insee.fr](https://www.insee.fr/fr/statistiques/5359503?sommaire=5359511) |
| 2021 | .csv | [insee.fr](https://www.insee.fr/fr/statistiques/6460133?sommaire=6462858) |
| 2022 | .csv | [insee.fr](https://www.insee.fr/fr/statistiques/7629866?sommaire=7625272) |
| 2023 | .xlsx | [insee.fr](https://www.insee.fr/fr/statistiques/8217905?sommaire=8201155) |
| 2024 | .xlsx | [insee.fr](https://www.insee.fr/fr/statistiques/8603464?sommaire=8578977) |

---

## 🚀 Reproduire l'analyse

```bash
# 1. Cloner le dépôt
git clone https://github.com/ton-profil/projet2-parite-industrie-france
cd projet2-parite-industrie-france

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. Placer les fichiers INSEE bruts dans data/raw/
#    (télécharger depuis les liens ci-dessus)

# 4. Exécuter le nettoyage
jupyter notebook notebooks/01_data_cleaning_v3.py

# 5. Exécuter l'analyse
jupyter notebook notebooks/02_analysis_parite.ipynb
```

## 👩‍💻 Auteure

**Adelaida RETUERTO**
Étudiante Data Analyst · En recherche d'alternance 

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profil-0077B5?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/adelaida-retuerto)

---

## 📄 Licence

Données publiques INSEE — [Licence Ouverte / Open Licence 2.0](https://www.etalab.gouv.fr/licence-ouverte-open-licence)
Code source — [MIT License](LICENSE)
