---
version: alpha
name: Generative Noodles
description: >
  Corporate Identity dieser App. Tokens übernommen aus der DESIGN.md des
  Bitcoin-Wiki-Visualizers
  (github.com/TLausZ/Bitcoin-Knowledge-Base-WIKI/blob/main/Visualizer/DESIGN.md),
  Format nach github.com/google-labs-code/design.md. Tokens haben Vorrang vor
  eigenen Annahmen.
omitted:
  - Elevation & Depth
colors:
  primary: "{colors.ink}"
  paper: "#ece2cd"                      # Arbeitsfläche, Panel, Klappe
  paper-bright: "#f2ead6"               # Eingabefelder, Text auf dunklen Flächen
  ink: "#5c4a34"                        # Titel, Buttontext, Slider-Griff, aktiver Grund
  ink-soft: "#6b5a42"                   # Beschriftungen der Regler
  ink-faint: "#8a7a5e"                  # Untertitel, Sektionen, Werte, Statuszeile, Hinweis
  line: "#000000"                       # Noodle-Konturen und Grafiken, siehe Abweichungen
  border: "rgba(110,92,64,0.25)"        # Trennlinien im Panel, Rasterlinien
  border-strong: "rgba(110,92,64,0.4)"  # Panel-, Klappen-, Button- und Blattrahmen
  bar: "rgba(110,92,64,0.18)"           # Slider-Schiene, blockierte Zellen
typography:
  title:
    fontFamily: "ui-sans-serif, system-ui, sans-serif"
    fontSize: 15px
    fontWeight: 600
  base:
    fontFamily: "ui-sans-serif, system-ui, sans-serif"
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.4
  ui:
    fontFamily: "ui-sans-serif, system-ui, sans-serif"
    fontSize: 12px
    fontWeight: 400
  label:
    fontFamily: "ui-sans-serif, system-ui, sans-serif"
    fontSize: 11px
    fontWeight: 400
rounded:
  button: 4px
spacing:
  page: 16px                            # Abstand von Panel und Hinweis zum Fensterrand
  panel: 12px                           # Innenabstand des Panels
  control: 8px                          # Abstand benachbarter Bedienelemente
components:
  button:
    backgroundColor: transparent
    textColor: "{colors.ink}"
    typography: "{typography.ui}"
    rounded: "{rounded.button}"
  button-active:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.paper-bright}"
  flap:
    backgroundColor: "{colors.paper}"
    textColor: "{colors.ink}"
    width: 18px
    height: 34px
---

## Overview

Alte topografische Vermessungskarte: Sepia-Papier, dünne braune Konturen,
zurückhaltende Beschriftung. Eine einzige Farbfamilie, kein reines Schwarz, kein
reines Weiss, keine Akzentfarbe. Flächen sind deckend, Linien nie. Keine
Schatten, keine Verläufe, keine Übergänge.

## Layout

Zwei Panels von je 276px Breite, oben links die Regler, oben rechts Grafiken und
Maske. Jedes hat eine angesetzte Klappe von 18 x 34px an seiner inneren Kante,
das rechte spiegelbildlich zum linken. Zugeklappt bleibt nur die Klappe stehen;
sie rückt an den Fensterrand und schliesst ihren Rahmen. Auf schmalen Fenstern
(unter 680px Breite oder 520px Höhe) sitzen beide unten, füllen die Fensterbreite
und starten zugeklappt; das Öffnen des einen schliesst das andere.

Das Blatt liegt zentriert in der Arbeitsfläche, in `paper-bright` mit einem
Rahmen in `border-strong` statt eines Schlagschattens.

## Zeichnung

Die Zeichnung selbst steht ausserhalb der Palette: schwarze Konturen auf weissem
Blatt, volle Deckkraft. Sie ist das Werkstück, nicht Teil des Interface, und muss
auf jedem Papier und in jeder Plotter-Software eindeutig sein. Das gespeicherte
SVG hat keinen Hintergrund, die Linien liegen schwarz auf transparent.

Rasterlinien in `border`, blockierte Zellen als Fläche in `bar`. Beide sind
Zeichenhilfen und erscheinen nie im gespeicherten SVG.

## Abweichungen von der Quelle

Die Interface-Sprache ist hier Englisch, nicht Deutsch: das Repository ist
öffentlich und englisch dokumentiert.

Die Regel «kein reines Schwarz, kein reines Weiss» gilt nur für das Interface.
Blatt und Zeichnung sind weiss und schwarz, weil sie das Ergebnis sind und nicht
die Umgebung. Alles Übrige folgt der Quelle.
