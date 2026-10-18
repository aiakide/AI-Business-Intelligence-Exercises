# 🧩 Übung — Objektorientierte Programmierung: Kundenverwaltung

**Kapitel 2 · Dauer: 45 Min · Python, keine externen Bibliotheken nötig**

## Ausgangslage

Der Kfz-Versicherer aus unserem roten Faden braucht eine kleine Softwarekomponente zur Verwaltung seiner Kunden. Bisher liegen Kundendaten nur verstreut in Tabellen — Heinz, der zuständige Entwickler, möchte sie stattdessen als Python-Objekte modellieren.

Jeder Kunde besitzt einen **Nachnamen** und einen **Vornamen**. Bei der Neuanlage eines Kunden wird automatisch eine eindeutige, fortlaufende **Kundennummer** vergeben (beginnend bei 1000) — diese darf sich im Nachhinein nicht mehr ändern. Außerdem führt jeder Kunde eine **Schadenshistorie**: eine Liste aller bisher gemeldeten Schadenshöhen (in EUR). Ein neu angelegter Kunde hat zunächst noch keine Schäden gemeldet.

Meldet ein Kunde einen neuen Schaden, wird der Betrag seiner Historie hinzugefügt. Für die Risikoprüfung will der Versicherer jederzeit den **durchschnittlichen Schaden** eines Kunden abfragen können sowie automatisch erkennen, ob ein Kunde **auffällig** ist — also im Schnitt Schäden oberhalb eines bestimmten Schwellenwerts meldet.

Der Versicherer übernimmt außerdem den kompletten Bestand eines alten Systems: eine CSV-Datei mit einer ganzen Liste bestehender Kunden (`bestandskunden.csv`, liegt neben dieser Übung). Diese sollen sich in einem Zug einlesen und als Objekte anlegen lassen, ohne jeden Kunden einzeln per Hand einzutippen.

Zur Kontrolle soll sich jeder Kunde außerdem lesbar ausgeben lassen. Eine mögliche Bildschirmausgabe sieht wie folgt aus (Zeilenumbrüche können variieren):

```
Kd.-Nr. 1000: Sauerland, Wilfried
Anzahl Schäden: 3, Ø Schadenshöhe: 2.450,00 EUR
Auffällig: Nein
```

## Aufgabe

Entwerfen und implementieren Sie eine passende Klassenlösung, die folgende Sachverhalte unterstützt:

- Anlage eines neuen Kunden mit Nachname und Vorname, inkl. automatischer, eindeutiger und nachträglich unveränderlicher Kundennummer
- Melden eines neuen Schadens für einen bestehenden Kunden
- Abfrage des durchschnittlichen Schadens eines Kunden
- Automatische Erkennung, ob ein Kunde auffällig ist (Durchschnitt oberhalb einer Schwelle, Standard 2.000 EUR)
- Einlesen des gesamten Kundenbestands aus `bestandskunden.csv` — für jede Zeile der Datei soll ein Kunde angelegt werden
- Lesbare Ausgabe eines Kunden wie im Beispiel oben

Schreiben Sie anschließend ein kurzes Testskript (ein paar Zeilen am Ende der Datei reichen), das:

- den gesamten Bestand aus `bestandskunden.csv` einliest und die Anzahl eingelesener Kunden ausgibt
- zeigt, dass die eingelesenen Kunden fortlaufende, eindeutige Kundennummern erhalten
- für mindestens einen Kunden mehrere Schäden meldet und anschließend Durchschnitt sowie Auffälligkeit ausgibt

**Nicht-funktionale Anforderungen:**

- Alle Attribute sind privat (führender Unterstrich, `self._name` statt `self.name`)
- Nachname und Vorname sollen nur über einen kontrollierten Zugriff (z. B. `@property`) lesbar/änderbar sein; die Kundennummer ist nur lesbar
- Die fortlaufende Nummerierung darf **nicht** über eine globale Variable außerhalb der Klasse gelöst werden

**Bonus, falls Zeit bleibt:** Ergänzen Sie eine Möglichkeit, den zuletzt gemeldeten Schaden eines Kunden wieder zu entfernen (z. B. bei einer irrtümlichen Meldung).

## Organisatorische Hinweise

- Reine Python-Bordmittel — keine Imports von NumPy/Pandas nötig
- Kein Abgabeformat vorgeschrieben — eine `.py`-Datei oder ein Notebook reicht
