## Übungsaufgaben zu Kapitel 2
#### Übungsaufgabe 2.3
Abschnitt | Advanced Persistent Threat | Commodity Threats
:---: | :---: | :---:
**Define Target** | Wen angreifen? | Egal
**Accomplices** | Komplexe Angriffe -> Expertise | zu viel Aufwand
**Tools** | Automatisierung | Automatisierung
**Infrastructure & employees** | Schwachstellen bei bestimmtem Ziel feststellen | Standardschwachstelle wird ausgenutzt
**Test for detection** | Angreifer möchte unentdeckt bleiben | Angreifer möchte unentdeckt bleiben
**Deployment** | Zusammensetzen des Angriffs | Zusammensetzen des Angriffs
**Initial intrusion** | Starten des Angriffs | Starten des Angriffs
**Outbound connection initiated** | Zugriff von außen ermöglichen | Zugriff von außen ermöglichen
**Expand access & credentials** | Ausweiten in Richtung eigentliches Ziel | Ziel bereits erreicht
**Strengthen foothold** | Dauerhaft etablieren | -
**Exfiltrate data** | Häufiges Spionageziel | ?
**Cover tracks and remain undetected** | Möglichst lange infizieren | -

---

#### Übungsaufgabe 2.4
> Wie sieht ein Idlescan aus, wenn der Port geschlossen ist?
- Schritt 1
  - SYN / ACK-Paket wird an Zombie gesendet
  - Zombie antwortet mit RST (und IPID)
- Schritt 2
  - SYN-Paket mit Port (spoofed source address) an zu scannenden Port senden
  - Ziel sendet RST an Zombie
- Schritt 3
  - SYN / ACK-Paket wird an Zombie gesendet
  - Zombie antwortet mit RST (nur einmal inkrementiert)
  
---

#### Übungsaufgabe 2.5
> Warum ist das Anhängen des Virus schwieriger als das einfache Überschreiben?

- Überschreiben der ersten Bytes des Original-Codes (Jump)
  - entsprechende Bytes retten (kopieren ans Ende)
  - später zurückkopieren
- Die kompilierten (nicht relativen) Adressen des Virus müssen gemäß Offset angepasst werden

> Wie ändert sich die Problematik wenn der Code vor das Wirtsprogramm geschrieben wird (prepending)
und was sind mögliche Lösungen?

- Prepending (umgekehrtes Problem)
  - Adressen im Viruscode unproblematisch
  - Adressen im Originalcode müssen angepasst werden (Offset des Virencodes)
  
---

#### Übungsaufgabe 2.6
> Skizzieren Sie den Prepending-Virus.

Header | Virus | Original
--- | --- | ---

- Einsprung von Header auf Virus
- Länge: `L + X`

> Skizzieren Sie den EPO-Virus.

Header | Original (mit Jump Virus) | Virus | gerettete Bytes (Jump)
--- | --- | --- | ---

- Einsprung im Original-Code
- Anhängen der ersetzten Bytes vom Original an das Ende des Programms

> Wie häufig wird ein Prepending-Virus aufgerufen (pro infizierter Datei)?

- Einmal, sofern das Original sich nicht selbst aufruft.

> Wie häufig wird ein EPO-Virus aufgerufen (pro infizierter Datei)?

- Eventuell gar nicht, weil der Programmteil nicht ausgeführt wird.
- Maximal einmal, da in erstem Durchlauf Jump-Byte mit Original-Code überschrieben wird.

> Was sind die daraus resultierenden Vor- und Nachteile des EPO-Virus?

Vorteil | Nachteil
:---: | :---:
Schwieriger zu erkennen | Wird eventuell nicht ausgeführt

---

#### Übungsaufgabe 2.7
> Was ist der Unterschied zwischen einem Virus und einem Wurm?

Aspekt | Viren | Würmer
:---: | :---: | :---:
**Verbreitung** | Lokal, hängt sich an Wirtsprogramme | Werden selbst aktiv und sorgen für ihre Verteilung
**Verteilung** | Mit der Wirtsdatei (z.B. Datenträger; Benutzer verteilt Virus) | Benötigen keine Wirtsprogramme (führen sich im Zuge der Verteilung selbst aus)

> Kann man Viren und Würmer kombinieren?

- Kombination ist möglich, dann allerdings keine genau Spezifikation mehr als *Virus* oder *Wurm* möglich

> Wenn ja, wie sähe das Resultat aus? Wenn nein, warum nicht?

- Programm als Resultat, das sich an Wirtsdateien hängt oder sich selbstständig über Netze verbreitet

---

#### Übungsaufgabe 2.8
> Schätzen Sie anhand der in der vorherigen Folie genannten
  Werten die Ausbreitung von SQL-Slammer innerhalb der
  ersten Minute.
  Wie viele Instanzen von SQL-Slammer existieren
  schätzungsweise nach 60 Sekunden?
  
- 60s / 8,5s = 7,06 Mal
- 2^7,06 = 133 Würmer nach einer Minute

> Wie ist die maximal beobachtete Probing Rate (UDP-Pakete)
  von 26.000 Hz je Host begründbar?

Datenart | Größe in Bytes
:---: | :---:
UDP-Nutzdaten | 376
UDP-Header | 8
IP-Header | 20
Ethernet | 38
**Summe** | **442**

- 100 Mbit/s / (442 * 8 Bit) = 28280 / s (Theoretisches Maximum)

> Warum verlangsamt sich das Wachstum der
  Verbreitungsgeschwindigkeit nach ca. 60 Sekunden?

- Viele Hosts versuchen Pakete zu senden, Netz beginnt Bottleneck zu werden.

> Wie viele Infektionsversuche pro Sekunde werden nach
  60 Sekunden von allen infizierten Systemen in Summe
  durchgeführt?

- 133 Systeme, maximale Probing-Rate
- 133 * 26000 Versuche / Sekunde = 3458000 Versuche / Sekunde
- 133 * 100 Mbit/s = 13,3 Gbit/s

> Wie lange dauert es, bis 75.000 verwundbaren Systeme
  infiziert sind? Gehen Sie davon aus, dass sich die Population
  der infizierten Systeme im Schnitt alle 37 Sekunden
  verdoppelt.
  
- log(75000) = 16,2 Verdopplungen
- 16,2 * 37s ≃ 600s = 10 Minuten

---

#### Übungsaufgabe 2.9
Datentyp | Beschreibung | Ausführbar
:---: | :---: | :---:
`.scr` | Screensaver | O
`.rtf` | Keine Makro-Unterstützung | X
`.hta` | HTML-Applikation | O
`.bmp` | Bitmap | X
`.exr` | Bildformat | X
`.wav` | Audioformat | X
`.pdf` | Dokumentenformat | O
`.xlsx` | Excel mit Makro-Unterstützung | O

---

#### Übungsaufgabe 2.10
> An welcher Stelle des Programms kann Überlauf auftreten?

- `givenHash` wird berechnet (OK)
- `userHash` wird aus Datenbank geholt (OK)
- `pw` -> Benutzereingabe ohne Längenbeschränkung

> Korrigieren Sie das Programm so, dass kein Überlauf mehr auftreten
  kann.

```C
/* Read pw from standard input;
Maximum Length 63 character (+ null) */

fgets(pw, 64, stdin);
```

> Was ist durch einen Überlauf alles möglich und welche Schutzziele werden dadurch angegriffen?

1. Eigenen Hash zum Vergleich in den Speicher schreiben
  - Ziel: Ohne Kenntnis eines gültigen Passworts ist die PW-Abfrage immer positiv
    - Angreifer loggt sich ein
    
2. Schadcode einfügen (durch Überschreiben des Stacks) und ausführen
  - Code Execution
    - Keine Vertraulichkeit mehr
    - Keine Integrität
    - Keine Verfügbarkeit
    
---

#### Übungsaufgabe 2.11
> Skizzieren Sie einen persistenten XSS-Angriff, bei dem ein
  Angreifer seine Opfer über eine vertrauenswürdige Seite
  auf eine schädliche umleitet. Welche Nachrichten sind
  notwendig?
  
Angreifer |  | Legitimer Server |  | Schädlicher Server |  | Opfer
:---: | :---: | :---: | :---: | :---: | :---: | :---:
Eingabeseite anfordern | **>** | **O** |  |  |  | 
**O** | **<**| Eingabeseite liefern |  |  |  | 
Skript injizieren | **>** | **O** |  |  |  | 
|  |  | **O** | **<**| **<** | **<**| Modifizierte Seite abrufen
|  |  | Modifizierte Seite abliefern | **>** | **>** | **>** | **O**
|  |  |  |  |  |  | Skript wird ausgeführt
|  |  |  |  | **O** | **<** | Umleitung zu schädlichem Server

---

#### Übungsaufgabe 2.12
> Welche Werte werden in einem SYN Cookie gespeichert?

- TCP-Handshake -> Sequenznummern müssen synchronisiert werden, IP, Port, Maximum Segment Size

Wert | Beschreibung
:---: | :---:
`t` | Sehr langsam sich ändernder Zeitstempel
`m` | MSS-Parameter
`s` | Hash-Wert von IP, Port und `t`

> In welcher Nachricht und welchem Wert wird das SYNCookie kodiert zum Client übertragen?

- Werte (`m` und `s`) werden in der Sequenznummer zum Client codiert (in SYN-ACK-Nachricht).

> Warum überträgt Server SYN-Cookies?

- SYN-Cookie kann aus ACK des Clients dekodiert werden. Bis ACK kommt, müssen keine Daten auf Server-Seite gespeichert
werden.

> Wie erhält der Sender das Cookie zurück?

- Durch den ACK-Client-Wert - 1

---

#### Übungsaufgabe 2.13
> An welchen Port des Hubs muss er seinen Rechner
  anschließen?

- Keine Auswahl eines Ports bei einem Hub nötig

> In welchem Modus betreibt er seine Netzwerk-Karte?

- Promiscuous -> Nur dann erhält man alle Daten.

> Der Angreifer benutzt die Software Wireshark um den Netzverkehr aufzuzeichnen.
> Welche IP-Adresse hat der Client, welche der Server?

System | IP-Adresse
:---: | :---:
**Client** | 192.168.0.2
**Server** | 192.168.0.1

> Filtern Sie nun auf „telnet“. Wie ist der Benutzername und
  wie das Passwort?

- Username: fake
- Password: user

---

#### Übungsaufgabe 2.14
> Wie sieht Alices ARP-Tabelleneintrag für Bob vor dem Angriff
  aus? Wie Bobs Eintrag für Alice?

ARP-Tabelle | IP-Adresse | MAC-Adresse
:---: | :---: | :---:
Alice | 137.196.7.14 | **58-23-D7-FA-20-B0**
Bob | 137.196.7.23 | **71-65-F7-2B-08-53**

> Welche ARP-Nachrichten muss der Angreifer verschicken?

ARP-Nachricht | IP-Adresse | MAC-Adresse
:---: | :---: | :---:
ARP Reply | 137.196.7.14 | 0C-C4-11-6F-E3-98
ARP Reply | 137.196.7.23 | 0C-C4-11-6F-E3-98

> Was bewirken diese Nachrichten?

- Alice und Bob machen ein Update der ARP-Tabelle. Nachrichten von Alice an Bob gehen an den Angreifer, während Nachrichten
von Bob an Alice ebenfalls an den Angreifer gehen.

> Was muss der Angreifer beachten, damit weder Alice noch Bob
  Verdacht schöpfen?

- Angreifer muss empfangene Nachrichten (nach potentieller Veränderung) an beabsichtigten Empfänger weiterleiten.

---

#### Übungsaufgabe 2.15
> Auf welche Arten werden
  DNS-Einträge manipuliert?
  
- Modifikation der DNS-Konfiguration auf lokalem PC
- Modifikation der DNS-Einträge anderer PCs über falschen DHCP-Server
  - Muss DHCP-Antworten schneller senden als legitimer DHCP-Server

> Was erreicht man durch
  die Manipulation des
  DNS-Eintrags?
  
- Falsche Abbildungen von Hostnamen zu IP-Adressen
  - Umleitung auf falsche Webseiten oder Mail-Server

> Was kann der Angreifer dann beispielsweise tun?

- Vertrauliche Informationen abfragen
  - Username und Passwort

> Wie kann man einen manipulierten DNS-Eintrag als Benutzer erkennen?

- Bei HTTPS hat Server kein passendes Zertifikat
- Ggf. nicht komplette Seite repliziert
- IP-Adresse ist falsch

---

#### Übungsaufgabe 2.16
##### User-Mode Rootkit
- Schadsoftware greift in Kommunikation ein

##### Wireshark
- Wireshark kopiert Daten von Netzwerkschnittstelle
- Keine Manipulation möglich

##### Chefsekretär/-in
- Man-in-the-Middle, da Kommunikation immer über Schreibtisch geht

##### Router
- Kann Man-in-the-Middle sein, Datenverkehr muss aber unverschlüsselt sein

##### Funksender
- Nur Empfänger, und dann nur lesend

---

#### Übungsaufgabe 2.17
>  Zeigen Sie an einem einfachen Beispiel, warum zwei Hash-Ketten bei nur einer Reduktionsfunktion überlappen
  (kollidieren) können. Warum ist dies ein Problem?

- Kette 1: `A` -H> `H(A)` -R> `B` -H> **`H(B)`** -R> `C` -H> **`H(C)`** -R> `D`
- Kette 2: `B` -H> **`H(B)`** -R> `C` -H> **`H(C)`** -R> `D` -H> `H(D)` -R> `E`

- Überlappung verschwendet Speicherplatz für Hash-Werte und deren Passwörter

> Welches Passwort liefert die Hashwerte 1tik0 bzw. ui32u?

- Zu `1tik0` gehört das Passwort `crypto`
- `ui32u` ist nicht in der Rainbow-Table gespeichert

> Die Anwendung der Hash- bzw. Reduktionsfunktion ergibt an einer
  Stelle wikipedia. Können Sie das Passwort finden? Warum? Warum
  wird wikipedia überhaupt gespeichert?

- `Hashwert1` -R> `PW` -H> `Hashwert2` -> `Wikipedia`

- Kann nicht gefunden werden, da Endwert der Kette nicht erreicht wurde.
- Wikipedia hat keine Vorgänger in der Rainbow Table

> Sie erhalten den Hash 1vn6s. Wie erfolgt die Suche nach dem
Passwort?

- Suche nach Passwort zu Hash `1vn6s`.
  - Anwendung von `R3` führt zu keinem Erfolg (-> kein Endpasswort)
  - Anwendung von `R2` -H> `R3` ebenfalls erfolglos
  - Anwendung von `R1` -H> `R2` -H> `R3` erfolgreich (-> `myname` als Endpasswort)
- An Anfang der Kette gehen und H auf Passwort anwenden
  - Ergibt `1vn6s`, d.h. `abcdefgh` ist gesuchtes Passwort

---

#### Übungsaufgabe 2.18
> Wie viele potentielle Passwörter kann man aus 14 ASCII-Zeichen bilden (Angabe der Potenz reicht)?

- 95^14 mögliche Passwörter der Länge 14

> Wie viele potentielle Passwörter gibt es bei 7 ASCII-Zeichen?

- 95^7

> Wie viele potentielle Passwörter gibt es bei 7 ASCII-Zeichen, welches keine Kleinbuchstaben einsetzt?
Berechnen Sie diesen Wert.

- 26 Zeichen fallen weg -> 69^7
- Entspricht 7.446.353.252.589 Passwörtern

> Gegeben sei ein Rechner, der 10^9 Passwörter/s prüfen kann. Wie lange bräuchte ein solcher Rechner im Durchschnitt, um
  ein mit LM Hash geschütztes Passwort der Länge 14 zu knacken?
  
- Pro Gruppe einen halben Passwort-Raum durchsuchen
- Für 7-stellige Passwörter: (7,45 Bio / 2) Passwörter / 10^9 Passwörter / s) = 3723 s ≃ 62 Minuten
