# Regenbogen

**Warum er bei 42 Grad steht.** Ein Regenbogen ist kein Ding am Himmel, sondern ein Winkel. Dieses
Blatt spurt die Strahlen einzeln durch den Wassertropfen, findet den Winkel, ohne ihn zu kennen, und
baut daraus einen Himmel — nicht gemalt, sondern aus 256 000 gespurten Strahlen gerechnet.

→ **[Blatt öffnen](https://ssims437.github.io/regenbogen/)**

- **Der Tropfen** — Brechung, innere Spiegelung und Austritt mit Vektoren gespurt, jeder Strahl
  einzeln, mit dem Lichtanteil, der übrig bleibt
- **Die Kurve** — Ausfallswinkel über dem Auftreffpunkt, mit dem Umkehrpunkt, an dem sich das Licht
  staut. Genau dort ist der Bogen
- **Der Himmel** — jedes Pixel bekommt seine Farbe aus einsortierten Strahlen, 32 Wellenlängen,
  umgerechnet über die CIE-Normspektralwerte und verschmiert mit der Sonnenscheibe
- **Alexanders dunkles Band** — nicht dunkler gemalt, sondern messbar leer
- **Prüflauf** — sieben Zeilen, darunter der Vergleich der Vektorspur gegen die geschlossene Formel

## Nirgends steht die Zahl 42

Das ist der Punkt des Blatts. Der Winkel wird **gesucht**, nicht gesetzt: Für jede Wellenlänge wird
die Umkehrstelle der Ablenkkurve numerisch eingegrenzt. Was herauskommt:

| | rot (700 nm) | violett (400 nm) | in den Büchern |
|---|---|---|---|
| **Hauptbogen** | 42,35° | 40,57° | 42,4 / 40,6 |
| **Nebenbogen** | 50,39° | 53,61° | 50,3 / 53,5 |

Die Farbfolge kippt zwischen den Bögen — beim Hauptbogen steigt der Winkel mit der Wellenlänge
(Rot außen), beim Nebenbogen fällt er (Rot innen). Der Prüflauf misst das über 31 Wellenlängen und
findet **keine einzige Ausnahme in beide Richtungen**.

## Was der Prüflauf zeigt

| Behauptung | Ergebnis |
|---|---|
| Snellius hält an jeder Grenzfläche | **5985 Grenzflächen** · größter Rest 4,6·10⁻¹² |
| **Vektorspur und Winkelformel sagen dasselbe** | 7485 Strahlen, drei Ordnungen · Abstand **7,9·10⁻¹¹ Grad** |
| der Bogen sitzt genau am Umkehrpunkt | 20 Fälle · numerische Suche gegen `cos θᵢ = √((n²−1)/(k²+2k))` · **7,7·10⁻⁸** |
| **die berühmten Winkel kommen von selbst heraus** | 42,35° / 50,39° — aus der Kurve gesucht, nicht eingetragen |
| **zwischen den Bögen kommt nichts heraus** | **256 000 Strahlen** · **0** landen zwischen 42,5° und 50,2° |
| jede Spiegelung kostet Licht | Hauptbogen 5,1 % · Nebenbogen 1,8 % · dritter Bogen 0,91 % des einfallenden Lichts |
| beim Nebenbogen steht die Farbfolge verkehrt | 31 Wellenlängen · 30 von 30 Schritten in **beide** Richtungen ausnahmslos |

## Was mich das gekostet hat

**Der Nebenbogen stand bei 179,9°.** Der Ausfallswinkel wurde aus dem Skalarprodukt zwischen
austretender und einfallender Richtung gewonnen — und der Arkuskosinus liefert nur 0…180°. Für den
Hauptbogen geht das gut, weil er dort tatsächlich liegt. Der Nebenbogen wird aber um **231°**
gedreht, und gefaltet sieht das aus wie 129°. Für einen einzelnen Strahl stimmt das Ergebnis sogar
noch — aber die Suche nach dem Bogen sucht ein **Extremum**, und im gefalteten Bild liegt das
Maximum bei `b → 0`, also bei einem Strahl, der geradewegs zurückkommt. Heraus kam 179,93° statt
50,4°: eine Zahl, die so falsch ist, dass sie nicht wie ein Rundungsfehler aussieht, sondern wie
ein anderes Blatt.

Die Lösung war nicht, die Formel einzusetzen — die soll ja geprüft werden —, sondern die
**Gesamtdrehung entlang des Weges mitzuzählen**: an jeder Grenzfläche die vorzeichenbehaftete
Richtungsänderung aufaddieren. Damit gibt es eine Ablenkung von 231°, die keine 129° ist, und der
Bogen ist ihr **Minimum** — bei jeder Ordnung.

**Der gerechnete Himmel war zuerst ein weißer Strich.** In der geometrischen Optik ist die
Umkehrstelle eine echte Singularität: unendlich viele Strahlen auf denselben Winkel. Was da fehlte,
ist nichts Rechnerisches, sondern die **Sonne**: Sie steht unter rund 0,53° am Himmel, also ist
jeder Bogen mit ihrer Scheibe verschmiert. Erst mit dieser Faltung — und einer Tonwertkurve, die
nur auf die Helligkeit wirkt und nicht auf die Farbe, sonst wird ausgerechnet die Umkehrstelle weiß
— sieht es aus wie ein Regenbogen, weil es aus demselben Grund so aussieht.

**Ein Restfehler, der keiner ist.** Die Prüfung „Snellius hält überall" scheiterte zunächst an einer
Schranke von 10⁻¹², obwohl gemessen 4,6·10⁻¹² herauskam. Das ist nicht der Fehler der Brechung,
sondern der des **Zurückrechnens**: Nahe am streifenden Einfall ist der Kosinus flach, und der
Arkuskosinus verliert dort rund die Hälfte seiner Stellen. Die Schranke steht jetzt bei 10⁻⁹ — mit
der Begründung direkt in der Prüfzeile, damit sie nicht später wie eine Bequemlichkeit aussieht.

**Was das Blatt nicht kann:** keine Airy-Theorie und damit **keine Interferenzbögen** — die blassen
Zusatzstreifen innen am Hauptbogen entstehen durch Wellenüberlagerung und sind mit reiner
Strahlenoptik grundsätzlich nicht zu haben. Keine Tropfenverformung (große Tropfen sind abgeplattet,
was den Bogen an den Seiten verändert), keine Mehrfachstreuung zwischen Tropfen, keine Polarisation
(die Fresnel-Anteile werden gemittelt, obwohl Regenbogenlicht stark polarisiert ist), keine
Rayleigh-Streuung der Luft dazwischen.

## Technik

Eine einzelne HTML-Datei. Kein Build, keine Bibliothek, nichts verlässt den Browser.
Vektorielle Strahlverfolgung, Fresnel-Formeln, CIE-Normspektralwerte, Canvas 2D, hell und dunkel.

## Die ganze Sammlung

Alle Blätter nach Feld geordnet, jedes mit eigenem Repo:
**[ssims437.github.io](https://ssims437.github.io/)**

## Lizenz

MIT
