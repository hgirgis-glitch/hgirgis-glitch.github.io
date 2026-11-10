# Kredit Seite

Eine einzelne Seite: Restschuld, Rate, Zinsen bis zum Ende, Sondertilgungen, "Wann ist GO?" (Tagesgeld größer als Restschuld), Netto Vermögen, Kredit gegen Tagesgeld, Liste der Darlehen.

Alles läuft im Browser. Es gibt keinen Server, keine Anmeldung und keine externen Anfragen. Die Zahlen in `daten.js` sind erfunden (4 Beispiel Darlehen). Eigene Zahlen kommen nur in diese eine Datei.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | die Seite (Code und Design) |
| `daten.js` | die Daten, hier eigene Zahlen eintragen |

Öffnen: `index.html` im Browser. Beide Dateien müssen im selben Ordner liegen.

## Daten eintragen (für Claude oder von Hand)

`daten.js` enthält `krows`. Das ist ein Tabellenblatt als Liste von Zeilen, jede Zeile eine Liste von Texten, genau so wie Excel die Zellen anzeigt (z. B. `"  1.400,00 € "`, `"2,00%"`, `"Dez.-27"`). Spaltenbuchstaben wie in Excel, A ist Position 0.

**Kopfblock, Zeilen 2 bis 5 (ein Darlehen pro Zeile)**

| Spalte | Inhalt |
|---|---|
| C | ursprünglicher Betrag |
| J | Name mit Betrag, z. B. `Bank A 200.000 €` (die erste Zahl wird als Darlehensbetrag gelesen) |

**Zeile mit `KapESt`:** in Spalte A steht `KapESt`, in Spalte B der Steuersatz, z. B. `26,38%`.

**Tilgungsplan:** Die Kopfzeile ist die Zeile mit `Monat` in Spalte B. Direkt darüber stehen die Titel der Darlehen, z. B. `Tilgungsplan 2036` (die Jahreszahl wird als Laufzeitende angezeigt). Zwei Zeilen unter `Monat` stehen Zinssatz (z. B. `2,00%`) und Rate je Darlehen.

Je Monat eine Zeile ab der Zeile drei unter `Monat`:

| Spalte | Inhalt |
|---|---|
| B | Monat, Format `Apr.-26`, `Mai-26`, `Juni-26`, `März-27` (deutscher Kurzname, Minus, zweistelliges Jahr) |
| C, G, K, O | Restschuld des Darlehens 1 bis 4 nach der Zahlung |
| D, H, L, P | Zinsen des Monats für Darlehen 1 bis 4 |
| F, J, N, R | Sondertilgung des Monats für Darlehen 1 bis 4 |
| T | Summe Restschuld |
| U | Summe Zinsen |
| W | Summe Sondertilgung |
| Y | Tagesgeld Bestand |
| Z | versteuerter Zinsertrag des Monats |
| AA | Tagesgeld Zinssatz, z. B. `2,50%` |
| AB | Sondersparen oder Ablöse (monatliche Sparrate) |

Die Zeilen müssen lückenlos aufeinander folgen. Sobald die Summe Restschuld (T) wieder 0 ist, endet der Plan.

`vrows` (Vermögen) wird für diese Seite nicht gebraucht und kann so bleiben.

## Grenzen, die man kennen sollte

- Die Seite rechnet genau mit **4 Darlehen** (die vier Spaltenblöcke). Weniger geht (Blöcke leer lassen). Mehr als 4 braucht eine Änderung im Code.
- Die Spaltenpositionen sind fest. Die Excel Liste muss also dieselbe Struktur haben oder die Daten müssen vor dem Eintragen in diese Struktur gebracht werden.
- Der Begriff "GO" ist ein persönliches Konzept: der Monat, ab dem das Tagesgeld größer ist als die Restschuld. Wer das nicht braucht, lässt es in Ruhe oder lässt es von Claude entfernen.
- Die Daten werden beim Öffnen der Seite aus `daten.js` geladen. Der Browser merkt sich den letzten Stand zusätzlich im lokalen Speicher. Nach einer Änderung der Daten einmal hart neu laden (Strg+Shift+R).

## Fertiger Auftrag für Claude

Diesen Text zusammen mit `index.html`, `daten.js` und der eigenen Excel Liste an Claude geben:

> Ich habe eine fertige Kredit Seite (index.html plus daten.js). Bitte lies die README.md und befülle daten.js mit den Zahlen aus meiner angehängten Excel Liste im beschriebenen Format (krows). Ändere index.html nicht. Wenn meine Liste nicht zur Struktur passt (zum Beispiel mehr als 4 Darlehen oder andere Spalten), sag mir das zuerst und schlage vor, wie wir es lösen. Öffne danach die Seite und prüfe, dass Restschuld heute, Rate im Monat und die Darlehensliste zu meiner Excel Liste passen. Nenne mir Abweichungen offen.
