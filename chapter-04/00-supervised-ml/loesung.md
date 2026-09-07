# ✅ Lösung — Betrugserkennung klassifizieren

**Session 4 · Musterlösung mit vollständigem Rechenweg**

> Für Dozierende / Selbstkontrolle. Rundungen: 2–3 Nachkommastellen; kleine Abweichungen durch Rundung sind bei Studierenden zu akzeptieren.

---

## Aufgabe 1 — Confusion Matrix & Metriken von Hand

**a) Confusion Matrix**

Auszählen der 20 Fälle:

| | Modell: Betrug | Modell: Kein Betrug |
|---|---|---|
| **Wirklich: Betrug** | TP = 5 (Fälle 1, 7, 10, 15, 18) | FN = 2 (Fälle 4, 13) |
| **Wirklich: Kein Betrug** | FP = 4 (Fälle 5, 9, 14, 19) | TN = 9 (Fälle 2, 3, 6, 8, 11, 12, 16, 17, 20) |

Konsistenzcheck: $5+2+4+9 = 20$ ✓

**b) Metriken**

$$\text{Accuracy} = \frac{TP+TN}{TP+TN+FP+FN} = \frac{5+9}{20} = \frac{14}{20} = 0{,}70 = 70{,}0\%$$

$$\text{Precision} = \frac{TP}{TP+FP} = \frac{5}{9} \approx 0{,}556 = 55{,}6\%$$

$$\text{Recall} = \frac{TP}{TP+FN} = \frac{5}{7} \approx 0{,}714 = 71{,}4\%$$

$$F_1 = 2 \cdot \frac{P \cdot R}{P+R} = 2 \cdot \frac{0{,}556 \times 0{,}714}{0{,}556+0{,}714} \approx 0{,}625 = 62{,}5\%$$

**c) Einordnung für die Geschäftsleitung**

70 % Accuracy klingt solide, verdeckt aber zwei unterschiedliche Schwächen: Von den 9 Fällen, die das Modell als "Betrug" markiert, sind nur 5 (55,6 %) wirklich Betrug — **fast jeder zweite Alarm ist ein Fehlalarm**. Und von den 7 tatsächlichen Betrugsfällen erkennt das Modell nur 5 (71,4 %) — **gut jeder vierte Betrugsfall bleibt unentdeckt**. Die Geschäftsleitung übersieht, dass Accuracy beide Fehlerarten (Fehlalarm vs. übersehener Betrug) zu einer Zahl verdichtet, obwohl sie geschäftlich sehr unterschiedliche Kosten verursachen (siehe Aufgabe 3).

---

## Aufgabe 2 — KNN von Hand

**a) Euklidische Distanzen zum neuen Fall (14, 7)**

| Fall | $x$ | $y$ | $(14-x)^2$ | $(7-y)^2$ | Summe | $d$ | Label |
|---|---|---|---|---|---|---|---|
| H1 | 2 | 1 | 144 | 36 | 180 | 13,416 | Legitim |
| H2 | 3 | 2 | 121 | 25 | 146 | 12,083 | Legitim |
| H3 | 15 | 8 | 1 | 1 | 2 | 1,414 | Betrug |
| H4 | 4 | 1 | 100 | 36 | 136 | 11,662 | Legitim |
| H5 | 18 | 9 | 16 | 4 | 20 | 4,472 | Betrug |
| H6 | 6 | 3 | 64 | 16 | 80 | 8,944 | Legitim |
| H7 | 16 | 7 | 4 | 0 | 4 | 2,000 | Betrug |
| H8 | 5 | 2 | 81 | 25 | 106 | 10,296 | Legitim |
| H9 | 17 | 10 | 9 | 9 | 18 | 4,243 | Betrug |
| H10 | 3 | 1 | 121 | 36 | 157 | 12,530 | Legitim |

**b) Sortiert nach Distanz (aufsteigend)**

1. H3 (1,414, Betrug)
2. H7 (2,000, Betrug)
3. H9 (4,243, Betrug)
4. H5 (4,472, Betrug)
5. H6 (8,944, Legitim)
6. H8 (10,296, Legitim)
7. H4 (11,662, Legitim)
8. H2 (12,083, Legitim)
9. H10 (12,530, Legitim)
10. H1 (13,416, Legitim)

Die **5 nächsten Nachbarn** (K = 5): H3, H7, H9, H5, H6.

**c) Majority Voting (K = 5)**

4 von 5 Nachbarn (H3, H7, H9, H5) sind "Betrug", nur 1 (H6) ist "Legitim" → Modell klassifiziert den neuen Fall als **Betrug**.

**d) K = 3 vs. K = 9**

- **K = 3:** nächste drei Nachbarn sind H3, H7, H9 — alle "Betrug" → 3/3 → **Betrug**. Gleiches Ergebnis wie bei K = 5, sogar eindeutiger.
- **K = 9:** alle Fälle außer dem am weitesten entfernten H1 fließen ein. Davon sind H3, H7, H9, H5 "Betrug" (4) und H6, H8, H4, H2, H10 "Legitim" (5) → Mehrheit **Legitim** — die Klassifikation **kippt**!

**Lehrpunkt:** Die Wahl von K ist keine Nebensächlichkeit. Ein zu kleines K (hier K = 3) folgt nur dem unmittelbaren lokalen Muster (hier eindeutig, aber bei verrauschten Daten anfällig für Ausreißer). Ein zu großes K (hier K = 9) zieht weit entfernte, weniger relevante Nachbarn hinzu und kann die Entscheidung "verwässern" bzw. sogar umkehren — hier, weil die 10 historischen Fälle stark in zwei Cluster (kleine/junge vs. große/alte Schäden) zerfallen und K = 9 praktisch fast den gesamten Datensatz einbezieht, statt nur die wirklich ähnlichen Nachbarn.

---

## Aufgabe 3 — Business-Entscheidung: Recall vs. Precision

**a) Recall & Precision**

Modell A: $\text{Recall} = \frac{6}{10} = 60\%$, $\text{Precision} = \frac{6}{14} \approx 42{,}9\%$

Modell B: $\text{Recall} = \frac{9}{10} = 90\%$, $\text{Precision} = \frac{9}{49} \approx 18{,}4\%$

**b) Gesamtschaden**

Modell A: $4 \times 15.000 + 8 \times 500 = 60.000 + 4.000 = \text{EUR } 64.000$

Modell B: $1 \times 15.000 + 40 \times 500 = 15.000 + 20.000 = \text{EUR } 35.000$

**c) Empfehlung**

Trotz der deutlich niedrigeren Precision (18,4 % vs. 42,9 %) verursacht **Modell B den geringeren Gesamtschaden** (EUR 35.000 vs. EUR 64.000), weil unerkannter Betrug (EUR 15.000) 30× teurer ist als ein Falschalarm (EUR 500). Die vielen zusätzlichen Fehlalarme von Modell B (40 statt 8) fallen finanziell kaum ins Gewicht gegen den einen zusätzlichen übersehenen Betrugsfall, den sich Modell A leistet. Empfehlung: **Modell B**, sofern die Fehlalarme organisatorisch (Kapazität für Nachprüfungen) verkraftbar sind.

**d) Sensitivität bei höheren Falschalarm-Kosten (EUR 2.000 statt EUR 500)**

Modell A: $4 \times 15.000 + 8 \times 2.000 = 60.000 + 16.000 = \text{EUR } 76.000$

Modell B: $1 \times 15.000 + 40 \times 2.000 = 15.000 + 80.000 = \text{EUR } 95.000$

Die Empfehlung **kippt**: Jetzt ist **Modell A** günstiger (EUR 76.000 vs. EUR 95.000), weil die vielen Fehlalarme von Modell B bei gestiegenen Fehlalarmkosten stärker ins Gewicht fallen als der eine zusätzliche unerkannte Betrugsfall. **Lehrpunkt:** Die "richtige" Precision/Recall-Balance ist keine feste Eigenschaft eines Modells, sondern hängt vollständig von den aktuellen Kostenannahmen ab — ändern sich die Kosten, ändert sich die optimale Wahl.

---

## Aufgabe 4 (Bonus) — Welcher Algorithmus passt?

1. **Random Forest** — große tabellarische Datenmenge, schnelle robuste Baseline ohne aufwendiges Hyperparameter-Tuning ist wichtiger als die letzten Prozentpunkte Accuracy.
2. **Gradient Boosting (XGBoost)** — Accuracy-Fokus, Rechenzeit ist kein Hindernis, Validation Set zur Überwachung des Overfitting-Risikos ist vorhanden — genau das Szenario, für das Boosting seinen Mehraufwand rechtfertigt.
3. **k-Nearest Neighbors (KNN)** — kleines, strukturiertes Feature-Set, kein Trainingsaufwand nötig (Lazy Learning), für eine überschaubare Fallzahl (50 Großschäden) gut geeignet.
4. **Convolutional Neural Network (CNN)** — Bilddaten (Schadensfotos) erfordern ein Verfahren, das räumliche Muster erkennt; kommt in Kapitel 6 (Deep Learning).
5. **Natural Language Processing (NLP)** — Freitext erfordert Sprachverarbeitung (Tokenisierung, Semantik); kommt in Kapitel 7.
