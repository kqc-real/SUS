# SUS Analyse

Dieses Verzeichnis enthält ein Jupyter Notebook zur Berechnung und Interpretation des System Usability Scale (SUS).

Kurzüberblick

- `SUS-Analyse.ipynb` — Haupt-Notebook: lädt einen Google‑Forms CSV‑Export (oder eine synthetische CSV), mappt Spalten zu Q1..Q10, normalisiert die Items, berechnet pro‑Proband SUS‑Scores (0–100), gibt Interpretationen aus und erzeugt ein interpretatives Verteilungsdiagramm.
- `sus_google_forms_export.csv` — Beispiel/Beispieldaten, wird vom Notebook ggf. erzeugt oder eingelesen.
- `sus_score_distribution_interpreted.png` — vom Notebook erzeugtes Interpretations‑Plot (Histogramm + Interpretationsbänder).

Wesentliches

- Normalisierung: Positive Items (Q1, Q3, Q5, Q7, Q9): normalisierter Wert = Antwort − 1; Negative Items (Q2, Q4, Q6, Q8, Q10): normalisierter Wert = 5 − Antwort. Ergebnis: 10 Werte 0–4 → Summe 0–40 → ×2.5 → SUS 0–100.
- 
- Interpretation (konventionelle Schwellen, Sauro & Lewis):
  - < 51: Inakzeptabel (F)
  - 51–67.99: Marginal (D)
  - 68–73.99: OK (C)
  - 74–80.29: Gut (B)
  - ≥ 80.3: Exzellent (A)

Wie man das Notebook benutzt (lokal)

1. Öffne das Notebook in JupyterLab / Jupyter Notebook oder Visual Studio Code (mit Jupyter‑Extension).
2. Wenn du reale Google‑Forms‑Daten verwendest: exportiere die Antworten als CSV und speichere sie als `sus_google_forms_export.csv` im selben Ordner wie das Notebook. Das Notebook versucht automatisch, Spalten zu mappen (robuster Mapping‑Fallback ist implementiert).
3. Alternativ: starte die Zelle, die `generate_synthetic_sus_csv(n=..., mean=..., sd=...)` aufruft, um eine synthetische Testdatei zu erzeugen.
4. Führe die Zellen sequentiell aus (Importe → Generator/CSV → Mapping → Berechnung → Plot). Die wichtigsten Zellen sind kommentiert.

Kurze Terminal-Befehle (optional)

- Notebook automatisiert ausführen und Ergebnis speichern (erfordert `jupyter`):

```bash
jupyter nbconvert --to notebook --execute SUS-Analyse.ipynb --inplace --ExecutePreprocessor.timeout=600
```

Abhängigkeiten

- Python 3.10+ empfohlen
- Benötigte Pakete (im Notebook importiert): `pandas`, `numpy`, `seaborn`, `matplotlib`, `pathlib`, `re`.
- In der bereitgestellten Notebook‑Kernelumgebung sind viele Pakete bereits installiert. Verwende bei Bedarf ein virtuelles Environment und installiere fehlende Pakete mit pip/conda.

Output / Artefakte

- `sus_google_forms_export.csv` — Eingabe/Beispieldaten (kann vom Generator überschrieben werden)
- `sus_score_distribution_interpreted.png` — Visualisierung mit Interpretationsbändern

Weiteres / Hinweise

- Standardmäßig werden Zeilen mit fehlenden Antworten in Q1..Q10 entfernt (`dropna`). Alternativ ist "Imputation" möglich — kurz: fehlende Item‑Werte werden durch plausibel geschätzte Ersatzwerte ersetzt (z. B. Pro‑Rating: Hochskalierung der beantworteten Items auf 10 Items; oder Multiple Imputation zur Berücksichtigung von Unsicherheit).
- Beispiele/Empfehlung:
  - Wenig fehlende Items (z. B. ≤1 pro Proband): Pro‑Rating (schnell, praktikabel).
  - Mehrere fehlende Items oder viele betroffene Fälle: Multiple/Iterative Imputation (z. B. MICE) oder Datenqualitätsmaßnahme.
  - Die konkrete Methode sollte dokumentiert werden; das Notebook implementiert Imputation nicht automatisch.
- Das Notebook enthält eine robuste `mappe_spaltennamen()` Funktion, die versucht, lange Google‑Forms‑Fragetexte auf Q1..Q10 zu mappen. Anpassungen sind möglich, falls deine Formulierungen stark abweichen.

Kontakt

- Bei Fragen oder Änderungswünschen: beschreibe kurz, welche Ausgabe oder welches Verhalten du ändern möchtest.
