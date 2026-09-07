# 💻 Übung — Statistik als Fundament

**Session 1 · Dauer: 30–60 Min · Von Hand oder mit Python — Deine Wahl**

## Ausgangslage

Du arbeitest als Analyst:in bei einem Kfz-Versicherer. Bevor Dein Team Machine-Learning-Modelle auf hunderttausende Verträge loslässt, sollst Du an zwei kleinen Beispieldatensätzen zeigen, dass Du die statistischen Grundlagen dahinter verstehst.

Empfohlen: Rechne mindestens die erste Aufgabe von Hand (Taschenrechner reicht) — das schärft das Verständnis für das, was später Python automatisiert. Ab dann steht es Dir frei, mit Python (z. B. NumPy/SciPy) nachzurechnen und Deine Handrechnung zu verifizieren.

Bearbeite die Aufgaben in der angegebenen Reihenfolge. Aufgabe 5 ist ein Bonus, falls Zeit bleibt.

---

## Aufgabe 1 — Lagemaße & Streuung (≈10 Min)

Ein Team hat die **Anzahl gemeldeter Schäden im letzten Jahr** von 8 zufällig ausgewählten Versicherten erfasst:

$$0,\ 1,\ 1,\ 2,\ 2,\ 2,\ 3,\ 5$$

**a)** Berechne das arithmetische Mittel, den Median und den Modus.

**b)** Welches Lagemaß beschreibt die "typische" Schadenhäufigkeit hier am besten? Begründe kurz — beachte den Wert 5 am rechten Rand der Verteilung.

**c)** Berechne die Stichprobenvarianz $s^2 = \dfrac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2$ und die Standardabweichung $s$.

**d)** Was bedeutet die Standardabweichung hier inhaltlich, in einem Satz an einen Fachbereichsleiter ohne Statistik-Hintergrund formuliert?

---

## Aufgabe 2 — Kovarianz & Korrelation (≈10 Min)

Für 5 Fahrzeuge liegen Alter (in Jahren) und die zuletzt abgerechneten Reparaturkosten (in EUR) vor:

| Fahrzeug | Alter $x$ (Jahre) | Reparaturkosten $y$ (EUR) |
|---|---|---|
| A | 2 | 620 |
| B | 4 | 850 |
| C | 6 | 1.300 |
| D | 8 | 1.400 |
| E | 10 | 1.830 |

**a)** Berechne $\bar{x}$ und $\bar{y}$.

**b)** Stelle eine Tabelle mit den Abweichungen $(x_i - \bar{x})$, $(y_i - \bar{y})$ und ihrem Produkt auf. Summiere die Produkte — das ist der Zähler der Kovarianz-Formel.

**c)** Berechne die Kovarianz $\text{Cov}(x,y) = \dfrac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})$.

**d)** Berechne zusätzlich die Stichprobenvarianzen $s_x^2$ und $s_y^2$ (gleiche Formel wie in Aufgabe 1c, einmal für $x$, einmal für $y$), und daraus den Pearson-Korrelationskoeffizienten $r = \dfrac{\text{Cov}(x,y)}{s_x \cdot s_y}$.

**e)** Interpretiere $r$: Richtung und Stärke des Zusammenhangs. Ist Kausalität belegt?

> Behalte $\text{Cov}(x,y)$ und $s_x^2$ — Du brauchst beide in Aufgabe 4 wieder.

---

## Aufgabe 3 — z-Transformation (≈8 Min)

Nutze weiterhin den Datensatz aus Aufgabe 2 (Reparaturkosten $y$) und die Standardabweichung $s_y$, die Du dort in Teilaufgabe d) berechnet hast.

**a)** Standardisiere jeden der 5 Reparaturkosten-Werte mit $z_i = \dfrac{y_i - \bar{y}}{s_y}$.

**b)** Welches Fahrzeug hat den auffälligsten (am weitesten von 0 entfernten) $z$-Wert? Was sagt das über diesen Fall aus?

**c)** Kontrollfrage: Was sollte die Summe aller $z$-Werte (näherungsweise) ergeben? Prüfe das an Deinem Ergebnis.

---

## Aufgabe 4 — Lineare Regression von Hand (≈15 Min)

Weiter mit dem Datensatz und den Zwischenergebnissen aus Aufgabe 2.

**a)** Berechne die Steigung $b = \dfrac{\text{Cov}(x,y)}{s_x^2}$ und den Achsenabschnitt $a = \bar{y} - b\bar{x}$ (Methode der kleinsten Quadrate, OLS).

**b)** Formuliere die Gleichung der Regressionsgeraden $\hat{y} = a + bx$.

**c)** Ein sechstes Fahrzeug ist 12 Jahre alt. Sage die erwarteten Reparaturkosten voraus. Bewegt sich diese Vorhersage noch innerhalb des beobachteten Datenbereichs, oder handelt es sich um eine Extrapolation?

**d)** Bestimme für jedes der 5 Fahrzeuge den vorhergesagten Wert $\hat{y}$ und das Residuum $(y - \hat{y})$, und summiere die quadrierten Residuen zu $SS_{\text{res}} = \sum(y-\hat{y})^2$. $SS_{\text{tot}}$ hast Du bereits in Aufgabe 2b berechnet — es ist die Summe der quadrierten Abweichungen von $\bar{y}$. Berechne daraus $R^2 = 1 - \dfrac{SS_{\text{res}}}{SS_{\text{tot}}}$ und interpretiere den Wert für einen Fachbereich, der nicht weiß, was $R^2$ ist.

---

## Aufgabe 5 — Logistische Regression & Odds Ratio (≈10 Min)

Das Data-Science-Team hat bereits ein Betrugsmodell trainiert (die Koeffizienten sind gegeben, Du musst sie **nicht** selbst schätzen):

$$z = -2{,}1 + 0{,}55 \cdot x_1 + 0{,}9 \cdot x_2$$

wobei $x_1$ = Anzahl Vorschäden, $x_2$ = Schadenmeldung nachts eingegangen (1 = ja, 0 = nein).

**a)** Berechne $\hat{p}$ für einen Kunden mit 3 Vorschäden, der **tagsüber** meldet ($x_2=0$), mit der Sigmoid-Funktion $\hat{p} = \dfrac{1}{1+e^{-z}}$.

**b)** Berechne $\hat{p}$ für denselben Kunden, wenn er stattdessen **nachts** meldet ($x_2=1$).

**c)** Berechne für beide Fälle die Odds ($\frac{\hat p}{1-\hat p}$) und das Verhältnis der beiden Odds zueinander (Odds Ratio).

**d)** Vergleiche Dein Ergebnis aus c) mit $e^{\beta_2} = e^{0{,}9}$. Stimmen die Werte überein? Was sagt das über die Interpretierbarkeit von Odds Ratios aus?

---

## Aufgabe 6 (Bonus) — Signifikanz in der Praxis (≈10 Min)

Drei Kolleg:innen präsentieren Dir ihre Ergebnisse. $\alpha = 0{,}05$ ist die vereinbarte Schwelle.

1. *"Fahrzeugalter beeinflusst die Reparaturkosten, $p = 0{,}002$."*
2. *"Die Farbe des Fahrzeugs beeinflusst die Schadenhäufigkeit, $p = 0{,}21$."*
3. *"Bei 850.000 Verträgen beeinflusst das Geburtsdatum (Wochentag) die Schadenhöhe minimal, aber signifikant, $p = 0{,}03$. Der Effekt liegt bei 1,20 EUR."*

**a)** Triff für jede Aussage die Entscheidung: H₀ verwerfen oder beibehalten?

**b)** Fall 3 ist ein Sonderfall. Was läuft hier schief, obwohl der $p$-Wert unter $\alpha$ liegt? (Stichwort: Effektgröße vs. statistische Signifikanz, Stichprobengröße)

**c)** Was würdest Du dem Fachbereich empfehlen: Soll man sich bei Entscheidungen allein auf $p$-Werte verlassen? Begründe in 2–3 Sätzen.
