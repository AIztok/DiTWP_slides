## Digitale Tragwerksplanung
### Verwalten & Schnittstellen

**Wie bleiben digitale Informationen nachvollziehbar, teilbar und vergleichbar?**

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

---

## Dateibenennung
### Der einfachste Metadatenspeicher

Ein guter Dateiname beantwortet bereits mehrere Fragen.

<div class="flow">
  <div class="box fragment">Projekt</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Bauwerk</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Bauteil</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Inhalt/Plantyp/...</div>
  <div class="arrow fragment">+</div>
  <div class="box fragment">Status / Version</div>
</div>

<br>

```text
DiTWP_ZBW-W_LT_SP_V01.pdf
```

--

## Robuste Namenskonventionen

- kurz, eindeutig und dokumentiert <!-- .element: class="fragment" -->
- konsistente Codes und Abkürzungen <!-- .element: class="fragment" -->
- ISO-Datum YYYY-MM-DD oder YYYYMMDD, wenn Datum relevant ist <!-- .element: class="fragment" -->
- Leerzeichen und Sonderzeichen möglichst vermeiden <!-- .element: class="fragment" -->
- Konvention in einer README/Anweisung dokumentieren <!-- .element: class="fragment" -->

--

<div class="callout fragment">
Der Zweck ist nicht „schöne Dateinamen“, sondern <strong>eindeutige, sortierbare und maschinenlesbare Information</strong>.
</div>

---

## Versionsverwaltung im Bauprojekt

<div class="two-col small">
  <div class="card">
    <h6>Intern</h6>
    <ul>
      <li>Arbeitsordner</li>
      <li>persönliche Bereiche</li>
      <li>Projektserver</li>
      <li>Planqualitätsprüfung</li>
    </ul>
  </div>
  <div class="card fragment">
    <h6>Extern</h6>
    <ul>
      <li>Planmanagement</li>
      <li>Prüf- und Freigabeprozesse</li>
      <li>Projektplattform / CDE</li>
    </ul>
  </div>
</div>

---

## Common Data Environment · CDE

Ein CDE ist im Sinn der ÖNORM ISO 19650 die vereinbarte Umgebung bzw. der Prozess, über den Projektinformationen erzeugt, geprüft, geteilt, freigegeben und archiviert werden. 

--

Ein CDE ist nicht zwingend ein bestimmtes Softwarepaket, sondern ein **gemeinsamer Informationsprozess**

CDE besteht aus:
- Dokumentmanagementsystem <!-- .element: class="fragment" -->
- Modellverwaltung <!-- .element: class="fragment" -->
- Kommunikations- und Kollaborations-Tools <!-- .element: class="fragment" -->
- Zugriffs- und Berechtigungsmanagement <!-- .element: class="fragment" -->
- Protokollierung und Nachvollziehbarkeit (Audit-Trail) <!-- .element: class="fragment" -->

--

Phasen / Bereiche jeder Information im CDE:
<div class="four-col">
  <div class="state fragment"><strong>WIP</strong><br><small>Work in Progress</small></div>
  <div class="state fragment"><strong>Shared</strong><br><small>Koordination / Prüfung</small></div>
  <div class="state fragment"><strong>Published</strong><br><small>freigegebene Information</small></div>
  <div class="state fragment"><strong>Archive</strong><br><small>nachvollziehbare Historie</small></div>
</div>

<div class="source-link">Vereinfachte Darstellung nach ISO-19650-orientiertem CDE-Workflow.</div>

---

## Was ist Git?

**Git = verteiltes Versionskontrollsystem**

- speichert nachvollziehbare Zustände eines Projekts <!-- .element: class="fragment" -->
- jede Änderung kann beschrieben werden <!-- .element: class="fragment" -->
- mehrere Arbeitsstände können parallel existieren <!-- .element: class="fragment" -->
- Historie bleibt reproduzierbar <!-- .element: class="fragment" -->

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

## Branches
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

---

## Version ≠ Revision ≠ Status

<table class="compact">
<thead>
<tr><th>Begriff</th><th>Frage</th><th>Beispiel</th></tr>
</thead>
<tbody>
<tr class="fragment"><td><strong>Version</strong></td><td>Welcher Bearbeitungsstand?</td><td>V01_2026-10-04 oder V01.1</td></tr>
<tr class="fragment"><td><strong>Revision</strong></td><td>Welcher formal ausgegebene Änderungsstand?</td><td>V01, P01, F02</td></tr>
<tr class="fragment"><td><strong>Status</strong></td><td>Wofür darf der Stand verwendet werden?</td><td>WIP, Prüfung, Freigabe</td></tr>
</tbody>
</table>

<div class="warning fragment">
Die konkrete Codierung ist projektabhängig. Entscheidend ist, dass Bedeutung und Prozess eindeutig definiert sind.
</div>


---

## Schnittstellen

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

---

## Takeaways

- Dateibenennung ist die einfachste Form von **Metadatenmanagement**. <!-- .element: class="fragment" -->
- CDE-Prozesse verwalten **Zustand, Freigabe und Verantwortung**. <!-- .element: class="fragment" -->
- Git macht Änderungen **nachvollziehbar und parallel bearbeitbar**. <!-- .element: class="fragment" -->
- Schnittstellen können datei-, repository-, objekt- oder API-basiert sein. <!-- .element: class="fragment" -->
