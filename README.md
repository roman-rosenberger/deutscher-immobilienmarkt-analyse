# Der deutsche Immobilienmarkt 2005 bis 2024 — Python-Analyse

Hypothesengetriebene Analyse quartalsweiser Kaufpreise in 21 deutschen Städten und drei Immobilientypen zwischen 2005 und 2024, umgesetzt in Python mit pandas und Plotly. Der Fokus liegt auf einer sauber dokumentierten Vorgehensweise: Hypothesen vorab formuliert, Datenqualität transparent behandelt, Ergebnisse gegen einen Robustheitscheck geführt und Zusatzbefunde offen ausgewiesen. Abschlussprojekt der IHK-Weiterbildung Data Analyst bei DataSmart Point (2026).

## Projektüberblick

Der deutsche Immobilienmarkt wird häufig als eine zusammenhängende Entwicklung beschrieben — „die Preise steigen", „der Markt boomt", „die Zinswende hat den Markt beendet". Diese Verallgemeinerungen verdecken, dass sich der Markt zeitlich, regional und nach Immobilientyp sehr unterschiedlich verhält.

Diese Analyse prüft drei Hypothesen an einem Datensatz von rund 20 Jahren:

- **H1:** Der Gesamtmarkt zeigt einen klaren, sich beschleunigenden Aufwärtstrend.
- **H2:** Die Preisunterschiede zwischen Städten haben sich nicht nur absolut, sondern auch relativ vergrößert.
- **H3:** Wohnungen (apartment) sind stärker gestiegen als Einfamilien- und Mehrfamilienhäuser.

Ergänzt wird die Analyse um einen Krisenvergleich (Finanzkrise 2008 versus Zinswende 2022), eine Vertiefung zur Volatilität von Mehrfamilienhäusern und einen Bonusteil zur Erschwinglichkeit von Wohneigentum.

## Datengrundlage

Der Datensatz stammt aus dem Kaggle-Set [„German City-Level Housing Market Dataset"](https://www.kaggle.com/datasets/meenaaditya/german-city-housing-market-dataset/data), das GREIX-Transaktionspreise, City-Metrics-Verteilungsdaten und GREIX-Erschwinglichkeitsindikatoren des Kiel-Instituts für Weltwirtschaft bündelt.

| Kennzahl | Wert |
| --- | --- |
| Städte | 21 |
| Immobilientypen | single_family, apartment, multi_family |
| Zeitraum | 2005 bis 2024, quartalsweise |
| Kernkennzahl | Transaktionspreis je m² (`price_m2`) |

**Umgang mit Datenqualität.** Der Rohdatensatz enthielt zusätzliche Spalten (Durchschnitts-, Median- und Perzentilpreise sowie eine Erschwinglichkeitskennzahl), die pro Stadt und Quartal widersprüchliche Werte enthielten — vermutlich durch einen nicht eindeutigen Merge beim Zusammenbau aus mehreren Quellen. Diese Spalten wurden aus der Hauptanalyse ausgeschlossen und nur der eindeutig belastbare `price_m2` verwendet. Die Erschwinglichkeitskennzahl wird im Bonusteil mit transparent dokumentierter Bereinigung (Mittelwert der Duplikate je Stadt und Jahr) dennoch einbezogen.

## Kernergebnisse

### H1 — Beschleunigter Aufwärtstrend, gefolgt von einem einzelnen Einbruchsjahr

Der durchschnittliche Kaufpreis je m² stieg von rund 1.700 € (2005) auf bis zu 4.300 € (Anfang 2022) — eine Verdopplung. Eine datengetriebene Phaseneinteilung anhand der jährlichen Wachstumsraten liefert vier statt der zunächst grob geschätzten drei Phasen:

| Phase | Zeitraum | Ø Wachstum pro Jahr |
| --- | --- | --- |
| Vorkrise und Finanzkrise | 2005 – 2008 | −0,12 % |
| Moderate Erholung | 2009 – 2014 | 4,13 % |
| Boomphase | 2015 – 2021 | 9,14 % |
| Korrektur | 2022 – 2024 | −2,92 % |

Die Korrektur konzentriert sich fast vollständig auf ein einziges Jahr: 2023 mit −12,27 %. 2024 verläuft mit −0,76 % nahezu stabil. Der direkte Vergleich mit der Finanzkrise (stärkster Jahresrückgang −1,28 % in 2007) macht die Schärfe der Zinswende deutlich — der Rückgang 2023 ist fast das Zehnfache.

### H2 — Die Schere zwischen den Städten hat sich real vergrößert

Die relative Streuung (Variationskoeffizient) der Preise über alle Städte stieg von 25,49 % (2005) auf einen Höhepunkt von 41,61 % (2017) und pendelt seither um 40 %. Der Anstieg geht über das reine Preiswachstum hinaus, die Preisschere ist also real gewachsen.

Die Spannweite der Preisentwicklung zwischen 2005 und 2024 liegt bei über 200 Prozentpunkten: München (+201,75 %), Hamburg (+176,19 %) und Lübeck (+150,00 %) an der Spitze, Chemnitz (−3,28 %) als einzige Stadt mit einem tatsächlichen Preisrückgang über den gesamten Zeitraum.

### H3 — Wohnungen führen das Feld an, Mehrfamilienhäuser sind investorengetrieben

Prozentuale Preissteigerung 2005 bis 2024 nach Immobilientyp:

| Immobilientyp | Preis 2005 | Preis 2024 | Veränderung |
| --- | --- | --- | --- |
| apartment | 1.675 € | ~3.900 € | +132,76 % |
| single_family | 1.954 € | ~3.850 € | +97,23 % |
| multi_family | 1.258 € | ~2.462 € | +95,70 % |

Ein Zusatzbefund vertieft H3: Mehrfamilienhäuser weisen eine deutlich höhere Volatilität der jährlichen Wachstumsrate auf (Standardabweichung 7,88) als apartment (5,48) und single_family (5,65). Dieses Verhalten passt zu einem investorengetriebenen Marktsegment — sowohl der stärkste Einzeljahresanstieg (+13,71 % in 2015) als auch der stärkste Einbruch aller drei Typen (−18,49 % in 2023) tritt bei multi_family auf.

### Bonus — Erschwinglichkeit

Die durchschnittliche Erschwinglichkeit (Anteil der Hypothekenkosten am Einkommen) verschlechterte sich von 21,69 % (2005) auf 31,15 % (2022). Auch nach dem Preisrückgang ab 2023 bleibt sie mit 27,08 % (2024) deutlich schlechter als vor der Boomphase — die Zinswende verteuert Finanzierung direkt und hebt fallende Kaufpreise teilweise auf.

Frankfurt am Main ist im Städtevergleich am schlechtesten erschwinglich (36,61 %), noch vor München (33,95 %). Bei der reinen Preissteigerung lag Frankfurt nur auf Platz 4 — das zeigt, dass ein hohes Ausgangspreisniveau ebenso stark wirkt wie ein starker Preisanstieg.

## Methodische Highlights

- **Hypothesen vorab formuliert.** H1 bis H3 stehen zu Beginn des Notebooks fest, bevor die Auswertung startet. Ergebnisse werden explizit gegen die Hypothese gespiegelt (bestätigt, präzisiert, widerlegt).
- **Robustheitscheck der Phaseneinteilung.** Die zunächst anhand des Liniendiagramms geschätzten Phasen wurden gegen die jährlichen Wachstumsraten geprüft und überarbeitet. Der Bericht dokumentiert beide Fassungen und begründet die Änderung.
- **Trendbereinigte Saisonprüfung.** Vor der Umstellung auf Jahreswerte wurde geprüft, ob ein echtes Saisonmuster verloren geht. Ergebnis: rund 4 Prozentpunkte Spannweite zwischen Q1 und Q4, dokumentiert als bekannte Nebenschwankung.
- **Fehlerhafte Spalten transparent behandelt.** Widersprüchliche Werte werden nicht heimlich gemittelt, sondern die betroffenen Spalten aus der Hauptanalyse ausgeschlossen. Der Bonusteil zur Erschwinglichkeit dokumentiert seine Bereinigungslogik explizit.
- **Städte-Abdeckung offen ausgewiesen.** Wo Daten fehlen (Leipzig ab 2014, Rhein-Erft-Kreis ab 2010), wird der Vergleich nicht auf 21 Städte hochgerechnet, sondern die Einschränkung im Bericht benannt.

## Grenzen

- **Nur 21 Städte.** Der Datensatz deckt eine Auswahl größerer Städte ab, nicht die Fläche. Aussagen über „den deutschen Immobilienmarkt" gelten für dieses Städtepanel, nicht für ländliche Räume.
- **Aggregierte Preise.** Innerhalb einer Stadt kann die Spreizung nach Lage, Baualter und Zustand erheblich sein. Der Datensatz bildet Stadt-Mittelwerte je Quartal ab.
- **Erschwinglichkeit rekonstruiert.** Die im Bonusteil verwendete Erschwinglichkeitskennzahl wurde aus widersprüchlichen Rohwerten durch Mittelwertbildung rekonstruiert — eine bewusste Vereinfachung, keine Fehlerkorrektur.
- **Kausalitäten interpretiert, nicht getestet.** Zusammenhänge mit Zinswende, Finanzkrise und Anlageverhalten werden im Bericht plausibel eingeordnet, aber nicht mit ökonometrischen Verfahren nachgewiesen.

## Nutzung

```bash
# Abhängigkeiten installieren
pip install -r requirements.txt

# Notebook öffnen
jupyter notebook Abschlussprojekt.ipynb
```

Der Datensatz `city_master_dataset.csv` liegt neben dem Notebook. Alle Zellen sind so ausgelegt, dass sie in der vorgegebenen Reihenfolge komplett durchlaufen — jede Kennzahl wird dort berechnet, wo sie inhaltlich hingehört, und nicht auf frühere Zwischenschritte referenziert.

## Repository-Inhalt

| Datei | Beschreibung |
| --- | --- |
| `Abschlussprojekt.ipynb` | Jupyter Notebook mit Analyse, Kommentaren und Visualisierungen |
| `city_master_dataset.csv` | Rohdaten (Kaggle-Datensatz, siehe Datengrundlage) |
| `abschlussprojekt_python.pdf` | Aufgabenstellung des Abschlussprojekts |
| `Der-deutsche-Immobilienmarkt-2005-bis-2024.pptx` | Präsentation der Ergebnisse |
| `requirements.txt` | Python-Abhängigkeiten |

## Technischer Stack

Python (pandas, plotly) · Jupyter Notebook · Git

## Kontext

Dieses Projekt ist das Abschlussprojekt des Python-Moduls meiner IHK-Weiterbildung zum Data Analyst bei DataSmart Point (2026). Nach zehn Jahren im Immobilienvertrieb verbinde ich hier Branchenkenntnis mit dem vollständigen Workflow eines Data Analysts — von der Datensichtung über hypothesengetriebene Analyse bis zur belastbaren Ergebniszusammenfassung.

Roman Rosenberger · September 2026

Datensatz-Quelle: Meena Aditya, „German City-Level Housing Market Dataset", Kaggle. Ursprungsdaten aus GREIX (Kiel-Institut für Weltwirtschaft).
