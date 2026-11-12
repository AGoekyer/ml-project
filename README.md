# ML-Modell für Kickstarter-Projektgründer: Kann mein Projekt sein Finanzierungsziel erreichen?

In diesem Projekt versuchen wir vorherzusagen, ob ein Kickstarter-Projekt sein
Finanzierungsziel erreichen kann. Das Modell soll als Hilfe für die Einschätzung realistischer Projekt-Parameter dienen, 
die vor dem Start des Projekts festgelegt werden müssen.

## Ziel

- **Wer nutzt das Ergebnis?** Projektgründer einer Kickstarter-Kampagne.
- **Vorhersage:** erfolgreich (1) oder gescheitert (0), als
  Erfolgswahrscheinlichkeit.
- **Hauptmetrik:** ROC-AUC. Dazu F1, Precision und Recall.
- **Erfolgskriterium:** ROC-AUC von mindestens 0,75 (akzeptable Vorhersage) auf den Testdaten und
  klar besser als die Baseline.

## Daten

- **Datensatz:** [Kickstarter Projects (Kemical, 2018)](https://www.kaggle.com/datasets/kemical/kickstarter-projects)
- **Datei:** `ks-projects-201801.csv` (rund 379.000 Projekte, 15 Spalten)

## Ergebnisse

| Modell | ROC-AUC (Testdaten) | Accuracy | F1 |
|---|---|---|---|
| Baseline: logistische Regression (2 Features) | 0,671 | 63,6 % | 0,455 |
| **Random Forest (getunt)** | **0,749** | **69,0 %** | **0,576** |
  
- **Erfolgskriterium:** Das Ziel von 0,75 verfehlt das Modell auf den Testdaten knapp (0,749).
  Es ist aber klar besser als die Baseline.
- **Wichtigste Einflussfaktoren:** Finanzierungsziel, Kategorie, Dauer
  der Kampagne.
- **Grenzen:** Das Modell erkennt Misserfolge besser als Erfolge. 
Das Modell könnte durch das Einspielen weiterer Feature-Daten verbessert werden.

## Aufbau des Repositorys

| Datei / Ordner | Inhalt |
|---|---|
| [`data/`](data/) | Ablage für den Datensatz (nicht im Repository) |
| [`models/`](models/) | Das gespeicherte finale Modell (`random_forest_model.joblib`) |
| [`01_assignment.md`](01_assignment.md) | Die Aufgabenstellung aus der Original-Vorlage|
| [`02_kanban_board.md`](02-eda.ipynb) | Das Notebook mit Analyse und Modellen |

## Einrichtung

Voraussetzungen: [uv](https://docs.astral.sh/uv/getting-started/installation/)
ab Version 0.13.5 und Python 3.13 (siehe [`.python-version`](.python-version)).

**1. Repository klonen**

```bash
git clone <ssh-url-des-repositorys>
cd <name-des-repositorys>
```

**2. Abhängigkeiten installieren**

Dieser Befehl erstellt eine virtuelle Umgebung in `.venv/` und installiert
alle Pakete:

```bash
uv sync
```

**3. Daten ablegen**

Lege `ks-projects-201801.csv` in den Ordner `data/` (siehe oben).

**4. Notebook ausführen**

```bash
code .
```

> **Hinweis:** Das Hyperparameter-Tuning und die Permutation Importance
> dauern einige Minuten. Alle Ergebnisse sind reproduzierbar, weil überall
> derselbe Zufallswert (`RANDOM_STATE = 42`) genutzt wird.

## Bibliotheken

pandas, numpy, scikit-learn, matplotlib
