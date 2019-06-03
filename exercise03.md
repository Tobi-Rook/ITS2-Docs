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

---

#### Übungsaufgabe 3.4
> In einem Unternehmen arbeiten vier Mitarbeiter mit folgenden MAC-Kategorien bzw. Vertraulichkeitsstufen:

Person | MAC-Kategorie | Vertraulichkeitsstufe
:---: | :---: | :---:
**Fred** | Engineering | Geheim
| | Product X | Streng Geheim
**James** | Managers | Geheim
| | Produkt X | Vertraulich
**Walter** | Engineering | Vertraulich
**Bill** | Managers | Vertraulich
| | Salary | Geheim

> Folgende Dateien gibt es:

Datei | MAC-Kategorie | Vertraulichkeitsstufe
:---: | :---: | :---:
`Switch-Config.doc` | Engineering | Vertraulich
`Firewall-Config.doc` | Engineering | Streng Geheim
`Product-X-Requirements.xls` | Product X | Geheim
`Product-X-Photo.jpg` | Product X | Öffentlich
`Company-Strategy.doc` | Managers | Geheim
`Management-Planning.doc` | Managers | Vertraulich

##### Lösung
Datei | Person
:---: | :---:
`Switch-Config.doc` | Fred, Walter
`Firewall-Config.doc` | Niemand
`Product-X-Requirements.xls` | Fred
`Product-X-Photo.jpg` | Jeder
`Company-Strategy.doc` | James
`Management-Planning.doc` | James, Bill

---

#### Übungsaufgabe 3.6
>  Wie viele Signaturen müssen jeweils (bei PKI mit Wurzel `A`) geprüft werden, um die Echtheit des öffentlichen 
Schlüssels von `E` bzw. `G` zu prüfen?

- Knoten `E`
  - `D` *- bestätigt >* `E`
  - `B` *- bestätigt >* `D`
  - `A` *- bestätigt >* `B`
- Knoten `G`
  - `C` *- bestätigt >* `G`
  - `A` *- bestätigt >* `C`
   
> Wie viele öffentliche Schlüssel muss der Browser mit und ohne diese Hierarchie speichern, um die Schlüssel 
aller Knoten des Baums (mit Wurzel `A`) verifizieren zu können?

- 7 Knoten im Baum
  - Ohne PKI müssten die öffentlichen Schlüssel aller Knoten gespeichert werden
  - Mit PKI muss nur die Wurzel `A` gespeichert werden
  
> Überlegen Sie sich Methoden, die es ermöglichen würden, dass jeder Benutzer des einen Baums jeden Benutzer 
des anderen Baums verifizieren kann.

- Wurzeln untereinander prüfen lassen
  - Cross-Zertifizierung zwischen `A` und `H`
- Einfügen einer gemeinsamen Wurzel bzw. Bridge Trust Center
- Alle Zertifikate der Wurzeln speichern

---

#### Übungsaufgabe 3.7
> Der Server verwendet normalerweise weitere Records wie [ServerCertificate], [CertificateRequest], [ServerKeyExchange], 
ServerHelloDone, ChangeCipherSpec, Finished. 
Wo sind diese abgeblieben?

- Verkürzter TLS-Handshake wird verwendet, da eine Sitzung wiederaufgenommen wird
- `Finished` verborgen durch `Change Cipher Spec`