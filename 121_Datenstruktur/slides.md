## Digitale Tragwerksplanung
### Datenstrukturen

**Von einzelnen Werten zu strukturierten Bauwerksinformationen**

<small class="muted">121 · Vorlesung</small>

Note:
Ziel der Einheit ist nicht, alle Datenformate im Detail zu lernen. Entscheidend ist das Verständnis, warum dieselbe Information unterschiedlich strukturiert werden kann und warum Software ein gemeinsames Schema benötigt.

---

## Was ist eine Datenstruktur?

> Eine Datenstruktur legt fest, **wie Informationen organisiert, gespeichert und miteinander verknüpft werden**.

<div class="flow">
  <div class="box fragment">Wert</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Liste / Tabelle</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Hierarchie</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Objektmodell</div>
</div>

--

## Warum ist die Struktur wichtig?

- Computer sehen zunächst nur **Daten**. <!-- .element: class="fragment" -->
- Die Struktur liefert **Bedeutung und Beziehungen**. <!-- .element: class="fragment" -->
- Unterschiedliche Aufgaben benötigen unterschiedliche Strukturen. <!-- .element: class="fragment" -->
- Datenaustausch funktioniert nur, wenn Sender und Empfänger die Struktur verstehen. <!-- .element: class="fragment" -->

<div class="callout fragment">
<strong>Tragwerksplanung:</strong> Koordinaten, Querschnitte, Materialien, Bauteile, Lager, Lasten und Beziehungen müssen eindeutig zuordenbar sein.
</div>

--

## Heute betrachten wir

<div class="three-col">
  <div class="card fragment">
    <h4>Grundkonzept</h4>
    Klassen & Objekte
  </div>
  <div class="card fragment">
    <h4>Flache Daten</h4>
    CSV / XLSX
  </div>
  <div class="card fragment">
    <h4>Hierarchische Daten</h4>
    JSON
  </div>
  <div class="card fragment">
    <h4>Parametrische Daten</h4>
    Grasshopper Data Trees
  </div>
  <div class="card fragment">
    <h4>Objektmodell</h4>
    IFC
  </div>
  <div class="card fragment">
    <h4>Berechnungsmodell</h4>
    SAF / IFC Structural
  </div>
</div>

---

## Klassen & Objekte
### Warum das **C** in IFC wichtig ist

**Industry Foundation Classes**

- Klassen werden in objektorientierten Programmiersprachen verwendet. <!-- .element: class="fragment" -->
- Eine Klasse kann als **Bauplan für Objekte** verstanden werden. <!-- .element: class="fragment" -->
- Objekte besitzen definierte **Attribute** und können **Funktionen** besitzen. <!-- .element: class="fragment" -->

Note:
Der historische Name IFC verweist auf die objektorientierte Softwareentwicklung der 1990er Jahre. Das Beispiel bleibt bewusst einfach und soll nur das Prinzip vermitteln.

--

## Beispiel: Klasse `Wand`

```python [1|2-5|7-8]
class Wand:
    def __init__(self, name, material, width):
        self.name = name
        self.material = material
        self.width = width

    def info(self):
        return f"{self.name}: {self.material}, d = {self.width} m"
```

<div class="callout fragment">
Die Klasse definiert, <strong>welche Informationen</strong> ein Objekt vom Typ <code>Wand</code> besitzt.
</div>

--

## Aus der Klasse wird ein Objekt

```python
w1 = Wand("W001", "KLH", 0.20)

print(w1.name)
print(w1.material)
print(w1.width)
print(w1.info())
```

Ausgabe:

```text
W001
KLH
0.2
W001: KLH, d = 0.2 m
```

--

## Klasse ≠ Objekt

<div class="two-col">
  <div class="card">
    <h3>Klasse</h3>
    <p><strong>Definition / Bauplan</strong></p>
    <ul>
      <li>Welche Attribute?</li>
      <li>Welche Datentypen?</li>
      <li>Welche Funktionen?</li>
    </ul>
  </div>

  <div class="card fragment">
    <h3>Objekt</h3>
    <p><strong>Konkrete Instanz</strong></p>
    <ul>
      <li>Name = W001</li>
      <li>Material = KLH</li>
      <li>Dicke = 0.20 m</li>
    </ul>
  </div>
</div>

--

## Bezug zur BIM-Software

<div class="flow">
  <div class="box">Klasse<br><strong>Wand</strong></div>
  <div class="arrow">→</div>
  <div class="box fragment">Objekt<br><strong>W001</strong></div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Attribute<br><strong>Material, Dicke, ...</strong></div>
</div>

<br>

- BIM-Programme implementieren Klassen in ihrer Software. <!-- .element: class="fragment" -->
- IFC definiert standardisierte Klassen für den Datenaustausch. <!-- .element: class="fragment" -->

---

## Flache Datenstrukturen
### CSV und Tabellen

Eine Tabelle organisiert Daten in **Zeilen und Spalten**.

```text
X ; Y ; Z
0 ; 0 ; 0
0 ; 0 ; 3.15
6 ; 0 ; 3.15
```

--

## CSV

**CSV = Comma-Separated Values**

- reine Textdatei <!-- .element: class="fragment" -->
- einfache, tabellarische Struktur <!-- .element: class="fragment" -->
- Trennzeichen z. B. `,` oder `;` <!-- .element: class="fragment" -->
- sehr leicht von Programmen zu lesen <!-- .element: class="fragment" -->

<div class="callout fragment">
Gut geeignet, wenn jeder Datensatz dieselbe einfache Struktur besitzt.
</div>

--

## CSV: Beispiel Bauteile

```csv
Name;Typ;Material;Dicke
W001;Wall;Concrete;0.20
W002;Wall;Concrete;0.25
S001;Slab;Concrete;0.30
```

Was funktioniert gut?

- viele gleichartige Datensätze <!-- .element: class="fragment" -->
- Filtern und Sortieren <!-- .element: class="fragment" -->
- Import / Export <!-- .element: class="fragment" -->

--

## Wo wird eine Tabelle schwierig?

Wir wollen zusätzlich speichern:

- eine Wand besitzt mehrere Schichten <!-- .element: class="fragment" -->
- jede Schicht besitzt Material + Dicke <!-- .element: class="fragment" -->
- die Wand besitzt eine Position mit X/Y/Z <!-- .element: class="fragment" -->
- die Wand besitzt beliebig viele Eigenschaften <!-- .element: class="fragment" -->

<div class="callout fragment">
<strong>Problem:</strong> Verschachtelte Beziehungen passen nur umständlich in eine flache Tabelle.
</div>

--

## XLSX ist nicht gleich CSV

<table class="compact">
<thead>
<tr><th></th><th>CSV</th><th>XLSX</th></tr>
</thead>
<tbody>
<tr class="fragment"><td>Struktur</td><td>Text / Tabelle</td><td>Workbook mit Tabellenblättern</td></tr>
<tr class="fragment"><td>Formatierung</td><td>nein</td><td>ja</td></tr>
<tr class="fragment"><td>Formeln</td><td>nein</td><td>ja</td></tr>
<tr class="fragment"><td>Maschinenlesbarkeit</td><td>sehr einfach</td><td>komplexer</td></tr>
<tr class="fragment"><td>Praxis</td><td>Schnittstelle</td><td>Bearbeitung / Tabellenmodell</td></tr>
</tbody>
</table>

---

## Hierarchische Datenstrukturen
### JSON

**JSON = JavaScript Object Notation**

- textbasiert <!-- .element: class="fragment" -->
- menschenlesbar <!-- .element: class="fragment" -->
- maschinenlesbar <!-- .element: class="fragment" -->
- hierarchisch / verschachtelbar <!-- .element: class="fragment" -->

--

## Ein einfaches JSON-Objekt

```json
{
  "type": "Punkt",
  "globalId": "028c968f-687d-484e-9c0a-5048a923b8c4",
  "name": "Punkt 1",
  "description": "Startkoordinate",
  "x": 10.2,
  "y": 20.1,
  "z": 162.5
}
```

--

## Key – Value

```json
{
  "name": "Punkt 1",
  "x": 10.2
}
```

<div class="two-col">
  <div class="card fragment">
    <h4>Key</h4>
    <code>"name"</code><br>
    <code>"x"</code>
  </div>
  <div class="card fragment">
    <h4>Value</h4>
    <code>"Punkt 1"</code><br>
    <code>10.2</code>
  </div>
</div>

--

## JSON kann verschachtelt werden

```json [1-2|3-7|8-11]
{
  "name": "W001",
  "location": {
    "x": 10.0,
    "y": 20.0,
    "z": 0.0
  },
  "properties": {
    "loadBearing": true,
    "fireResistance": "REI120"
  }
}
```

--

## Dieselben Daten als Baum

<div class="tree">W001
├── name = "W001"
├── location
│   ├── x = 10.0
│   ├── y = 20.0
│   └── z = 0.0
└── properties
    ├── loadBearing = true
    └── fireResistance = "REI120"</div>

<div class="callout fragment">
Die Baumdarstellung macht die <strong>Hierarchie</strong> sichtbar.
</div>

--

## JSON: Arrays / Listen

```json
{
  "walls": [
    {"name": "W001", "width": 0.20},
    {"name": "W002", "width": 0.25},
    {"name": "W003", "width": 0.15}
  ]
}
```

<div class="callout fragment">
Ein JSON-Dokument kann Objekte, Listen und weitere verschachtelte Objekte kombinieren.
</div>

--

## Daten aus JSON lesen

```python [1|3-4|6-8]
import json

with open("model.json", "r", encoding="utf-8") as f:
    model = json.load(f)

first_wall = model["walls"][0]
print(first_wall["name"])
print(first_wall["width"])
```

<pre class="fragment"><code class="language-text">W001
0.2</code></pre>

--

## Verschachtelte Eigenschaft lesen

```python
wall = {
    "name": "W001",
    "properties": {
        "loadBearing": True,
        "fireResistance": "REI120"
    }
}

print(wall["properties"]["fireResistance"])
```

```text
REI120
```

--

## Datenstruktur allein reicht nicht
### Wir benötigen ein **Schema**

Zwei Dateien können syntaktisch gültiges JSON sein – aber völlig unterschiedlich aufgebaut.

<div class="two-col small">
  <div>
    <pre><code class="language-json">{
  "x": 10,
  "y": 20
}</code></pre>
  </div>
  <div>
    <pre><code class="language-json">{
  "coordinates": [10, 20]
}</code></pre>
  </div>
</div>

<div class="callout fragment">
Beides ist gültiges JSON. Aber welche Struktur erwartet die Software?
</div>

--

## JSON Schema

Ein Schema beschreibt Regeln für die Daten.

```json
{
  "type": "object",
  "properties": {
    "name": {"type": "string"},
    "x": {"type": "number"},
    "y": {"type": "number"},
    "z": {"type": "number"}
  },
  "required": ["name", "x", "y", "z"]
}
```

--

## Warum ein Schema?

<div class="flow">
  <div class="box">Software A</div>
  <div class="arrow">→</div>
  <div class="box fragment"><strong>gemeinsames Schema</strong></div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Software B</div>
</div>

<br>

- Namen der Felder sind definiert. <!-- .element: class="fragment" -->
- Datentypen sind definiert. <!-- .element: class="fragment" -->
- Pflichtfelder können definiert werden. <!-- .element: class="fragment" -->
- Verschachtelung und Beziehungen sind definiert. <!-- .element: class="fragment" -->

---

## Datenstrukturen in Grasshopper

Für parametrische Modelle ist nicht nur die Geometrie wichtig, sondern auch:

**Wie sind die Daten organisiert?**

<div class="flow">
  <div class="box fragment">Item</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">List</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Data Tree</div>
</div>

--

## Item

Ein einzelner Wert:

```text
5.00
```

Beispiele:

- Zahl <!-- .element: class="fragment" -->
- Punkt <!-- .element: class="fragment" -->
- Kurve <!-- .element: class="fragment" -->
- Text <!-- .element: class="fragment" -->
- Brep <!-- .element: class="fragment" -->

--

## List

Mehrere Elemente in einer linearen Reihenfolge:

```text
[0]  0.00
[1]  2.00
[2]  4.00
[3]  6.00
```

<div class="callout fragment">
Eine Liste besitzt eine Reihenfolge, aber noch keine zusätzliche Gruppierung.
</div>

--

## Data Tree

<div class="tree">{0}
├── [0]  Punkt A0
├── [1]  Punkt A1
└── [2]  Punkt A2

{1}
├── [0]  Punkt B0
├── [1]  Punkt B1
└── [2]  Punkt B2</div>

--

## Was bedeutet `{0}` oder `{1}`?

- `{0}` = erster **Branch / Ast** <!-- .element: class="fragment" -->
- `{1}` = zweiter **Branch / Ast** <!-- .element: class="fragment" -->
- `[0]`, `[1]`, ... = Position eines Elements im Ast <!-- .element: class="fragment" -->

<div class="callout fragment">
Data Trees sind hierarchische Datenstrukturen für zusammengehörige Datengruppen.
</div>

--

## Beispiel aus der Tragwerksplanung

Wir modellieren drei Rahmen mit jeweils vier Stützen.

<div class="tree fragment">{0}  → Rahmen 1 → Stütze 1, 2, 3, 4
{1}  → Rahmen 2 → Stütze 1, 2, 3, 4
{2}  → Rahmen 3 → Stütze 1, 2, 3, 4</div>

<br>

<div class="fragment">
Die Geometrie ist nicht nur eine Liste von 12 Stützen – die <strong>Gruppierung</strong> enthält zusätzliche Information.
</div>

--

## Flatten verändert die Struktur

Vorher:

```text
{0}: A0 A1 A2
{1}: B0 B1 B2
```

Nach `Flatten`:

```text
{0}: A0 A1 A2 B0 B1 B2
```

<div class="callout fragment">
Die Elemente bleiben erhalten – aber Information über ihre Gruppierung geht verloren.
</div>

--

## Graft verändert die Struktur

Vorher:

```text
{0}: A B C
```

Nach `Graft`:

```text
{0;0}: A
{0;1}: B
{0;2}: C
```

<div class="callout fragment">
In parametrischen Modellen kann eine Änderung der Datenstruktur das Ergebnis vollständig verändern.
</div>

---

## IFC
### Nicht einfach „eine 3D-Datei“

IFC beschreibt Vereinbarungen über:

- **Klassen** <!-- .element: class="fragment" -->
- **Eigenschaften** <!-- .element: class="fragment" -->
- **Beziehungen** <!-- .element: class="fragment" -->
- **Geometrie** <!-- .element: class="fragment" -->
- **räumliche Struktur** <!-- .element: class="fragment" -->
- **Metadaten** <!-- .element: class="fragment" -->

--

## Schema und Dateiformat

<div class="two-col">
  <div class="card">
    <h3>IFC Schema</h3>
    <p>Regeln und Klassen zur Beschreibung von Bauwerksinformationen.</p>
  </div>

  <div class="card fragment">
    <h3>Datei</h3>
    <p>Eine konkrete Serialisierung dieser Informationen, z. B. <code>.ifc</code>.</p>
  </div>
</div>

<div class="callout fragment">
<strong>Schema</strong> und <strong>Dateiformat</strong> sind nicht dasselbe.
</div>

--

## IFC-Klassen sind hierarchisch

<div class="tree">IfcRoot
└── IfcObjectDefinition
    └── IfcObject
        └── IfcProduct
            └── IfcElement
                └── ...
                    └── IfcWall</div>

<div class="fragment small">
Eine Klasse erbt Eigenschaften und Beziehungen von übergeordneten Klassen.
</div>

--

## Rooted und Non-rooted

<div class="two-col">
  <div class="card">
    <h3>Rooted</h3>
    <ul>
      <li>eindeutige Identität</li>
      <li>Name / Beschreibung</li>
      <li>Owner History / Metadaten</li>
      <li>für Bauwerksobjekte und Beziehungen</li>
    </ul>
  </div>

  <div class="card fragment">
    <h3>Non-rooted</h3>
    <ul>
      <li>Hilfsobjekte</li>
      <li>Koordinaten</li>
      <li>Vektoren</li>
      <li>geometrische Definitionen</li>
    </ul>
  </div>
</div>

--

## IFC ist ein Netz von Objekten

<div class="flow">
  <div class="box">IfcProject</div>
  <div class="arrow">→</div>
  <div class="box fragment">IfcBuilding</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">IfcBuildingStorey</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">IfcWall</div>
</div>

<br>

<div class="fragment">
Zusätzlich existieren Beziehungen zu Material, Eigenschaften, Geometrie, Typen usw.
</div>

--

## Beispiel: eine Wand in IFC

<div class="tree">IfcWall
├── GlobalId
├── Name
├── ObjectPlacement ─────→ IfcLocalPlacement
├── Representation ──────→ Geometrie
├── IsDefinedBy ─────────→ Property Sets
├── HasAssociations ─────→ Material
└── ContainedInStructure → Geschoss</div>

<div class="callout fragment">
Die Bedeutung entsteht nicht nur durch einzelne Werte, sondern durch die <strong>Beziehungen zwischen Objekten</strong>.
</div>

--

## Ein Blick in eine `.ifc`-Datei

<pre><code class="language-step" data-line-numbers="1-4|5-7">#42=IFCWALL(
  '2Y$abc...',
  #5,
  'W001',
  ...,
  #120,
  #145);
</code></pre>

<div class="fragment small">
Die STEP-Serialisierung verwendet Referenzen wie <code>#120</code> oder <code>#145</code>, um Objekte miteinander zu verknüpfen.
</div>

Note:
Das Beispiel ist absichtlich schematisch und keine vollständige IFC-Instanz. Hier nur das Prinzip der Referenzen erläutern.

---

## Geometriemodell vs. Berechnungsmodell

<div class="two-col">
  <div class="card">
    <h3>Physisches Modell</h3>
    <ul>
      <li>reale Bauteile</li>
      <li>Volumengeometrie</li>
      <li>Schichten / Material</li>
      <li>Architektur / Konstruktion</li>
    </ul>
  </div>

  <div class="card fragment">
    <h3>Analytisches Modell</h3>
    <ul>
      <li>Stäbe / Flächen / Knoten</li>
      <li>Lager</li>
      <li>Querschnitte</li>
      <li>Lasten</li>
    </ul>
  </div>
</div>

--

## IFC Structural

IFC kann auch Objekte für das **analytische Tragwerksmodell** beschreiben.

Beispiele:

```text
IfcStructuralCurveMember
IfcStructuralSurfaceMember
IfcStructuralPointConnection
IfcStructuralLoad...
```

<div class="fragment callout">
Die FE-Software muss diese Informationen anschließend in ihr internes Berechnungsmodell interpretieren.
</div>

---

## SAF
### Structural Analysis Format

Fokus: **Austausch von Statik- bzw. Berechnungsmodellen**

- offenes Austauschformat <!-- .element: class="fragment" -->
- tabellenorientiert <!-- .element: class="fragment" -->
- auf XLSX-Struktur aufgebaut <!-- .element: class="fragment" -->
- für den praktischen Austausch zwischen Statikprogrammen <!-- .element: class="fragment" -->

--

## SAF: Grundprinzip

<div class="flow">
  <div class="box">Structural<br>Points</div>
  <div class="box fragment">Structural<br>Curves</div>
  <div class="box fragment">Materials</div>
  <div class="box fragment">Cross<br>Sections</div>
  <div class="box fragment">Supports</div>
  <div class="box fragment">Loads</div>
</div>

<br>

<div class="fragment small">
Die Informationen werden auf definierte Tabellenblätter verteilt und über IDs miteinander verknüpft.
</div>

--

## Beispiel einer SAF Datei:

<iframe width="640" height="480" style="border:1px solid #eeeeee;" src="https://3dviewer.net/embed.html#model=https://raw.githubusercontent.com/AIztok/SBB/main/docs/FH_SBB_Unterug_v01.ifc$camera=-10.48394,10.67134,-18.34521,5.00000,0.00544,-6.00000,0.00000,1.00000,0.00000,45.00000$projectionmode=perspective$envsettings=fishermans_bastion,off$backgroundcolor=42,43,46,255$defaultcolor=200,200,200$defaultlinecolor=100,100,100$edgesettings=off,0,0,0,1"></iframe>

[SAF Export FE-Modell Unterzug](https://aiztok.github.io/DiTWP/100_Informationen/120_Datenstruktur/121_VO](https://aiztok.github.io/DiTWP/100_Informationen/130_Datenformate/135_SAF#beispiel)
--


## IFC Structural und SAF

<table class="compact">
<thead>
<tr><th></th><th>IFC Structural</th><th>SAF</th></tr>
</thead>
<tbody>
<tr class="fragment"><td>Grundidee</td><td>objektorientiertes IFC-Schema</td><td>tabellenorientiertes Austauschmodell</td></tr>
<tr class="fragment"><td>Schwerpunkt</td><td>Bauwerksinformation + analytisches Modell</td><td>analytisches Modell</td></tr>
<tr class="fragment"><td>Struktur</td><td>Netz aus Objekten & Beziehungen</td><td>Tabellen + IDs</td></tr>
<tr class="fragment"><td>Lesbarkeit</td><td>komplexer</td><td>direkt in Tabellen sichtbar</td></tr>
<tr class="fragment"><td>Typischer Einsatz</td><td>openBIM / Modellintegration</td><td>CAE ↔ CAE</td></tr>
</tbody>
</table>

---

## Beispiel: Export aus einer FE-Software

<div class="flow">
  <div class="box">SOFiSTiK<br>Berechnungsmodell</div>
  <div class="arrow">→</div>
  <div class="box fragment">SAF</div>
  <div class="box fragment">IFC Structural</div>
</div>

<br>

Fragen beim Vergleich:

- Welche Elemente werden exportiert? <!-- .element: class="fragment" -->
- Wie werden Querschnitte und Materialien gespeichert? <!-- .element: class="fragment" -->
- Wie werden Knoten, Stäbe und Lager verknüpft? <!-- .element: class="fragment" -->
- Welche Informationen gehen verloren? <!-- .element: class="fragment" -->

---

## Eine Information – mehrere Strukturen

Beispiel: **Punkt P1 = (10, 20, 0)**

<div class="three-col small">
  <div class="card fragment">
    <h4>CSV</h4>
    <pre><code>P1;10;20;0</code></pre>
  </div>

  <div class="card fragment">
    <h4>JSON</h4>
    <pre><code>{
  "name":"P1",
  "xyz":[10,20,0]
}</code></pre>
  </div>

  <div class="card fragment">
    <h4>Objekt</h4>
    <pre><code>Point(
  name="P1",
  x=10,
  y=20,
  z=0
)</code></pre>
  </div>
</div>

--

## Welche Struktur ist die beste?

<div class="fragment">
<strong>Keine allgemein.</strong>
</div>

<br>

Die passende Struktur hängt ab von:

- Art und Komplexität der Information <!-- .element: class="fragment" -->
- benötigten Beziehungen <!-- .element: class="fragment" -->
- Software und Schnittstelle <!-- .element: class="fragment" -->
- Lesbarkeit für Menschen <!-- .element: class="fragment" -->
- Effizienz für Maschinen <!-- .element: class="fragment" -->

---

## Vergleich

<table class="compact">
<thead>
<tr>
  <th></th>
  <th>CSV</th>
  <th>JSON</th>
  <th>IFC</th>
  <th>SAF</th>
</tr>
</thead>
<tbody>
<tr class="fragment"><td>Grundstruktur</td><td>Tabelle</td><td>Hierarchie</td><td>Objektnetz</td><td>Tabellen</td></tr>
<tr class="fragment"><td>Verschachtelung</td><td>gering</td><td>sehr gut</td><td>sehr komplex</td><td>über IDs</td></tr>
<tr class="fragment"><td>Menschenlesbar</td><td>sehr gut</td><td>gut</td><td>begrenzt</td><td>gut</td></tr>
<tr class="fragment"><td>Typischer Zweck</td><td>einfache Daten</td><td>Datenaustausch / APIs</td><td>Bauwerksinformation</td><td>Statikmodell</td></tr>
</tbody>
</table>

---

## Drei Begriffe unterscheiden

<div class="three-col">
  <div class="card fragment">
    <h3>Daten</h3>
    <p>Konkrete Werte</p>
    <code>0.20</code>
  </div>

  <div class="card fragment">
    <h3>Struktur</h3>
    <p>Anordnung und Beziehungen</p>
    <code>wall.width</code>
  </div>

  <div class="card fragment">
    <h3>Schema</h3>
    <p>Regeln für diese Struktur</p>
    <code>width: number</code>
  </div>
</div>

--

## Merksatz

<div class="callout" style="font-size:1.15em;">
<strong>Daten werden erst durch ihre Struktur und ein gemeinsames Schema zuverlässig austauschbar.</strong>
</div>

<br>

<div class="fragment">
In der digitalen Tragwerksplanung ist deshalb nicht nur wichtig, <strong>welche</strong> Informationen vorhanden sind, sondern auch <strong>wie</strong> sie organisiert und verknüpft sind.
</div>

---

## Takeaways

1. **Klassen** definieren Eigenschaften von Objekten. <!-- .element: class="fragment" -->
2. **CSV** eignet sich für einfache tabellarische Daten. <!-- .element: class="fragment" -->
3. **JSON** kann komplexe hierarchische Strukturen abbilden. <!-- .element: class="fragment" -->
4. **Grasshopper Data Trees** speichern Gruppierung als Teil des parametrischen Modells. <!-- .element: class="fragment" -->
5. **IFC** beschreibt Bauwerksinformationen als Klassen und Beziehungen. <!-- .element: class="fragment" -->
6. **SAF / IFC Structural** fokussieren auf den Austausch analytischer Modelle. <!-- .element: class="fragment" -->

--

## Weiterführende Kursseiten

- [121_VO – Datenstrukturen](https://aiztok.github.io/DiTWP/100_Informationen/120_Datenstruktur/121_VO)
- [132_JSON](https://aiztok.github.io/DiTWP/100_Informationen/130_Datenformate/132_JSON)
- [133_CSV & XLSX](https://aiztok.github.io/DiTWP/100_Informationen/130_Datenformate/133_CSV-and-XLSX)
- [134_IFC](https://aiztok.github.io/DiTWP/100_Informationen/130_Datenformate/134_IFC)
- [135_SAF](https://aiztok.github.io/DiTWP/100_Informationen/130_Datenformate/135_SAF)
- [Grasshopper – Datenstruktur](https://aiztok.github.io/DiTWP/000_Einfuehrung/010_Software/013_Grasshopper)

---
