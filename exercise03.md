## Übungsaufgaben zu Kapitel 3
#### Übungsaufgabe 3.1
> Sie hängen an Ihr altes Passwort eine 1 an. Wie verändert sich der Hash-Wert?

- Hash-Wert ändert sich komplett (durch Streueigenschaft der Funktion)

> Wie viele verschiedene Passwörter gibt es pro Hash-Wert?

- Unendlich viele Passwörter pro Hash

> Wie viele verschiedene Hash-Werte gibt es pro Passwort?

- Ein Hash pro Passwort (Funktion)

> Sie signieren einen Vertrag mittels kryptografischer Hash-Funktion und hinterlegen den Hash bei einem
  Notar. Kann Ihr Vertragspartner den Vertrag (sinnvoll) modifizieren ohne dass es bemerkt würde?

- Nein, denn ein anderer Vertrag ändert im Normalfall den Hash-Wert
- Bei Kollision (gleicher Hash-Werte) schwierig zu finden, insbesondere wenn Vertrag sinnvoll sein soll
  
> Der Vertragspartner behauptet, Sie hätten den Vertrag signiert. Sie selbst sagen, sie wären es nicht gewesen.
  Kann Ihr Vertragspartner seinen Standpunkt beweisen?
  
- Nein, da Hash-Funktion zur Erkennung von Modifikationen gebraucht werden, nicht aber zur Authentizität
  
---
  
#### Übungsaufgabe 3.2
> Warum stellen One-Time Pads einen Unbreakable Code dar? 
Wie würde eine Brute-Force Attacke aussehen? (Bsp. 200 ASCII-Zeichen mit je 7 Bits kodiert -> 1400 Bit langer Einwegcode)

- Angreifer probiert alle 1400 Bit langen Schlüssel aus
- Suche nach sinnvollen ASCII-Texten

> Was sieht der Angreifer als Resultat seiner Attacke?

- Richtiger Text `Klausuraufgabe 1: Viren...` wird gefunden
- Aber auch:
  - `Klausuraufgabe 1: Würmer...`
  - `Klausuraufgabe 1: Subnetting...`
- Alle sinnvollen ASCII-Texte mit einer Länge von 200 Buchstaben werden gefunden
- Angreifer weiß nicht, welcher Text der richtige ist

---

#### Übungsaufgabe 3.3

> Eine Unternehmen verwendet zur Zutrittskontrolle des Gebäudes ein biometrisches Authentifizierungssystem, das mit
  Gesichtserkennung arbeitet (Verfahren weist Fehlerraten FAR = 0,08 % und FRR = 4 % auf).
  
> Welche dieser Fehlerraten ist sicherheitsrelevant?

- Die FAR ist sicherheitsrelevant, da Personen Zugang erlangen können, die keinen haben sollten
- FRR sollte auch niedrig sein, da sonst keine ausreichende Benutzerakzeptanz vorhanden

> Jeden Tag betreten 500 berechtigte und erfasste Personen das Gebäude. Wie viele von ihnen werden vom verwendeten
  biometrischen System im Schnitt abgewiesen?
  
- 4 % * 500 = 20 Personen werden im Schnitt fälschlich abgewiesen
  
> Welcher Schwellwert ist bei obigen Fehlerraten eingestellt?

- Schwellwert liegt bei ca. 0,8

> Wie hoch ist die EER (Equal-Error-Rate) ungefähr?

- EER bei Empfindlichkeit von 0,3 (0,7 % FAR / FRR)
