# Implémentation d'une Stratégie d'Investissement Quantitative Global Macro Multi-Actifs

**Mémoire de fin d'études — M2 Gestion d'Actifs, Université Paris Nanterre**
**Auteur :** TAHIR Badr-eddine  |  **Directeur de mémoire :** [À COMPLÉTER : nom du directeur]  |  **2024**
**Diplômé major de promotion — 16/20**

---

## Résumé

[À COMPLÉTER : coller ici le résumé complet du mémoire — un paragraphe. Reprendre le texte du résumé tel qu'il figure dans le PDF.]

## Contexte

Ce mémoire développe une stratégie d'investissement systématique global macro multi-actifs, traduisant l'analyse des cycles macroéconomiques en décisions concrètes d'allocation de portefeuille. Les travaux ont été menés en parallèle de mon stage buy-side chez BCP / Upline Capital Management (Casablanca), où une version préliminaire du framework a été implémentée sur un portefeuille d'ETFs américains, surperformant le S&P 500 de 4,5 % en risque ajusté (avant frais).

## Données

- **Univers d'investissement :** [À COMPLÉTER : ex. ETFs américains couvrant actions, obligations, matières premières et cash — lister les tickers ou classes d'actifs spécifiques]
- **Période d'étude :** [À COMPLÉTER : ex. janvier 2010 – décembre 2023]
- **Indicateurs macroéconomiques :** [À COMPLÉTER : ex. pente de la courbe des taux, ISM PMI, taux de chômage, CPI, indicateurs de conditions financières, spreads de crédit]
- **Sources :** [À COMPLÉTER : ex. FRED, Bloomberg, FactSet]

## Méthodologie

[À COMPLÉTER : détailler chaque point — c'est la section la plus lue par les recruteurs.]

- **Identification des régimes macroéconomiques :** [À COMPLÉTER : ex. framework des phases du cycle économique (expansion / ralentissement / récession / reprise), ou méthode de détection de régimes — HMM, règles de seuil, basé sur l'output gap]
- **Construction des signaux :** [À COMPLÉTER : comment les variables macro sont transformées en signaux d'allocation]
- **Règle d'allocation :** [À COMPLÉTER : ex. tilts sectoriels/asset-class par régime, overlay risk-parity, optimisation moyenne-variance sous contraintes macro]
- **Rebalancement :** [À COMPLÉTER : fréquence et gestion du turnover]
- **Benchmark :** [À COMPLÉTER : ex. S&P 500, portefeuille 60/40, portefeuille multi-actifs équipondéré]

## Résultats Principaux

[À COMPLÉTER : 2-3 conclusions concrètes. Si la stratégie a effectivement délivré les 4,5 % de surperformance mentionnés sur le CV, l'énoncer ici avec la fenêtre exacte et préciser si c'est brut ou en risque ajusté. Exemples :]

- La stratégie a surperformé le benchmark S&P 500 de 4,5 % en risque ajusté (avant frais) sur la période out-of-sample [À COMPLÉTER : dates]
- [À COMPLÉTER : ratio de Sharpe, drawdown maximum, taux de réussite]
- [À COMPLÉTER : quels régimes macro ont le plus / le moins contribué à la performance]

## Structure du Dépôt

```
├── these.pdf               # Mémoire complet
├── code/                   # Code d'analyse et de backtest
│   └── ...
└── README.md
```

## Environnement Technique

[À COMPLÉTER : langages et bibliothèques utilisés — ex. Python (pandas, numpy, bibliothèque de backtest), R, Excel/VBA. Si les backtests peuvent être reproduits à partir du code, le préciser ici.]

## Travaux Connexes

Un mémoire ultérieur, étendant ce framework avec des méthodes de statistical learning appliquées à l'allocation sectorielle actions, a été réalisé à NEOMA Business School en 2025 :
👉 [Statistical Learning for US Sectoral Equity Allocation](https://github.com/badreddinetahir0/sectoral-equity-allocation-neoma_thesis)

## Contact

**TAHIR Badr-eddine** — Portfolio & Fund Analyst, Natixis Investment Managers
📧 badr-eddine.tahir@dauphine.eu
🔗 [LinkedIn](https://www.linkedin.com/in/tahirbadr-eddine/)
