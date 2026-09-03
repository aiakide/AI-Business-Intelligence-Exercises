# 💻 Übung — Betrugserkennung klassifizieren

**Session 4 · Dauer: 30–60 Min · Von Hand oder mit Python — Deine Wahl**

## Ausgangslage

Du bist Analyst:in bei einem Kfz-Versicherer und sollst ein Betrugserkennungsmodell bewerten, bevor es produktiv geht. Bearbeite die drei Aufgaben in der angegebenen Reihenfolge. Aufgabe 4 ist ein Bonus, falls Zeit bleibt.

Empfohlen: Rechne mindestens Aufgabe 1 und 2 von Hand (Taschenrechner reicht) — das schärft das Verständnis für das, was später Scikit-Learn automatisiert.

---

## Aufgabe 1 — Confusion Matrix & Metriken von Hand (≈15 Min)

Ein neues Modell wurde an 20 Schadensfällen aus dem letzten Quartal getestet. Für jeden Fall liegt vor, was **tatsächlich** zutraf und was das **Modell vorhergesagt** hat:

| Fall | Tatsächlich | Modell sagt | Fall | Tatsächlich | Modell sagt |
|---|---|---|---|---|---|
| 1 | Betrug | Betrug | 11 | Kein Betrug | Kein Betrug |
| 2 | Kein Betrug | Kein Betrug | 12 | Kein Betrug | Kein Betrug |
| 3 | Kein Betrug | Kein Betrug | 13 | Betrug | Kein Betrug |
| 4 | Betrug | Kein Betrug | 14 | Kein Betrug | Betrug |
| 5 | Kein Betrug | Betrug | 15 | Betrug | Betrug |
| 6 | Kein Betrug | Kein Betrug | 16 | Kein Betrug | Kein Betrug |
| 7 | Betrug | Betrug | 17 | Kein Betrug | Kein Betrug |
| 8 | Kein Betrug | Kein Betrug | 18 | Betrug | Betrug |
| 9 | Kein Betrug | Betrug | 19 | Kein Betrug | Betrug |
| 10 | Betrug | Betrug | 20 | Kein Betrug | Kein Betrug |

**a)** Zähle die vier Ergebnis-Typen aus (TP, FN, FP, TN) und trage sie in eine 2×2-Confusion-Matrix ein. Mach einen Konsistenzcheck: Ergibt die Summe 20?

**b)** Berechne Accuracy, Precision, Recall und F1-Score.

**c)** Die Geschäftsleitung sagt: "70 % Accuracy ist doch schon ziemlich gut." Wie bewertest Du das angesichts von Precision und Recall? Was übersieht die Geschäftsleitung?

---

## Aufgabe 2 — KNN von Hand (≈20 Min)

Historische Schadensfälle mit zwei Merkmalen — Schadenhöhe (in Tsd. EUR) und Fahrzeugalter (in Jahren) — sowie ihrem bekannten Label:

| Fall | Schadenhöhe (Tsd. EUR) | Fahrzeugalter (Jahre) | Label |
|---|---|---|---|
| H1 | 2 | 1 | Legitim |
| H2 | 3 | 2 | Legitim |
| H3 | 15 | 8 | Betrug |
| H4 | 4 | 1 | Legitim |
| H5 | 18 | 9 | Betrug |
| H6 | 6 | 3 | Legitim |
| H7 | 16 | 7 | Betrug |
| H8 | 5 | 2 | Legitim |
| H9 | 17 | 10 | Betrug |
| H10 | 3 | 1 | Legitim |

Ein **neuer Schadensfall** hat Schadenhöhe = 14 (Tsd. EUR) und Fahrzeugalter = 7 Jahre.

**a)** Berechne die euklidische Distanz vom neuen Fall zu jedem der 10 historischen Fälle:

$$d = \sqrt{(x_{\text{neu}}-x_i)^2 + (y_{\text{neu}}-y_i)^2}$$

**b)** Sortiere die Fälle nach Distanz (aufsteigend) und bestimme die **5 nächsten Nachbarn** (K = 5).

**c)** Wende Majority Voting an: Wie klassifizierst Du den neuen Fall?

**d)** Kritisch reflektiert: Was würde bei **K = 3** passieren? Was bei **K = 9**? Rechne beide Fälle kurz durch und vergleiche die Ergebnisse mit c). Was lernst Du daraus über die Wahl von K?

---

## Aufgabe 3 — Business-Entscheidung: Recall vs. Precision (≈15 Min)

Zwei fertig trainierte Modelle stehen zur Wahl. Getestet auf denselben 500 Schadensfällen (davon 10 tatsächlich Betrug, 490 legitim):

**Kosten pro Fehler:** Unerkannter Betrug = EUR 15.000 Schaden · Falschalarm = EUR 500 (Untersuchung + Kundenverstimmung)

**Modell A (konservativ):** TP = 6, FN = 4, FP = 8, TN = 482

**Modell B (aggressiv):** TP = 9, FN = 1, FP = 40, TN = 450

**a)** Berechne für beide Modelle Recall und Precision.

**b)** Berechne für beide Modelle den Gesamtschaden (unerkannter Betrug + Falschalarme in EUR).

**c)** Welches Modell empfiehlst Du dem Versicherer? Begründe mit den Zahlen aus a) und b) — nicht nur mit "höhere Accuracy".

**d)** Angenommen, die Kosten pro Falschalarm steigen auf EUR 2.000 (z. B. weil jede Untersuchung künftig eine externe Gutachterprüfung auslöst). Ändert sich Deine Empfehlung? Rechne kurz nach.

---

## Aufgabe 4 (Bonus) — Welcher Algorithmus passt? (≈10 Min)

Ordne jedem Szenario den passenden Algorithmus zu (KNN, Random Forest, Gradient Boosting, CNN, NLP) und begründe in einem Satz.

1. Der Fachbereich will in wenigen Tagen ein erstes Betrugsmodell auf 300.000 historischen Verträgen (rein tabellarische Merkmale) testen — Trainingszeit und Stabilität sind wichtiger als die letzten paar Prozent Accuracy.
2. Für das Produktivsystem soll die bestmögliche Accuracy erzielt werden. Mehr Rechenzeit beim Training ist kein Problem, ein Validierungsset zur Überwachung steht bereit.
3. Ein:e Analyst:in will schnell 50 Großschadensfälle (> EUR 50.000) anhand weniger Merkmale nachvollziehbar klassifizieren, ganz ohne Modelltraining.
4. Schadensfotos sollen automatisch nach Beschädigungsart klassifiziert werden.
5. Freitext aus Schadensmeldungen soll automatisch nach Dringlichkeit sortiert werden.
