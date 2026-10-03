## Digitale Tragwerksplanung
### Verwalten & Schnittstellen

**Wie bleiben digitale Informationen nachvollziehbar, teilbar und vergleichbar?**

<small class="muted">311 · Vorlesung · ca. 90 min</small>

Note:
Roter Faden: Wir beginnen bei der einfachsten Form der Verwaltung – dem Dateinamen – und gehen schrittweise zu CDE, Git, modellbasierter Versionsverwaltung und Schnittstellen über.

---

## Warum überhaupt verwalten?

<div class="two-col">
  <div>
    <ul>
      <li class="fragment">Wer hat etwas geändert?</li>
      <li class="fragment">Wann wurde es geändert?</li>
      <li class="fragment">Warum wurde es geändert?</li>
      <li class="fragment">Welche Version ist gültig?</li>
      <li class="fragment">Was hat sich fachlich geändert?</li>
    </ul>
  </div>

  <div>
    <img
      class="image-small"
      src="https://aiztok.github.io/DiTWP/Bilder/311_Datenname.png"
      alt="XKCD file naming"
    >
    <div class="attribution">Quelle: XKCD 1459</div>
  </div>
</div>

Note:
Einstieg über ein alltägliches Problem. Ziel: zeigen, dass Versionsverwaltung kein Softwarethema ist, sondern Informationsmanagement.

--

## Lernziele

Nach dieser Einheit sollen Sie erklären können:

- wie Dateinamen **Information strukturieren** <!-- .element: class="fragment" -->
- warum **Version, Revision und Status** nicht dasselbe sind <!-- .element: class="fragment" -->
- was ein **CDE** im Projekt leistet <!-- .element: class="fragment" -->
- wie **Git, Branch, Commit, Pull Request und Merge** zusammenhängen <!-- .element: class="fragment" -->
- warum **Text-Diff ≠ Modell-Diff** ist <!-- .element: class="fragment" -->
- wie sich Datei-, Repository-, Modell- und API-Schnittstellen unterscheiden <!-- .element: class="fragment" -->

---

## 1 · Dateibenennung
### Der einfachste Metadatenspeicher

Ein guter Dateiname beantwortet bereits mehrere Fragen.

<div class="flow">
  <div class="box fragment">Projekt</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Bauwerk</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Bauteil</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Status / Version</div>
</div>

<br>

```text
DiTWP_ZBW-W_LT_V01_2026-09-16.ifc
```

--

## Robuste Namenskonventionen

- kurz, eindeutig und dokumentiert <!-- .element: class="fragment" -->
- konsistente Codes und Abkürzungen <!-- .element: class="fragment" -->
- ISO-Datum `YYYY-MM-DD`, wenn Datum relevant ist <!-- .element: class="fragment" -->
- Leerzeichen und Sonderzeichen möglichst vermeiden <!-- .element: class="fragment" -->
- Konvention in einer `README.md` dokumentieren <!-- .element: class="fragment" -->

<div class="callout fragment">
Der Zweck ist nicht „schöne Dateinamen“, sondern <strong>eindeutige, sortierbare und maschinenlesbare Information</strong>.
</div>

--

## Version ≠ Revision ≠ Status

<table class="compact">
<thead>
<tr><th>Begriff</th><th>Frage</th><th>Beispiel</th></tr>
</thead>
<tbody>
<tr class="fragment"><td><strong>Version</strong></td><td>Welcher Bearbeitungsstand?</td><td>V01, V02, V03</td></tr>
<tr class="fragment"><td><strong>Revision</strong></td><td>Welcher formal ausgegebene Änderungsstand?</td><td>Rev. A, Rev. B</td></tr>
<tr class="fragment"><td><strong>Status</strong></td><td>Wofür darf der Stand verwendet werden?</td><td>WIP, Prüfung, Freigabe</td></tr>
</tbody>
</table>

<div class="warning fragment">
Die konkrete Codierung ist projektabhängig. Entscheidend ist, dass Bedeutung und Prozess eindeutig definiert sind.
</div>

---

## 2 · Versionsverwaltung im Bauprojekt

<div class="two-col">
  <div class="card">
    <h3>Intern</h3>
    <ul>
      <li>Arbeitsordner</li>
      <li>persönliche Bereiche</li>
      <li>Projektserver</li>
      <li>Planqualitätsprüfung</li>
    </ul>
  </div>
  <div class="card fragment">
    <h3>Extern</h3>
    <ul>
      <li>Planmanagement</li>
      <li>Prüf- und Freigabeprozesse</li>
      <li>EPLASS / EXAKT / CDES</li>
      <li>Projektplattform / CDE</li>
    </ul>
  </div>
</div>

--

## Common Data Environment · CDE

Ein CDE ist kein bestimmtes Produkt, sondern ein **gemeinsamer Informationsprozess**.

<div class="four-col">
  <div class="state fragment"><strong>WIP</strong><br><small>Work in Progress</small></div>
  <div class="state fragment"><strong>Shared</strong><br><small>Koordination / Prüfung</small></div>
  <div class="state fragment"><strong>Published</strong><br><small>freigegebene Information</small></div>
  <div class="state fragment"><strong>Archive</strong><br><small>nachvollziehbare Historie</small></div>
</div>

<div class="source-link">Vereinfachte Darstellung nach ISO-19650-orientiertem CDE-Workflow.</div>

--

## CDE: Information wechselt den Zustand

<div class="flow">
  <div class="box">WIP</div>
  <div class="arrow">→</div>
  <div class="box fragment">Prüfen</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Shared</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Freigeben</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Published</div>
</div>

<br>

<div class="callout fragment">
Nicht nur die Datei ist wichtig – auch <strong>Zustand, Verantwortlichkeit und Freigabe</strong> gehören zur Information.
</div>

--

## CDE und Git: ähnliche Prinzipien

<table class="compact">
<thead><tr><th>Bauwesen</th><th>Softwareentwicklung</th></tr></thead>
<tbody>
<tr class="fragment"><td>Arbeitsstand</td><td>Branch / lokaler Arbeitsstand</td></tr>
<tr class="fragment"><td>Version / Änderung</td><td>Commit</td></tr>
<tr class="fragment"><td>Prüfung / Freigabe</td><td>Review / Pull Request</td></tr>
<tr class="fragment"><td>Zusammenführen</td><td>Merge</td></tr>
<tr class="fragment"><td>Projektplattform</td><td>Repository-Plattform</td></tr>
</tbody>
</table>

<div class="warning fragment">
Das ist eine <strong>Analogie</strong>, keine 1:1-Abbildung. Ein CDE ersetzt Git nicht – und Git ersetzt keinen projektspezifischen Freigabeprozess.
</div>

---

## 3 · Was ist Git?

**Git = verteiltes Versionskontrollsystem**

- speichert nachvollziehbare Zustände eines Projekts <!-- .element: class="fragment" -->
- jede Änderung kann beschrieben werden <!-- .element: class="fragment" -->
- mehrere Arbeitsstände können parallel existieren <!-- .element: class="fragment" -->
- Historie bleibt reproduzierbar <!-- .element: class="fragment" -->
- lokal nutzbar – ein Onlinedienst ist nicht zwingend nötig <!-- .element: class="fragment" -->

--

## Git ≠ GitHub

<div class="two-col">
  <div class="card">
    <h3>Git</h3>
    <ul>
      <li>Versionskontrolle</li>
      <li>Commits</li>
      <li>Branches</li>
      <li>Merges</li>
      <li>lokal verwendbar</li>
    </ul>
  </div>
  <div class="card fragment">
    <h3>GitHub / GitLab</h3>
    <ul>
      <li>Hosting von Repositories</li>
      <li>Benutzer & Rechte</li>
      <li>Pull Requests</li>
      <li>Reviews</li>
      <li>Zusammenarbeit online</li>
    </ul>
  </div>
</div>

--

## Commit = nachvollziehbarer Zustand

```text
commit 9f4b3c1
Author: Projektteam
Date:   2026-09-16

    PSet_ConcreteElementGeneral ergänzt
```

Ein guter Commit beantwortet:

- **Was** wurde geändert? <!-- .element: class="fragment" -->
- **Warum** wurde es geändert? <!-- .element: class="fragment" -->
- **Wer** hat es geändert? <!-- .element: class="fragment" -->
- **Wann** wurde es geändert? <!-- .element: class="fragment" -->

---

## 4 · Branches
### Parallel arbeiten ohne den Hauptstand zu überschreiben

<div class="branchline">
  <div class="branchlabel">main</div>
  <div class="commits">
    <span class="commit">A</span><span class="line"></span><span class="commit">B</span><span class="line"></span><span class="commit fragment">E</span>
  </div>
</div>

<div class="branchline fragment">
  <div class="branchlabel">feature</div>
  <div class="commits">
    <span class="commit">B</span><span class="line"></span><span class="commit">C</span><span class="line"></span><span class="commit">D</span>
  </div>
</div>

--

## Feature Branch

Typische Anwendung:

> „Wir probieren eine alternative Lösung aus, ohne den abgestimmten Hauptstand zu verändern.“

Beispiele aus der Tragwerksplanung:

- alternative Stützenstellung <!-- .element: class="fragment" -->
- andere Querschnittsabmessungen <!-- .element: class="fragment" -->
- geänderte Bauphase <!-- .element: class="fragment" -->
- zusätzliche Property Sets <!-- .element: class="fragment" -->

--

## Vorsicht mit der BIM-Analogie

<div class="two-col">
  <div class="card">
    <h3>Branch</h3>
    <p>Alternative Entwicklung <strong>desselben Informationsbestands</strong>.</p>
  </div>
  <div class="card fragment">
    <h3>Fachmodell</h3>
    <p>Architektur-, Tragwerks- und TGA-Modell sind meist <strong>separate Informationsmodelle</strong>.</p>
  </div>
</div>

<div class="warning fragment">
Fachmodelle werden häufig <strong>referenziert, föderiert und koordiniert</strong> – nicht wie zwei Git-Branches zeilenweise zusammengeführt.
</div>

--

## Typischer GitHub-Workflow

<div class="flow">
  <div class="box fragment">Branch</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Ändern</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Commit</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Pull Request</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Review</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Merge</div>
</div>

Note:
Hier nicht die GitHub-Oberfläche erklären, sondern das Prinzip. Die Klickschritte gehören in die Übung bzw. die Git-Unterseite.

---

## 5 · Pull Request & Review

Ein Pull Request ist eine **Änderungsanfrage**.

- Welche Änderungen sollen übernommen werden? <!-- .element: class="fragment" -->
- Welche Dateien sind betroffen? <!-- .element: class="fragment" -->
- Was wurde hinzugefügt / gelöscht? <!-- .element: class="fragment" -->
- Gibt es Kommentare oder Rückfragen? <!-- .element: class="fragment" -->
- Ist ein Merge technisch möglich? <!-- .element: class="fragment" -->

--

## Diff: Änderungen sichtbar machen

<img class="image-wide" src="https://aiztok.github.io/DiTWP/Bilder/Pasted-image-20240930125622.png" alt="GitHub diff example">

<div class="attribution">Beispiel aus der DiTWP-Seite: Änderungen einer Markdown-Datei in GitHub.</div>

---

## 6 · Merge-Konflikte

Git kann viele Änderungen automatisch zusammenführen.

Ein Konflikt entsteht typischerweise, wenn:

- dieselbe Zeile unterschiedlich geändert wurde <!-- .element: class="fragment" -->
- eine Datei auf einer Seite gelöscht und auf der anderen geändert wurde <!-- .element: class="fragment" -->
- Git nicht eindeutig entscheiden kann, welcher Inhalt gelten soll <!-- .element: class="fragment" -->

--

## GitHub erkennt den Konflikt

<img class="image-wide" src="https://aiztok.github.io/DiTWP/Bilder/311_VO_Github_07.png" alt="GitHub merge conflict">

<div class="attribution">Beispiel aus der DiTWP-Seite.</div>

--

## Konfliktmarker

```text [1|2|3|4|5]
<<<<<<< feature
5.) Arbeitsfuge nicht bearbeiten
=======
5.) Arbeitsfuge gründlich bearbeiten
>>>>>>> main
```

<div class="callout fragment">
Git markiert den Konflikt – <strong>der Mensch muss die fachlich richtige Lösung festlegen</strong>.
</div>

--

## Konflikt direkt im Editor

<img class="image-wide" src="https://aiztok.github.io/DiTWP/Bilder/311_VO_Github_08.png" alt="GitHub conflict editor">

<div class="attribution">Beispiel aus der DiTWP-Seite.</div>

---

## 7 · Textdateien und binäre Dateien

<table class="compact">
<thead><tr><th>Textbasiert</th><th>Binär / proprietär</th></tr></thead>
<tbody>
<tr><td><code>.md</code>, <code>.py</code>, <code>.json</code>, <code>.csv</code>, <code>.ifc</code> (SPF)</td><td><code>.xlsx</code>, <code>.docx</code>, <code>.3dm</code>, viele native CAD/BIM-Dateien</td></tr>
<tr class="fragment"><td>zeilenweiser Diff gut möglich</td><td>Datei kann versioniert werden</td></tr>
<tr class="fragment"><td>Merge oft möglich</td><td>inhaltlicher Diff/Merge meist eingeschränkt</td></tr>
</tbody>
</table>

--

## Git kann auch Binärdateien versionieren

Was bleibt sichtbar?

- Wer hat hochgeladen? <!-- .element: class="fragment" -->
- Wann? <!-- .element: class="fragment" -->
- Welche Commit-Beschreibung? <!-- .element: class="fragment" -->
- Welche Dateiversion gehört zu welchem Projektstand? <!-- .element: class="fragment" -->

<div class="warning fragment">
Was meistens fehlt: ein verständlicher <strong>fachlicher Diff</strong> innerhalb der Datei.
</div>

--

## Große Binärdateien: Git LFS

**Git LFS** ersetzt große Dateien im Repository durch kleine Pointer-Dateien und verwaltet den eigentlichen Inhalt separat.

Typische Kandidaten:

- große Punktwolken <!-- .element: class="fragment" -->
- große native CAD-/BIM-Dateien <!-- .element: class="fragment" -->
- große Ergebnisdateien <!-- .element: class="fragment" -->

<div class="source-link">Weiterführend: GitHub Docs · About Git Large File Storage</div>

---

## 8 · IFC und Git

Die verbreitete `.ifc`-Datei verwendet meist **IFC-SPF**.

```text
ISO-10303-21;
HEADER;
...
DATA;
#57=IFCPROPERTYSET(...);
#58=IFCDEFINESBYPROPERTIES(...);
...
ENDSEC;
END-ISO-10303-21;
```

<div class="callout fragment">
IFC-SPF ist textbasiert – daher kann Git grundsätzlich einen Zeilen-Diff anzeigen.
</div>

--

## Beispiel: IFC-Diff in GitHub

<img class="image-wide" src="https://aiztok.github.io/DiTWP/Bilder/311_VO_Github_ifc_7.png" alt="IFC GitHub diff">

<div class="attribution">Beispiel: PSet wurde in einer IFC-Datei ergänzt.</div>

--

## Aber: Text-Diff ≠ Modell-Diff

Ein Text-Diff beantwortet:

> Welche **Zeilen** sind anders?

Ein Ingenieur möchte oft wissen:

> Welche **Bauteile, Geometrien oder Eigenschaften** sind anders?

<div class="warning fragment">
Eine kleine fachliche Änderung kann beim erneuten IFC-Export sehr viele Textzeilen verändern.
</div>

--

## STEP-Instanznummern sind nicht stabil

```text
#123=IFCWALL(...);
```

`#123` identifiziert eine Instanz **innerhalb dieser Datei**.

<div class="two-col">
  <div class="card fragment">
    <h3>STEP-ID</h3>
    <p>lokal innerhalb der Serialisierung</p>
    <p>kann sich beim neuen Export ändern</p>
  </div>
  <div class="card fragment">
    <h3>GlobalId</h3>
    <p>für IfcRoot-Objekte</p>
    <p>soll über Austauschstände persistent bleiben</p>
  </div>
</div>

--

## Semantischer IFC-Diff

Statt Zeilen zu vergleichen, werden **Objekte** verglichen.

<div class="flow">
  <div class="box fragment">Added</div>
  <div class="box fragment">Deleted</div>
  <div class="box fragment">Changed</div>
</div>

<br>

```python [1|3-7]
from ifcdiff import IfcDiff

diff = IfcDiff("old.ifc", "new.ifc", "diff.json")
diff.diff()
print(diff.change_register)
diff.export()
```

<div class="source-link">IfcOpenShell · IfcDiff</div>

---

## 9 · Speckle
### Versionierung auf Modellebene

Speckle arbeitet mit strukturierten Modellobjekten statt nur mit Dateien.

- neue Sendung → neue Modellversion <!-- .element: class="fragment" -->
- Versionen sind zeitlich nachvollziehbar <!-- .element: class="fragment" -->
- Änderungen zwischen Versionen können verglichen werden <!-- .element: class="fragment" -->
- Geometrie, Parameter und Struktur können Gegenstand des Vergleichs sein <!-- .element: class="fragment" -->

<div class="callout fragment">
Git ist eine gute Analogie – technisch ist Speckle aber keine einfache „Git-Version für 3D-Dateien“.
</div>

--

## Datei-Diff vs. Modell-Diff

<div class="two-col">
  <div class="card">
    <h3>Git</h3>
    <p><strong>Datei / Text</strong></p>
    <p>„Welche Zeilen oder Dateien änderten sich?“</p>
  </div>
  <div class="card fragment">
    <h3>Speckle / IfcDiff</h3>
    <p><strong>Objekt / Modell</strong></p>
    <p>„Welche Bauteile oder Eigenschaften änderten sich?“</p>
  </div>
</div>

---

## 10 · Schnittstellen

Eine Schnittstelle definiert, **wie Information zwischen Systemen übertragen wird**.

<table class="compact">
<thead><tr><th>Prinzip</th><th>Übertragen wird</th><th>Beispiel</th></tr></thead>
<tbody>
<tr class="fragment"><td>Dateibasiert</td><td>komplette Datei</td><td>IFC, SAF</td></tr>
<tr class="fragment"><td>Repository-basiert</td><td>versionierter Informationsbestand</td><td>Git</td></tr>
<tr class="fragment"><td>Objektbasiert</td><td>strukturierte Modellobjekte</td><td>Speckle</td></tr>
<tr class="fragment"><td>API-basiert</td><td>Anfragen / Antworten zwischen Software</td><td>REST API</td></tr>
</tbody>
</table>

--

## Der rote Faden

<div class="flow">
  <div class="box fragment">Dateiname</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">CDE</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Git</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">IFC-Diff</div>
  <div class="arrow fragment">→</div>
  <div class="box fragment">Speckle / API</div>
</div>

<br>

<div class="callout fragment">
Mit zunehmender Digitalisierung verschiebt sich die Frage von <strong>„Welche Datei ist neu?“</strong> zu <strong>„Welche Information hat sich fachlich geändert?“</strong>.
</div>

---

## Takeaways

- Dateibenennung ist die einfachste Form von **Metadatenmanagement**. <!-- .element: class="fragment" -->
- CDE-Prozesse verwalten **Zustand, Freigabe und Verantwortung**. <!-- .element: class="fragment" -->
- Git macht Änderungen **nachvollziehbar und parallel bearbeitbar**. <!-- .element: class="fragment" -->
- GitHub ergänzt Git um **Review und Zusammenarbeit**. <!-- .element: class="fragment" -->
- Binärdateien können versioniert werden, aber sind schwerer zu vergleichen. <!-- .element: class="fragment" -->
- IFC-SPF ist textbasiert, trotzdem ist ein **semantischer Modelldiff** oft aussagekräftiger als ein Textdiff. <!-- .element: class="fragment" -->
- Schnittstellen können datei-, repository-, objekt- oder API-basiert sein. <!-- .element: class="fragment" -->

--

## Weiterführende Quellen

<div class="small" style="text-align:left">

- DiTWP · 311_VO: https://aiztok.github.io/DiTWP/300_Informationen_teilen/310_Verwalten-and-Schnittstellen/311_VO
- UK BIM Framework · Guidance Part C: Common Data Environment
- GitHub Docs · Branches, Pull Requests, Merge Conflicts, Git LFS
- buildingSMART · IFC Formats / Software Identity
- IfcOpenShell · IfcDiff
- Speckle Docs · Compare Versions

</div>

<div class="source-link">Die Beispiele und Screenshots stammen – soweit nicht anders angegeben – aus der DiTWP-Kursseite.</div>
