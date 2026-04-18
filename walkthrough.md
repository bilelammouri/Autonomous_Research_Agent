# Système Consolidé d'Agent de Recherche Autonome

Monsieur le Professeur, j'ai regroupé et mis à jour le cœur de votre système dans un dossier unique pour garantir une stabilité totale. Ce pipeline ignore l'interface et se concentre sur la **production scientifique** brute.

## Structure du Dossier `Autonomous_Research_Agent`

L'ensemble du flux est désormais modulaire et synchronisé :
- **`scopus_collector.py`** : Transforme votre thème en requête booléenne, collecte les métadonnées et exporte en `.bib`.
- **`analysis_engine.R`** : Analyse bibliométrique via R-Bibliometrix, génère les cartes réseaux et les métriques de citations.
- **`paper_ranker.py`** : Fusionne les données de Scopus et de R pour identifier les 15 articles les plus influents (Ranking).
- **`review_drafter.py`** : Rédige la synthèse thématique de 5000 mots en LaTeX et compile le PDF final.
- **`master_agent.py`** : Le chef d'orchestre qui exécute toute la mission en une seule commande.

---

## Étapes pour Tester (Mode Commande)

Suivez ces étapes dans votre terminal pour lancer une mission complète :

### 1. Préparation
Assurez-vous que votre clé API Scopus est dans `agent_config.json` à la racine (le script la copiera automatiquement).

### 2. Lancement Global
Ouvrez votre terminal dans le dossier du projet et exécutez :
```powershell
cd "Autonomous_Research_Agent"
python master_agent.py
```

### 3. Résultats
Une fois le script terminé, vous trouverez dans le dossier :
- `main.pdf` : Votre revue de littérature synthétique Q1 compilée.
- `results.bib` : Votre base de données bibliographique complète.
- `bibliometric_summary.png` : Les graphiques impact/citations générés par R.
- `citation_metrics.csv` : Le détail du classement calculé par R.

---

## Points Techniques Clés

> [!IMPORTANT]
> **Dépendances R** : Le script R a été configuré pour installer `bibliometrix` localement dans `../R_libs` s'il ne le trouve pas. La première exécution peut donc prendre 2-3 minutes pour le setup R.
> 
> **Handshake R-Python** : Le `paper_ranker.py` ne se contente plus de lire les citations de Scopus ; il croise ces données avec l'analyse de prestige calculée par R pour garantir que les papiers les plus "centraux" dans le réseau sont prioritaires pour la rédaction.

Ce dossier est maintenant votre version de référence "Production" pour vos tests de pipeline.
