# ✅ Lösung — Statistik als Fundament

**Session 1 · Musterlösung mit vollständigem Rechenweg**

> Für Dozierende / Selbstkontrolle. Rundungen: 2–3 Nachkommastellen; kleine Abweichungen durch Rundung sind bei Studierenden zu akzeptieren.

---

## Aufgabe 1 — Lagemaße & Streuung

Daten: $0, 1, 1, 2, 2, 2, 3, 5$ ($n=8$, bereits sortiert)

**a) Lagemaße**

- $\bar{x} = \dfrac{0+1+1+2+2+2+3+5}{8} = \dfrac{16}{8} = 2$
- Median: $n=8$ (gerade) → Mittel der 4. und 5. sortierten Werte: $\dfrac{2+2}{2} = 2$
- Modus: $2$ (kommt 3× vor, häufigster Wert)

**b) Welches Lagemaß passt am besten?**

Mittelwert, Median und Modus sind hier zufällig identisch ($=2$) — ungewöhnlich, aber an diesem kleinen, moderat rechtsschiefen Datensatz (Ausreißer bei 5) so möglich. In der Praxis wäre bei stärkerer Schiefe der **Median** robuster, da er von dem Ausreißerwert 5 nicht verzerrt wird (der Mittelwert würde bei stärkerer Rechtsschiefe nach oben gezogen). Lehrpunkt: Studierende sollen erkennen, *warum* der Median hier robust ist, nicht nur den Wert nennen.

**c) Varianz & Standardabweichung**

Abweichungen vom Mittelwert (2): $-2, -1, -1, 0, 0, 0, 1, 3$
Quadrierte Abweichungen: $4, 1, 1, 0, 0, 0, 1, 9$ → Summe $= 16$

- Populationsvarianz: $\sigma^2 = \dfrac{16}{8} = 2$ → $\sigma = \sqrt{2} \approx 1{,}41$
- Stichprobenvarianz: $s^2 = \dfrac{16}{7} \approx 2{,}29$ → $s = \sqrt{2{,}29} \approx 1{,}51$

**d) Interpretation**

*"Im Schnitt melden unsere Versicherten etwa 2 Schäden pro Jahr, mit einer typischen Schwankung von rund 1,5 Schäden nach oben oder unten — die meisten liegen also zwischen 0 und 3,5 Schäden."*

---

## Aufgabe 2 — Kovarianz & Korrelation

| Fahrzeug | $x$ | $y$ | $x-\bar x$ | $y-\bar y$ | $(x-\bar x)(y-\bar y)$ |
|---|---|---|---|---|---|
| A | 2 | 620 | −4 | −580 | 2.320 |
| B | 4 | 850 | −2 | −350 | 700 |
| C | 6 | 1.300 | 0 | 100 | 0 |
| D | 8 | 1.400 | 2 | 200 | 400 |
| E | 10 | 1.830 | 4 | 630 | 2.520 |

**a)** $\bar{x} = \dfrac{30}{5} = 6$, $\bar{y} = \dfrac{6.000}{5} = 1.200$

**b)** $S_{xy} = 2.320+700+0+400+2.520 = 5.940$

**c) Kovarianz (Stichprobe)**

$$\text{cov}(x,y) = \frac{S_{xy}}{n-1} = \frac{5.940}{4} = 1.485$$

**d) $S_{xx}$, $S_{yy}$, Korrelationskoeffizient**

- $S_{xx} = (-4)^2+(-2)^2+0^2+2^2+4^2 = 16+4+0+4+16 = 40$
- $S_{yy} = 580^2+350^2+100^2+200^2+630^2 = 336.400+122.500+10.000+40.000+396.900 = 905.800$

$$r = \frac{S_{xy}}{\sqrt{S_{xx}\cdot S_{yy}}} = \frac{5.940}{\sqrt{40 \cdot 905.800}} = \frac{5.940}{\sqrt{36.232.000}} \approx \frac{5.940}{6.019{,}3} \approx 0{,}987$$

**e) Interpretation**

$r \approx 0{,}99$: ein sehr starker, **positiver** linearer Zusammenhang — ältere Fahrzeuge haben tendenziell höhere Reparaturkosten. Kausalität ist **nicht** belegt; Korrelation zeigt nur den statistischen Zusammenhang (denkbare Drittvariablen: Kilometerstand, Ersatzteilpreise für ältere Modelle).

---

## Aufgabe 3 — z-Transformation

**a) Populationsvarianz/-Standardabweichung von $y$**

$$\sigma_y^2 = \frac{S_{yy}}{n} = \frac{905.800}{5} = 181.160 \quad\Rightarrow\quad \sigma_y = \sqrt{181.160} \approx 425{,}63$$

**b) z-Werte** ($z_i = \frac{y_i - 1.200}{425{,}63}$)

| Fahrzeug | $y$ | $y-\bar y$ | $z$ |
|---|---|---|---|
| A | 620 | −580 | −1,363 |
| B | 850 | −350 | −0,822 |
| C | 1.300 | +100 | +0,235 |
| D | 1.400 | +200 | +0,470 |
| E | 1.830 | +630 | +1,480 |

**c)** Fahrzeug E hat mit $z \approx +1{,}48$ den auffälligsten Wert — seine Reparaturkosten liegen fast 1,5 Standardabweichungen über dem Durchschnitt, deutlich der teuerste Fall relativ zur Gesamtverteilung.

**d) Kontrollfrage**

Die Summe aller $z$-Werte muss (näherungsweise) **0** ergeben, da $z$ um den Mittelwert zentriert ist: $-1{,}363-0{,}822+0{,}235+0{,}470+1{,}480 \approx 0{,}000$ ✓ (kleine Abweichung nur durch Rundung).

---

## Aufgabe 4 — Lineare Regression von Hand

**a) Steigung & Achsenabschnitt**

$$b = \frac{S_{xy}}{S_{xx}} = \frac{5.940}{40} = 148{,}5$$

$$a = \bar y - b\bar x = 1.200 - 148{,}5 \cdot 6 = 1.200 - 891 = 309$$

**b) Regressionsgleichung**

$$\hat{y} = 309 + 148{,}5 \cdot x$$

**c) Vorhersage für $x=12$**

$$\hat{y} = 309 + 148{,}5 \cdot 12 = 309 + 1.782 = 2.091\ \text{EUR}$$

Der beobachtete Datenbereich reicht nur bis $x=10$ — bei $x=12$ **extrapoliert** das Modell außerhalb der Trainingsdaten. Die Vorhersage ist plausibel, aber weniger sicher als eine Interpolation innerhalb $[2,10]$; Studierende sollten diesen Vorbehalt benennen.

**d) $R^2$**

Da $R^2 = r^2$ für die einfache lineare Regression: $R^2 = 0{,}987^2 \approx 0{,}974$

*Interpretation für den Fachbereich:* "Etwa 97 % der Schwankungen in den Reparaturkosten lassen sich allein durch das Fahrzeugalter erklären — ein sehr starkes Modell für nur eine erklärende Variable."

---

## Aufgabe 5 — Logistische Regression & Odds Ratio

$z = -2{,}1 + 0{,}55x_1 + 0{,}9x_2$

**a) Tagsüber ($x_1=3, x_2=0$)**

$$z = -2{,}1 + 0{,}55\cdot 3 + 0{,}9\cdot 0 = -2{,}1+1{,}65 = -0{,}45$$
$$\hat p = \frac{1}{1+e^{0{,}45}} = \frac{1}{1+1{,}568} \approx 0{,}389 \;(38{,}9\%)$$

**b) Nachts ($x_1=3, x_2=1$)**

$$z = -2{,}1+1{,}65+0{,}9 = 0{,}45$$
$$\hat p = \frac{1}{1+e^{-0{,}45}} = \frac{1}{1+0{,}638} \approx 0{,}610 \;(61{,}0\%)$$

**c) Odds & Odds Ratio**

- Odds (tags) $= \dfrac{0{,}389}{1-0{,}389} = \dfrac{0{,}389}{0{,}611} \approx 0{,}637$
- Odds (nachts) $= \dfrac{0{,}610}{0{,}390} \approx 1{,}564$
- Odds Ratio $= \dfrac{1{,}564}{0{,}637} \approx 2{,}456$

**d) Vergleich mit $e^{\beta_2}$**

$$e^{0{,}9} \approx 2{,}460$$

Die beiden Werte stimmen (bis auf Rundung) überein — das bestätigt die Kerneigenschaft der logistischen Regression: $e^{\beta_j}$ liefert die Odds Ratio für Merkmal $j$ **direkt aus dem Koeffizienten**, ohne dass man zwei konkrete Fälle durchrechnen muss. Genau das macht die Koeffizienten interpretierbar.

---

## Aufgabe 6 (Bonus) — Signifikanz in der Praxis

**a) Entscheidungen bei $\alpha = 0{,}05$**

1. $p=0{,}002 < 0{,}05$ → H₀ **verwerfen** (Effekt signifikant)
2. $p=0{,}21 \geq 0{,}05$ → H₀ **beibehalten** (kein ausreichender Beweis für einen Effekt)
3. $p=0{,}03 < 0{,}05$ → formal H₀ **verwerfen** — aber siehe b)

**b) Was läuft in Fall 3 schief?**

Bei sehr großen Stichproben (hier 850.000 Verträge) werden selbst **winzige, praktisch irrelevante Effekte** statistisch signifikant, weil der Standardfehler mit wachsendem $n$ sinkt. Ein Effekt von 1,20 EUR ist für keine reale Entscheidung (Tarifierung, Rückstellungen) handlungsrelevant — trotz $p<\alpha$. Das ist der klassische Unterschied zwischen **statistischer Signifikanz** (ist der Effekt von Null unterscheidbar?) und **praktischer/ökonomischer Relevanz** (ist der Effekt groß genug, um etwas zu ändern?).

**c) Empfehlung an den Fachbereich**

Nicht allein auf $p$-Werte verlassen. Immer zusammen berichten: Effektgröße (wie groß, in EUR/Prozentpunkten?), Konfidenzintervall, Stichprobengröße und fachliche Plausibilität. Ein $p$-Wert beantwortet nur "ist da überhaupt etwas?", nicht "ist es wichtig genug, um zu handeln?".
