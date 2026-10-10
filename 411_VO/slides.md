
# Digitale Tragwerksplanung

## Informationen werden Realität

---

<img
  src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Skizze.png"
  alt="Skizze Informationsfluss Planung und Fertigung"
  style="max-width:40%;height:auto;">

---

## Inhalt

<div class="two-col">
<div class="card">

### Informationsfluss verstehen

- Planung → Fertigung → Bauwerk
- menschenlesbar vs. maschinenlesbar
- Schnittstellen als Fehlerquelle **und** Fehlerkorrektur

</div>
<div class="card">

### Prozesse robust gestalten

- CAD · CAE · CAM unterscheiden
- DFM und Poka Yoke anwenden
- Versionierung als Teil der Qualitätssicherung verstehen
- Modellkomplexität bewusst wählen

</div>
</div>

---

# Vom digitalen Modell zum realen Bauwerk

--

## Status quo: digitale Inseln

<div class="flow-row">
  <div class="flow-box">Objekt- / Fachplanung<br><span>CAD · CAE · BIM</span></div>
  <div class="arrow">→</div>
  <div class="flow-box">Prüfung<br><span>Pläne · Berichte</span></div>
  <div class="arrow">→</div>
  <div class="flow-box">Auftragnehmer<br><span>eigene CAD · CAE · CAM</span></div>
  <div class="arrow">→</div>
  <div class="flow-box">Werk / Subunternehmer<br><span>Werkstattplanung</span></div>
</div>

<div class="callout">
Information wird mehrfach <strong>übersetzt, neu erfasst, geprüft und weitergegeben</strong>.
</div>

<div class="fragment">

**Jede Schnittstelle kann gleichzeitig Fehlerquelle und Fehlerkorrektur sein.**

</div>

---

## Der Informationsfluss als Leitmotiv

<div class="pipeline">
  <div>Anforderung</div><span>→</span>
  <div>Tragwerksplanung</div><span>→</span>
  <div>CAD / BIM / CAE</div><span>→</span>
  <div>Fertigungsinformation</div><span>→</span>
  <div>CAM / Postprocessor</div><span>→</span>
  <div>Maschine / Mensch</div><span>→</span>
  <div>Bauwerk</div>
</div>

<div class="pipeline feedback">
  <div>Prüfung</div><span>←</span>
  <div>Messung</div><span>←</span>
  <div>Rückmeldung</div><span>←</span>
  <div>Abweichung</div>
</div>

### Ziel

> Die digitale Kette nicht nur **automatisieren**, sondern **robust gestalten**.

---

## Menschenlesbar ≠ maschinenlesbar

<div class="two-col">
<div class="card accent-blue">

### Für Menschen

- Plan / PDF
- Bericht
- Modell im Viewer
- Montageanweisung
- Skizze / Markierung

**Stärke:** Interpretation, Kontext, Plausibilitätsprüfung

</div>
<div class="card accent-orange">

### Für Maschinen

- IFC
- BVBS / ABS
- NC-DSTV
- G-Code
- Robotersprache (ROS, KRL, RAPID...)

**Stärke:** eindeutige, strukturierte, wiederholbare Verarbeitung

</div>
</div>

<div class="callout">Digital ist nicht automatisch maschinenlesbar. Ein PDF ist digital – aber primär dokumentorientiert.</div>

---

# Bauen ist Fertigung

--

## Einzelfertigung – mit vielen Wiederholungen

Bauwerke sind meist **Unikate**.

Aber sie bestehen aus:

<div class="flow-row compact">
  <div class="flow-box">Bauwerk</div><div class="arrow">→</div>
  <div class="flow-box">Bauteile</div><div class="arrow">→</div>
  <div class="flow-box">Bauelemente</div><div class="arrow">→</div>
  <div class="flow-box">Einzelprodukte</div>
</div>

<div class="fragment">

Dort entstehen Möglichkeiten für:

**Standardisierung · Parametrisierung · Automatisierung · Vorfertigung**

</div>

--

## Fertigungsverfahren nach DIN 8580

<div class="six-grid">
  <div class="card"><strong>1 · Urformen</strong><br>Betonieren, Gießen, 3D-Druck</div>
  <div class="card"><strong>2 · Umformen</strong><br>Biegen, Walzen, Ziehen</div>
  <div class="card"><strong>3 · Trennen</strong><br>Schneiden, Bohren, Fräsen</div>
  <div class="card"><strong>4 · Fügen</strong><br>Schweißen, Schrauben, Kleben</div>
  <div class="card"><strong>5 · Beschichten</strong><br>Korrosionsschutz, Hydrophobierung</div>
  <div class="card"><strong>6 · Stoffeigenschaften ändern</strong><br>z. B. Wärmebehandlung</div>
</div>

--

## Warum muss die Planung Fertigung kennen?

<div class="three-col">
<div class="card">
<h3>Ausführbarkeit</h3>
<p>Ist das geplante Detail realistisch herstell- und montierbar?</p>
</div>
<div class="card">
<h3>Datenqualität</h3>
<p>Welche Information muss in welcher Form beim Werk / auf der Baustelle ankommen?</p>
</div>
<div class="card">
<h3>Automatisierung</h3>
<p>Nur geeignete, strukturierte Information kann zuverlässig weiterverarbeitet werden.</p>
</div>
</div>

<div class="quote">Planung endet nicht am Plan. Sie definiert Voraussetzungen für reale Herstellungsprozesse.</div>

---

# CAD · CAE · CAM

- CAD - Computer-Aided Design
- CAE - Computer-Aided Engineering
- CAM - Computer-Aided Manufacturing

--

## CAD · CAE · CAM

<div class="three-col">
<div class="card accent-blue">
<h4>CAD</h4>
<p class="big">Was soll entstehen?</p>
<p>Geometrie · Modell · Zeichnung · Detail</p>
</div>
<div class="card accent-green">
<h4>CAE</h4>
<p class="big">Wie verhält es sich?</p>
<p>Analyse · Simulation · Bemessung · Optimierung</p>
</div>
<div class="card accent-orange">
<h4>CAM</h4>
<p class="big">Wie wird es hergestellt?</p>
<p>Werkzeugwege · Zuschnitt · Biegen · Maschinenbefehle</p>
</div>
</div>

--

## CAD · Computer-Aided Design

<div class="two-col">
<div>

**Typische Aufgaben**

- 2D-Zeichnungen
- 3D-Planung
- konstruktive Details
- technische Dokumentation
- parametrische Geometrie

</div>
<div class="card">

### Bauwerksplanung

Rhino / AutoCAD / Revit / Tekla / Allplan …

</div>
</div>

--

## CAE · Computer-Aided Engineering

<div class="two-row">
<div class="card">

### Tragwerksplanung

- Schnittgrößen
- Verformungen
- Spannungen
- Stabilität & Dynamik
- Bemessung

</div>
<div>

### Wichtig

Ein CAE-Modell ist eine **Abstraktion der Realität**.

Mehr Freiheitsgrade und Parameter bedeuten nicht automatisch eine bessere Prognose.

</div>
</div>

--

## CAM · Computer-Aided Manufacturing

<div class="two-col">
<div>

CAM überführt Planungsinformation in eine **fertigungsbezogene Beschreibung**:

- Werkzeugbahnen
- Maschinenachsen
- Bearbeitungsreihenfolge
- Prozessparameter

</div>
<div class="card accent-orange">

### Beispiele Bauwesen

- CNC-Bewehrungsbiegung
- Stahlprofilbearbeitung
- Laserschneiden
- 3D-Betondruck
- robotische Fertigung

</div>
</div>

---

## Vom Modell zur Maschine

<div class="pipeline big-pipeline">
  <div>CAD / BIM</div><span>↔</span>
  <div>CAE</div><span>↔</span>
  <div>CAM</div><span>→</span>
  <div>NC / CNC / Roboter</div>
</div>

--

# Maschinen bekommen Anweisungen

--

## Vom Lochband zur digitalen Schnittstelle

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/411_VO_Lochband.png" alt="Lochband">
<div class="source">Bildquelle: gcodetutor</div>
</div>
<div>

Frühe numerische Steuerungen nutzten physische Datenträger.

<div class="timeline-mini">
  <span>Lochkarte / Lochband</span> → <span>NC</span> → <span>CNC</span> → <span>vernetzte Fertigung</span>
</div>


--

## NC-Fräsen: der Schritt zur numerischen Steuerung

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/411_VO_NC_machine.png" alt="Frühe NC Fräsmaschine">
<div class="source">Bildquelle: make magazine</div>
</div>
<div>

### 1950er Jahre

Numerisch gesteuerte Werkzeugmaschinen zeigen früh:

> Geometrie kann in **formalisierten Bewegungsanweisungen** beschrieben werden.

</div>
</div>

---

## Maschinen-Sprachen im Bauwesen

<table class="compact-table">
<thead><tr><th>Anwendung</th><th>Information</th><th>Beispiel</th></tr></thead>
<tbody>
<tr><td>CNC / 3D-Druck</td><td>Bewegungen + Prozessparameter</td><td><strong>G-Code</strong></td></tr>
<tr><td>Bewehrung</td><td>Stabdurchmesser + Biegeform + Längen</td><td><strong>BVBS / ABS</strong></td></tr>
<tr><td>Stahlbau</td><td>Profil + Bohrungen + Schnitte</td><td><strong>NC-DSTV</strong></td></tr>
<tr><td>Roboter</td><td>Trajektorie + Aktionen + Logik</td><td><strong>ROS / KRL (Kuka) / RAPID (ABB) / …</strong></td></tr>
</tbody>
</table>

<div class="callout">Der Plan ist für Menschen. Das Maschinenformat ist für die Fertigung.</div>

--


## G-Code

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/423_3D-Druck_slicer.gif" alt="3DDruck">
</div>
<div>

G-Code findet in vielen Bereichen der modernen Fertigung und Produktion Anwendung


--

## Bewehrung: von der Biegeliste zur CNC-Maschine

<div class="pipeline big-pipeline">
  <div>Bewehrungsmodell</div><span>→</span>
  <div>Biegeinformation</div><span>→</span>
  <div>BVBS</div><span>→</span>
  <div>Biegemaschine</div><span>→</span>
  <div>Stab</div>
</div>

### Potenzial

- weniger manuelle Dateneingabe
- reproduzierbare Biegeformen
- direkter Datenfluss aus der Planung

### Risiko

**Fehler werden ebenso effizient automatisiert.**

--

<img src="https://aiztok.github.io/DiTWP/Bilder/424_BVBS_gif.gif" alt="BVBS_Viewer">

--

<iframe width="560" height="315" src="https://www.youtube.com/embed/llc576PmdUg?si=_VxAcB63eNycvJYy" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

--

## Stahlbau: NC-DSTV als Fertigungsinformation

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/425_dstv-nc_Bild_1.png" alt="NC-DSTV Bild">
<div class="source">Bildquelle: Klietsch</div>
</div>
<div>


NC-DSTV beschreibt Bearbeitungen an Stahlprofilen, z. B.:

- Konturen
- Bohrungen
- Schnitte
- Markierungen

</div>
</div>

---

## Robotik: Geometrie allein reicht nicht

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/426_Roboter_Roksi.gif" alt="Robotersimulation">
<div class="source">Animation: DiTWP</div>
</div>
<div>

Robotische Prozesse benötigen zusätzlich:

- Bewegungsplanung
- Kollisionserkennung
- Werkzeugorientierung
- Sensorik
- Prozesslogik
- Simulation

<div class="callout">Je autonomer der Prozess, desto wichtiger werden robuste digitale Schnittstellen.</div>

</div>
</div>

---

# Design for Manufacturing

--

## DFM: Fertigung bereits im Entwurf mitdenken

<div class="quote">Nicht erst fragen: „Kann man das herstellen?“<br>Sondern: „Wie gestalten wir es so, dass es zuverlässig hergestellt werden kann?“</div>

<div class="four-grid">
<div class="card">Vereinfachen</div>
<div class="card">Standardisieren</div>
<div class="card">Montage mitdenken</div>
<div class="card">Prüfung ermöglichen</div>
</div>

---

## DFM · Vereinfachen und standardisieren

<div class="two-col">
<div class="card">

### Vereinfachen

> Was es nicht gibt, kann nicht versagen.

- unnötige Teile vermeiden
- Varianten reduzieren
- gleiche Details wiederverwenden

</div>
<div class="card">

### Standardisieren

- wiederverwendbare Berechnungsmodule
- parametrisierte Details
- standardisierte Materialien / Profile
- wiederkehrende Fertigungslogik

</div>
</div>

---

## DFM · Montage und Wartung mitdenken

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_DFM_Ankerschienen_Presse.png" alt="Ankerschienen für Spannpresse">
<div class="source">Bild: DiTWP</div>
</div>
<div>

### Beispiel Vorspannung

Kleine planerische Maßnahmen können die spätere Ausführung massiv vereinfachen.

- Wie wird ein 200+ kg Spannpresse positioniert?
- Wo kann angeschlagen werden?
- Welche Zugänglichkeit bleibt erhalten?
- Wie erfolgt spätere Inspektion / Austausch?

</div>
</div>

---

## DFM · Toleranzen fertigungsgerecht festlegen

<div class="two-col">
<div>

### Nicht:

**„Toleranzen minimieren“**

</div>
<div>

### Sondern:

**unnötig enge Toleranzen vermeiden**

</div>
</div>

<div class="callout">
Toleranzen müssen Funktion, Montage, Fertigung und Kosten gemeinsam berücksichtigen.
</div>

Beispiele:

- Lichtmaße + Langzeitverformung
- Spundwandtoleranzen
- Bodenanker
- Lager / Fugen / Einbauteile

---

# Fehler vermeiden: Poka Yoke

--

## Poka Yoke

> Prozesse, Produkte und Schnittstellen so gestalten, dass Fehler **vermieden** oder **sofort erkannt** werden.

<div class="three-col">
<div class="card"><strong>Fehler unmöglich machen</strong><br>Geometrische Codierung</div>
<div class="card"><strong>Fehler sichtbar machen</strong><br>Farben, Warnungen, Plausibilitätschecks</div>
<div class="card"><strong>Fehler früh stoppen</strong><br>Validierung vor Export / Fertigung</div>
</div>

--

## Poka Yoke · physische Beispiele

<div class="two-col images-equal">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Schraubverbindung_Bild.png" alt="Farbkodierte Schraubverbindungen">
<p><strong>Farbcodierung:</strong> schnell erkennbar</p>
</div>
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Schrauben_Bild.png" alt="Schrauben mit Größenabständen">
<p><strong>Größenabstand:</strong> Verwechslung erschweren</p>
</div>
</div>

<div class="source">Bilder: DiTWP / Quellen siehe 411_VO</div>

---

## Poka Yoke · digital

<div class="two-col">
<div class="card bad">

### Fehleranfällig

- Material als Freitext
- beliebige Zahleneingabe
- Export überschreibt Datei
- IFC-Klasse frei tippen
- kein Versionsstand sichtbar

</div>
<div class="card good">

### Robuster

- Dropdown mit gültigen Werten
- Wertebereich / Plausibilitätscheck
- Export + Status + Pfad
- Auswahl gültiger IFC-Klassen
- Versionskontrolle / Commit

</div>
</div>

---

# Kompliziert ≠ komplex

---

## Kompliziert

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Uhrwerk_Bild.png" alt="Uhrwerk">
<div class="source">Bildquelle:  fotocommunity.de</div>
</div>
<div>

Viele Teile und Beziehungen – aber grundsätzlich:

- zerlegbar
- beschreibbar
- regelbasiert
- reproduzierbar

<div class="quote">Schwer zu verstehen – aber bei ausreichendem Wissen gut beherrschbar.</div>

</div>
</div>

---

## Komplex

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Mayo_Bild.png" alt="Mayonnaise">
<div class="source">Bildquelle: images.vrt.be</div>
</div>
<div>

Das Verhalten entsteht aus Wechselwirkungen.

- Rückkopplungen
- Abhängigkeiten
- Unsicherheiten
- nichtlineares Verhalten
- schwer vollständig vorhersehbar

<div class="quote">Einzelteile können einfach sein – ihr Zusammenspiel nicht.</div>

</div>
</div>

---

## Tragwerksplanung: kompliziertes Modell ≠ bessere Prognose

<div class="two-col">
<div class="card">

### Modell A

Balkenmodell

- E, A, I
- klare Lagerung
- wenige Parameter
- gut prüfbar

</div>
<div class="card">

### Modell B

3D-Schalen- / Volumenmodell

- Kontakt
- Lagersteifigkeiten
- Rissmodell
- Bodenfedern
- Bauzustände

</div>
</div>

<div class="callout">Modell B ist nur dann „besser“, wenn die zusätzlichen Annahmen und Parameter ausreichend belastbar sind.</div>

---

## Ockhams Rasiermesser

<div class="two-col image-text">
<div>
<img src="https://aiztok.github.io/DiTWP/Bilder/421_VO_Ockham.png" alt="Ockhams Rasiermesser Cartoon">
</div>
<div>

Wenn mehrere Modelle die Beobachtung ausreichend erklären:

> Bevorzuge nicht unnötig zusätzliche Annahmen.

### Für Ingenieurmodelle

**So einfach wie möglich – aber so detailliert wie erforderlich.**

</div>
</div>

---

## Underfitting ↔ Overfitting

<div class="model-scale">
  <div class="zone under"><strong>zu einfach</strong><br>relevante Effekte fehlen</div>
  <div class="zone goodzone"><strong>angemessen</strong><br>relevante Physik + belastbare Parameter</div>
  <div class="zone over"><strong>zu kompliziert</strong><br>viele unsichere Parameter / Scheingenauigkeit</div>
</div>

### Die zentrale Frage

Nicht: **„Wie detailliert kann ich modellieren?“**

Sondern: **„Welche Modellkomplexität ist für meine Fragestellung gerechtfertigt?“**

---

# Kernaussagen

<div class="four-grid takeaway-grid">
<div class="card">Information wird erst wertvoll, wenn sie korrekt weiterverarbeitet werden kann.</div>
<div class="card"><DFM und Poka Yoke beginnen bereits in der Planung.</div>
<div class="card"><Mehr (Modell)komplexität ist nicht automatisch mehr Genauigkeit.</div>
<div class="card">Automatisierung braucht robuste Schnittstellen, Einheiten, Semantik und Prüfungen.</div>
</div>

--

# Vom digitalen Modell zur Realität

<div class="pipeline big-pipeline final-flow">
  <div>Information</div><span>→</span>
  <div>Modell</div><span>→</span>
  <div>Schnittstelle</div><span>→</span>
  <div>Fertigung</div><span>→</span>
  <div>Bauwerk</div>
</div>

<div class="quote large-quote">Digitalisierung bedeutet nicht nur Daten erzeugen.<br><strong>Sie bedeutet Informationsflüsse bewusst gestalten.</strong></div>
