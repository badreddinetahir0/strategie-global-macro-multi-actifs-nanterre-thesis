# Implémentation d'une Stratégie d'Investissement Quantitative Global Macro Multi-Actifs

**Rapport de Projet de Fin d'Études — Filière Gestion Financière et Comptable, Université Paris Nanterre / Upline Capital Management**
**Auteur :** TAHIR Badr-eddine  |  **Encadrant pédagogique :** M. Sbai Hicham  |  **Encadrante professionnelle :** Mme Amrani Hanchi Wafae  |  **2022–2023**

---

## Résumé

Ce projet de fin d'études développe et implémente une stratégie d'investissement quantitative global macro multi-actifs, conçue pour surpasser les approches traditionnelles (portefeuille 60/40, gestion passive indicielle) dans des environnements de marché volatils et corrélés. En s'appuyant sur l'analyse des cycles macroéconomiques et la prévision d'indicateurs clés (PIB, IPC) via des modèles d'apprentissage automatique (LSTM), la stratégie identifie quatre régimes économiques — *Fire* (PIB↑, IPC↑), *Goldilocks* (PIB↑, IPC↓), *Stagflation* (PIB↓, IPC↑) et *Ice* (PIB↓, IPC↓) — et alloue dynamiquement un portefeuille d'ETFs américains (actions, obligations, matières premières) en fonction du régime détecté. Trois méthodes d'optimisation de portefeuille sont comparées : Mean-Variance, CVaR et Risk Parity. Les résultats montrent que la stratégie surperforme le S&P 500 (SPY) sur la période backtestée, avec un drawdown maximum significativement inférieur.

## Contexte

Ce travail a été réalisé dans le cadre d'un stage au sein du pôle gestion alternative chez **Upline Capital Management** (Casablanca, Maroc), filiale à 100 % du Groupe Banque Centrale Populaire. UCM gère environ 8 milliards de dollars d'actifs sous gestion. L'objectif était de développer une stratégie quantitative multi-actifs pour le desk de placements internationaux, capable de générer des rendements supérieurs à l'indice de référence, y compris dans des contextes de ralentissement économique.

## Données

- **Univers d'investissement :** ~70 ETFs américains couvrant actions (sectoriels, factoriels, large/mid/small cap), obligations (Treasuries, TIPS, IG corporate), matières premières (or, pétrole, agriculture, métaux) et instruments short (ProShares inverse ETFs)
- **Période :** Janvier 1999 – Juin 2023 (données mensuelles/trimestrielles)
- **Indicateurs macroéconomiques :** ISM PMI Manufacturing, PMI Services, Consumer Confidence (UMich, Conference Board), NFIB, Non-Farm Payrolls, Initial Claims, CPI, PPI, Retail Sales, Industrial Production, Housing Starts/Permits, M2, Fed Funds Rate, 10Y-2Y Treasury Spread, WTI, Gold, et d'autres
- **Sources :** Bloomberg, FactSet

## Méthodologie

Le pipeline se décompose en quatre étapes :

### 1. Sélection des indicateurs macroéconomiques
- Analyse de corrélation (seuil ≥ 0.4) entre les indicateurs et le PIB / IPC pour filtrer les variables les plus prédictives
- Régression linéaire simple pour valider la significativité statistique de chaque indicateur retenu
- Construction d'une grille de notation (scoring) transformant les valeurs des indicateurs en signaux directionnels sur le PIB et l'IPC

### 2. Prévision macroéconomique (LSTM)
- Modèle LSTM (Long Short-Term Memory) entraîné pour chaque indicateur macroéconomique sélectionné
- Variables explicatives spécifiques identifiées pour chaque indicateur via analyse de corrélation
- Prévisions glissantes sur 48 mois, évaluées sur MSE, RMSE, MAE et R²
- Les prévisions des indicateurs sont agrégées via la grille de notation pour produire un PIB et un IPC prévisionnels

### 3. Allocation d'actifs par régime
- Identification de quatre régimes économiques à partir des variations trimestrielles du PIB et de l'IPC prévisionnels :
  - **Fire** : PIB haussier + IPC haussier → surpondération actions cycliques, matières premières
  - **Goldilocks** : PIB haussier + IPC baissier → surpondération actions growth, obligations longues
  - **Stagflation** : PIB baissier + IPC haussier → surpondération énergie, short sur indices et immobilier
  - **Ice** : PIB baissier + IPC baissier → surpondération défensives, short sur cycliques et technologie
- Pour chaque régime, sélection des ETFs dont la performance historique dans ce régime dépasse leur moyenne et dont le ratio rendements positifs/négatifs est favorable
- Positions short via ETFs inverses (ProShares) pour les actifs sous-performants dans le régime détecté

### 4. Optimisation de portefeuille
Trois approches comparées pour la pondération des actifs sélectionnés :
- **Mean-Variance (MVO)** : portefeuille à variance minimale et portefeuille Max Sharpe, avec contraintes de poids entre 2 % et 8 % par actif
- **CVaR (Conditional Value-at-Risk)** : minimisation des pertes extrêmes au-delà du seuil de VaR
- **Risk Parity** : équilibrage de la contribution au risque de chaque actif

## Résultats Principaux

Performance des portefeuilles optimisés vs. le benchmark SPY (S&P 500), sur la période complète (janv. 1999 – juin 2023) :

| Approche | Rendement annualisé | Volatilité annualisée | Ratio de Sharpe | Max Drawdown |
|---|---|---|---|---|
| **Mean-Variance (Max Sharpe)** | **12,57 %** | 24,97 % | **0,34** | −19,37 % |
| **CVaR (Min Variance)** | 10,15 % | 21,68 % | 0,32 | −15,63 % |
| **Risk Parity** | 6,05 % | 12,50 % | 0,22 | **−8,27 %** |
| **SPY (Benchmark)** | 5,58 % | 26,30 % | 0,09 | −23,65 % |

**Principaux constats :**
- Les trois approches surperforment le benchmark SPY en rendement ajusté au risque (Sharpe supérieur)
- L'approche Mean-Variance Max Sharpe offre le meilleur rendement absolu (12,57 % vs 5,58 %) avec un Sharpe de 0,34 contre 0,09 pour le SPY
- L'approche Risk Parity offre la meilleure protection contre les baisses (max drawdown de −8,27 % contre −23,65 % pour le SPY) tout en maintenant un rendement supérieur au benchmark
- L'approche CVaR constitue un compromis entre rendement et gestion du risque extrême, avec un drawdown de −15,63 %
- L'allocation par régime permet de capter les tendances haussières tout en réduisant l'exposition lors des phases de contraction

## Structure du Dépôt

```
├── these.pdf               # Mémoire complet (en français)
├── code/                   # Code d'analyse et de backtest (Python)
│   └── ...
└── README.md
```

## Environnement Technique

Python 3, avec `pandas`, `numpy`, `keras`/`tensorflow` (LSTM), `scipy.optimize` (optimisation de portefeuille), `matplotlib`. Les backtests sont réalisés sur données trimestrielles avec rebalancement par régime.

## Travaux Connexes

Un mémoire ultérieur, étendant ce framework avec des méthodes de statistical learning appliquées à l'allocation sectorielle actions sur les 11 secteurs GICS, a été réalisé à NEOMA Business School en 2025 :
👉 [Statistical Learning for US Sectoral Equity Allocation](https://github.com/badreddinetahir0/sectoral-equity-allocation-neoma_thesis)

## Contact

**TAHIR Badr-eddine** — Portfolio & Fund Analyst, Natixis Investment Managers
📧 badr-eddine.tahir@dauphine.eu
🔗 [LinkedIn](https://www.linkedin.com/in/tahirbadr-eddine/)
