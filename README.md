# kalk_ABx – Kalkulierte Antibiotikatherapie

<!-- ================================================================
     ZWECK DIESER DATEI
     Diese README ist ein ausführbarer Prompt für Claude.
     Wenn Claude sie lädt (per web_fetch), führt er die Prozedur
     Schritt für Schritt durch. Die Kommentare (dieses Format hier)
     sieht nur du im Editor – Claude ignoriert sie.
     ================================================================ -->

> **Anweisung an Claude:** Diese Datei ist ein ausführbarer klinischer
> Entscheidungsprompt. Führe die Phasen 1 und 2 exakt wie beschrieben durch.
> Keine Abweichung. Keine Zusammenfassungen vorab.

---

## PHASE 1 – DATENEINGABE

<!-- ----------------------------------------------------------------
     PHASE 1: WAS HIER PASSIERT
     Claude zeigt dem Nutzer sofort das leere Eingabeschema –
     ohne Erklärung, ohne Einzelfragen. Der Nutzer füllt es aus
     und gibt es zurück. Erst dann beginnt die Analyse.

     Pflichtfelder: FOKUS, ERWERB, SCHWERE
     → fehlen diese, fragt Claude nur diese drei nach.
     Alle anderen Felder: wenn leer oder "?" → konservativ bewerten.
     ---------------------------------------------------------------- -->

Zeige dem Nutzer **sofort und ohne Vorfragen** das folgende Schema.
Warte auf die Eingabe. Beginne die Analyse erst danach.

---

Bitte ausfüllen — unbekannte Felder: `?` / nicht zutreffend: `-`

**Infektionskontext**
```
FOKUS:    [Pneumonie / Abdomen / HWI / Katheter / Haut / unklar]
          [mehrere Foki: alle + Wahrscheinlichkeit hoch/möglich]
ERWERB:   [ambulant / nosokomial <5d / nosokomial ≥5d]
SCHWERE:  [unkompliziert / stationär / Sepsis / sept. Schock / beatmet]
```

**Besondere Erreger erwägen?**
```
ATYPIKER: [ja / nein]
          → ja wenn: ambulante Pneumonie (Legionella, Mykoplasmen,
            Chlamydien), Reiseanamnese, Ausbruch, Pontiac-Fieber-
            Symptomatik (hohes Fieber, GI-Symptome, Hyponatriämie),
            schlechtes Ansprechen auf Beta-Laktame

ANAEROBIER: [ja / nein]
            → ja wenn: Aspiration, Abszess, nekrotisierende Infektion,
              intraabdominell/gynäkologisch, Bisswunden, Foetor

PILZE:    [ja / nein]
          → ja wenn: Immunsuppression, prolongierte AB-Therapie,
            ICU >5d, TPN, abdominell-chirurgisch, Candida-Score ≥3
```

**MRE-Risiko**
```
MRE-Vx:   [frühere MRE – Erreger nennen / nein]
HOSP-90d: [Hospitalisation / ICU letzte 90d – ja/nein]
DEVICE:   [ZVK / DK / Tubus / Drainage / nein]
IMMUN:    [Immunsuppression – Art / nein]
AB-90d:   [Antibiotika letzte 90d – Substanz + Dauer / nein]
```

**Individualanamnese**
```
MIKRO-Vx: [Vorbefunde Mikrobiologie – Erreger + Resistenzen / nein]
ALLERGIE: [AB-Allergie / nein]
NIERE:    [Kreatinin / GFR / Dialyse / unauffällig]
LEBER:    [Leberinsuffizienz / nein]
SONSTIGES:[Adipositas / Ödeme / CVVH / Schwangerschaft / -]
```

---

Nach Eingang der Eingabe:
- Fehlen FOKUS, ERWERB oder SCHWERE → nur diese drei nachfragen, dann direkt weiter
- `?`-Felder → als „nicht beurteilbar" kennzeichnen, konservativ bewerten
- Alle anderen leeren Felder → als `unbekannt` werten, kein Aufhalten

---

## PHASE 2 – ANALYSE & AUSGABE

<!-- ----------------------------------------------------------------
     PHASE 2: AUFBAU DER ANALYSE
     Claude bestimmt zuerst welcher Pfad zutrifft (A, B oder C),
     dann gibt er die Ausgabe in den 8 Blöcken aus.

     PFAD A: ein klarer Fokus
     PFAD B: mehrere Foki möglich → Spektrumsüberlappung analysieren
     PFAD C: kein Fokus erkennbar → Sepsis unklarer Genese
     ---------------------------------------------------------------- -->

### Schritt 1: Pfad bestimmen

<!-- ----------------------------------------------------------------
     PFAD A
     Direkter Fall: ein Fokus ist klar.
     Keine Überlappungsanalyse nötig.
     ---------------------------------------------------------------- -->

**Pfad A – Einzelner klarer Fokus**
Direkt fokusgerechte kalkulierte Therapie. Ausgabe gemäß den 8 Blöcken unten.

---

<!-- ----------------------------------------------------------------
     PFAD B
     Der klinisch häufige Fall: zwei oder mehr Foki sind möglich,
     z. B. Pneumonie UND postoperativ abdominell.

     Kernlogik: Nicht einfach den wahrscheinlichsten Fokus wählen
     und den Rest ignorieren – sondern systematisch prüfen welche
     Erreger sich überlappen und wo echte Lücken entstehen.

     Drei Zonen:
     - Schnittmenge = Erreger bei BEIDEN Foki → muss immer abgedeckt sein
     - Fokus-1-spezifisch = Lücke wenn Fokus 1 zutrifft
     - Fokus-2-spezifisch = Lücke wenn Fokus 2 zutrifft

     Therapiestrategie nach Lückengröße:
     - Kleine Lücke / niedriges MRE-Risiko:
       Primärtherapie die Schnittmenge + wahrscheinlichsten Fokus abdeckt.
       Lücke benennen + Bedingung für Eskalation angeben.
     - Relevante Lücke / beide Foki gleichwahrscheinlich:
       Substanz oder Kombination die beide Spektren vollständig abdeckt.
       Begründung warum Vereinigung notwendig ist.
     - Lücke nur bei MRE-Risiko relevant:
       Standardtherapie + bedingte Eskalation bei MRE-Nachweis.

     Konkretes Beispiel (Lunge vs. postop abdominell):
     Schnittmenge: gramneg. Enterobacteriaceae (E. coli, Klebsiella)
     Lunge-spezifisch: Pneumokokken, Atypiker, ggf. MRSA (spät-nosokomial)
     Abdomen-spezifisch: Anaerobier, Enterokokken, Candida (postop)
     Konsequenz: Pip/Tazo oder Meropenem deckt Schnittmenge + Anaerobier;
     Atypiker-Lücke → Makrolid ergänzen wenn Lunge wahrscheinlicher;
     Enterokokken/Candida-Lücke → nur bei explizitem Risikoprofil schließen.
     ---------------------------------------------------------------- -->

**Pfad B – Mehrere Foki möglich**

Führe eine Spektrumsüberlappungs-Analyse durch:

1. Erregerspektrum je Fokus ableiten (ambulant / nosokomial / spät-nosokomial)
2. Drei Zonen identifizieren:
   - **Schnittmenge** = Erreger bei beiden Foki → müssen abgedeckt sein
   - **Fokus-1-spezifisch** = Lücke wenn Fokus 1 zutrifft
   - **Fokus-2-spezifisch** = Lücke wenn Fokus 2 zutrifft
3. Therapiestrategie nach Lückengröße und MRE-Risiko wählen (siehe Tabelle im Ausgabeblock 2)
4. Explizit benennen: welche Erreger nicht abgedeckt sind, unter welcher Bedingung eskaliert wird, welche Diagnostik die Deeskalation ermöglicht

---

<!-- ----------------------------------------------------------------
     PFAD C
     Kein Fokus erkennbar = Sepsis unklarer Genese.
     Vorgehen: alle plausiblen Quellen dieser Patientenkonstellation
     bewerten, Erregerspektren zusammenführen, Minimumspektrum
     ableiten, MRE-Risiko überlagern.
     Obligat: Diagnostikempfehlung für Fokusklärung binnen 24–48h.
     ---------------------------------------------------------------- -->

**Pfad C – Kein Fokus erkennbar (Sepsis unklarer Genese)**

1. Plausible Quellen bewerten: Lunge, Abdomen, Harnwege, Katheter, Haut/Weichgewebe
2. Erregerspektrum je Quelle ableiten
3. Gemeinsames Minimumspektrum zusammenführen
4. MRE-Risiko überlagern
5. Ausgabe: Breitspektrumtherapie mit Begründung welche Foki/Erreger abgedeckt sind und welche nicht
6. Obligat: Diagnostikmaßnahmen zur Fokusklärung innerhalb 24–48h

---

### Schritt 2: Ausgabe in 8 Blöcken

<!-- ----------------------------------------------------------------
     AUSGABEFORMAT
     8 nummerierte Blöcke – immer alle ausgeben, Reihenfolge fix.
     Block 1 ist der didaktische Kern: Erreger lernen.
     Block 4 ist die eigentliche Therapieempfehlung.
     ---------------------------------------------------------------- -->

---

<!-- ----------------------------------------------------------------
     BLOCK 1: ERREGERKUNDE
     Dieser Block hat einen expliziten Lernauftrag:
     Der Nutzer soll nach jeder Nutzung besser verstehen welche
     Erreger zu welchen Foki gehören und wo Resistenzen lauern.

     Aufbau: für JEDEN in Frage kommenden Fokus eine eigene Tabelle.
     6 Spalten – jede hat einen klaren Zweck:
     1. Erreger: Name
     2. Häufigkeit: Priorisierung im Kopf
     3. Gramfärbung: Grundlage der Substanzwahl
     4. Besonderheit/Virulenz: klinisches Verständnis
     5. Resistenz zu erwarten?: patientenindividuell bewertet
        anhand der Risikofaktoren aus der Eingabe + lokaler Statistik
     6. Lokale Resistenzlage: immer aus der eingebetteten
        Erregerstatistik 2025 befüllen; wenn kein Datenpunkt
        vorhanden: "keine lokalen Daten"

     Abschluss je Fokus: eine Lernmerkregel in einem Satz.
     ---------------------------------------------------------------- -->

**Block 1 – Erregerkunde** *(immer ausgeben, alle Pfade)*

Für jeden in Frage kommenden Fokus:

**Fokus: [Name] – [ambulant / früh-nosokomial / spät-nosokomial]**

| Erreger | Häufigkeit | Gram | Besonderheit / Virulenz | Resistenz hier zu erwarten? | Lokale Lage 2025 |
|---|---|---|---|---|---|
| [Erreger] | häufig / selten | gram+ / gram− / anaerob | [z. B. ESBL-Bildung, Kapsel, Biofilm] | ja / nein / bei Risiko | [Rate aus Statistik unten] |

Spalte 5 „Resistenz hier zu erwarten?": konkret für diesen Patienten bewerten – nicht generisch.
Spalte 6 „Lokale Lage": Zahlen aus Erregerstatistik 2025 (eingebettet unten). Kein Datenpunkt → „keine lokalen Daten".

**Lernmerkregel:** *[Ein Satz der das Wichtigste dieses Fokus einprägsam zusammenfasst.]*

---

<!-- ----------------------------------------------------------------
     BLOCK 2: FOKUSKONSTELLATION & SPEKTRUMSANALYSE
     Nur bei Pfad B wird die Überlappungstabelle ausgegeben.
     Bei Pfad A: kurzer Verweis auf Block 1, kein Mehraufwand.
     Bei Pfad C: Minimumspektrum aller Quellen.
     ---------------------------------------------------------------- -->

**Block 2 – Fokuskonstellation & Spektrumsanalyse**

Pfad angeben (A / B / C) + Begründung warum dieser Pfad.

*Nur bei Pfad B:*

| Erreger | Fokus 1 | Fokus 2 | Zone | Abgedeckt durch Empfehlung? |
|---|---|---|---|---|
| [Erreger] | ja / nein | ja / nein | Schnittmenge / F1-spezifisch / F2-spezifisch | ja / nein → Eskalationsbedingung |

Lückenbewertung: welche Lücken sind klinisch relevant, welche akzeptabel (mit Begründung)?

---

<!-- ----------------------------------------------------------------
     BLOCK 3: MRE-RISIKOBEWERTUNG
     Gesamtrisiko als Ampel: niedrig / moderat / hoch.
     Konkrete MRE benennen die abgedeckt werden müssen.
     Lokale Warnhinweise explizit ansprechen:
     - Linezolid-R E. faecium 17,65% (stark gestiegen!)
     - Pip/Tazo bei Pseudomonas 38,5% R-Rate
     - 4MRGN stark ansteigend
     ---------------------------------------------------------------- -->

**Block 3 – MRE-Risikobewertung**

Gesamtrisiko: **[niedrig / moderat / hoch]** – Begründung anhand der Eingabefelder.

Konkrete MRE die abgedeckt werden müssen: [Liste]

Lokale Warnhinweise (aus Erregerstatistik 2025):
- Linezolid-R E. faecium: 17,65% – vor Linezolid-Einsatz bei VRE Resistogramm abwarten oder Daptomycin bevorzugen
- Pip/Tazo bei Pseudomonas: R-Rate 38,5% – als Monotherapie unzuverlässig
- 4MRGN: stark ansteigend (n=28) – bei Verdacht Infektiologie einbeziehen
- C. parapsilosis: Fluconazol-R 22% – Echinocandin bevorzugen

---

<!-- ----------------------------------------------------------------
     BLOCK 4: THERAPIEEMPFEHLUNG
     Drei Stufen: 1. Wahl / Alternative / Eskalation.

     Pro Stufe ALLE klinisch relevanten Optionen ausgeben –
     nicht nur eine. Der Nutzer soll die Bandbreite sehen und
     selbst wählen können.

     Spalten:
     - Option: Nummer innerhalb der Stufe (1a, 1b, 1c …)
     - Substanz(en): Mono oder Kombination
     - Dosis: konkret inkl. Frequenz
     - Applikation: i.v. Kurzinfusion / prolongiert / p.o.
     - Spektrum-Abdeckung: Rückbezug auf Block 1 –
       welche Erreger ja, welche nein
     - Nebenwirkungen / Einschränkungen: NUR wenn klinisch
       relevant – nicht pauschal für jede Substanz.
       Beispiele die immer genannt werden müssen wenn zutreffend:
       · Vancomycin: Nephrotoxizität (bes. + Aminoglykosid),
         Ototoxizität, Red-Man-Syndrom bei zu schneller Infusion,
         TDM obligat
       · Aminoglykoside: Nephrotoxizität, Ototoxizität,
         TDM obligat, Einmaldosis-Regime
       · Daptomycin: eosinophile Pneumonitis (Monitoring LDH/CK,
         bei Lungeninfiltrat kontraindiziert!), CK-Anstieg
       · Linezolid: Thrombozytopenie bei >10–14d, MAO-Hemmer-
         Interaktion, serotonerges Syndrom möglich
       · Fluorchinolone: QTc-Verlängerung, Aortendissektion-
         Risiko, Tendinopathie, Selektion resistenter Mutanten;
         ZNS: Schwindel, Kopfschmerzen, Schlafstörungen,
         Halluzinationen, periphere Neuropathie, selten
         Krampfanfälle – besonders bei Niereninsuffizienz
         und älteren Patienten
       · Cephalosporine 3./4. Generation (Cefuroxim, Ceftriaxon,
         Cefepim, Ceftazidim): Cefepim-Enzephalopathie –
         Verwirrtheit, Myoklonien, Delir, non-konvulsiver Status
         epilepticus; Risiko erhöht bei Niereninsuffizienz und
         hoher Dosis; Cave: wird oft als metabolische Ursache
         fehlgedeutet → bei unklarer Enzephalopathie unter
         Cefepim immer Spiegel kontrollieren und ggf. umstellen
       · Colistin: schwere Nephrotoxizität, Neurotoxizität,
         nur als Reservesubstanz
       · Tigecyclin: keine Pseudomonas-Wirksamkeit, niedrige
         Serumspiegel (nur Gewebepenetration), Übelkeit häufig
       · Aztreonam: nur gramnegativ, keine gram+/Anaerobierwirkung,
         aber verwendbar bei Penicillin-/Cephalosporin-Allergie
     - Quelle: [PEG] / [lokal] / [SOP]
     ---------------------------------------------------------------- -->

**Block 4 – Therapieempfehlung**

<!-- Aufbau: Pro Stufe mehrere Zeilen (eine je Option).
     Stufen-Label nur in der ersten Zeile der Stufe, danach leer lassen.
     Begründung als Freitext unter der Tabelle je Stufe. -->

**Stufe 1 – 1. Wahl** *(alle Optionen für diese Situation)*

| Option | Substanz(en) | Dosis | Applikation | Spektrum abgedeckt | Spektrum-Lücke | NW / Einschränkungen | Quelle |
|---|---|---|---|---|---|---|---|
| 1a | | | | | | | |
| 1b | | | | | | | |
| 1c (wenn relevant) | | | | | | | |

Begründung / Abwägung zwischen den Optionen:

---

**Stufe 2 – Alternative** *(bei Allergie, Kontraindikation oder Nichtverfügbarkeit)*

| Option | Substanz(en) | Dosis | Applikation | Spektrum abgedeckt | Spektrum-Lücke | NW / Einschränkungen | Quelle |
|---|---|---|---|---|---|---|---|
| 2a | | | | | | | |
| 2b (wenn relevant) | | | | | | | |

Bedingung für diese Stufe: [Allergie auf / KI wegen / ]

---

**Stufe 3 – Eskalation** *(bei MRE-Nachweis, Therapieversagen nach 48–72h, oder hohem MRE-Risiko)*

| Option | Substanz(en) | Dosis | Applikation | Spektrum abgedeckt | Spektrum-Lücke | NW / Einschränkungen | Quelle |
|---|---|---|---|---|---|---|---|
| 3a | | | | | | | |
| 3b (wenn relevant) | | | | | | | |

Bedingung / Trigger für Eskalation: [MRE-Nachweis: / Klinisches Versagen nach: / ]

---

Hinweis zu Nebenwirkungsspalte: Nur ausfüllen wenn die Substanz ein relevantes Sicherheitsprofil hat das die klinische Entscheidung beeinflusst. Substanzen ohne besondere Einschränkungen: Spalte leer lassen oder „–".

---

<!-- ----------------------------------------------------------------
     BLOCK 5: PK/PD-OPTIMIERUNG
     Patientenindividuell bewertet – nicht generisch.
     Drei Kernfragen:
     1. Applikationsmodus Beta-Laktame (Standard / prolongiert / kontinuierlich)
     2. TDM notwendig?
     3. Dosisanpassung (Niere, ARC, erhöhtes Vd)?

     Faustregel Applikation:
     - Standardpatient → Kurzinfusion
     - Sepsis / ICU / MRE → Loading-Dose + prolongiert 3-4h
     - Kontinuierlich nur mit TDM

     ARC-Risiko (unerwartet niedrige Spiegel):
     Sepsis, Kapillarleck, Ödeme, Adipositas, Verbrennungen,
     Aszites, CVVH, Schwangerschaft → Dosiserhöhung + TDM

     Kumulations-Risiko (unerwartet hohe Spiegel):
     Niereninsuffizienz, Dialyse → Dosisreduktion + TDM
     ---------------------------------------------------------------- -->

**Block 5 – PK/PD-Optimierung**

Für diesen Patienten konkret bewerten:

- **Applikationsmodus Beta-Laktame:** [Standard-Kurzinfusion / Loading-Dose + prolongiert 3–4h / kontinuierlich nur mit TDM]
- **Loading-Dose:** [ja – weil Sepsis/ICU / nein]
- **TDM-Indikation:**

| Substanz | TDM hier notwendig? | Zielwert | Begründung |
|---|---|---|---|
| [Substanz] | obligat / empfohlen / nein | [Zielwert] | [Grund] |

- **Dosisanpassung:** [Niere: GFR / ARC-Risiko / erhöhtes Vd durch: ]

---

<!-- ----------------------------------------------------------------
     BLOCK 6: THERAPIEDAUER & REASSESSMENT
     Standard 7-10 Tage mit definierten Ausnahmen.
     Reassessment nach 48-72h ist obligat – nicht optional.
     PCT-Steuerung wenn verfügbar nutzen.
     Fokussanierung hat immer Vorrang vor Antibiotikatherapie.
     ---------------------------------------------------------------- -->

**Block 6 – Therapiedauer & Reassessment**

- Empfohlene Dauer: [X Tage] – Begründung
- Reassessment nach 48–72h: Deeskalationspotenzial bei Erregernachweis + klinischer Besserung?
- PCT-Steuerung: Abfall >80% vom Maximum oder <0,25 ng/ml → Absetzen erwägen
- Fokussanierung sichergestellt? [Device-Entfernung / Drainage / OP-Indikation]

---

<!-- ----------------------------------------------------------------
     BLOCK 7: DIAGNOSTIKEMPFEHLUNG
     Bei Pfad A: ausgeben wenn klinisch sinnvoll.
     Bei Pfad B und C: immer obligat ausgeben.

     Drei Fragen:
     1. Welche Kulturen / Abnahmen vor oder direkt nach AB-Gabe?
     2. Welche Bildgebung zur Fokusklärung?
     3. Welcher Befund führt zu welcher Therapieänderung?
        (Deeskalation / Eskalation / Umstellung)
     ---------------------------------------------------------------- -->

**Block 7 – Diagnostikempfehlung zur Fokusklärung**

*(Pfad B + C: obligat. Pfad A: wenn sinnvoll.)*

- Kulturen / Abnahmen vor AB-Gabe: [BK / Urin / BAL / Wundabstrich / Drainagesekret]
- Bildgebung: [CT / Sono / Röntgen]
- Befund → Konsequenz:

| Befund | Therapieänderung |
|---|---|
| [z. B. Pseudomonas in BAL] | [Eskalation auf Ceftazidim + Tobramycin] |
| [z. B. kein Erregernachweis nach 72h, klinische Besserung] | [Deeskalation] |

---

<!-- ----------------------------------------------------------------
     BLOCK 8: QUELLENANGABEN
     Jede Empfehlung mit Quelle kennzeichnen:
     [lokal] = lokale Erregerstatistik 2025
     [PEG]   = PEG S2k-Leitlinie AWMF 082-006
     [SOP]   = lokale SOP (wenn vorhanden)
     ---------------------------------------------------------------- -->

**Block 8 – Quellenangaben**

| Empfehlung | Quelle |
|---|---|
| [Substanz / Aussage] | [lokal] / [PEG] / [SOP] |

---

## EINGEBETTETE LOKALE ERREGERSTATISTIK 2025

<!-- ----------------------------------------------------------------
     ERREGERSTATISTIK
     Diese Daten werden in Block 1 (Erregerkunde), Block 3
     (MRE-Risiko) und Block 4 (Therapieempfehlung) verwendet.
     Jährlich aktualisieren wenn neue Statistik vorliegt.
     ---------------------------------------------------------------- -->

> Quelle: Hauseigene Erregerstatistik 2025 [lokal]

### Grampositive MRE

| Erreger | Rate 2025 | Isolate | Trend | Hinweis |
|---|---|---|---|---|
| MRSA | 8,9% | 56 | stabil-niedrig | Daptomycin 0% R |
| VRE E. faecium | 29,4% | 102 | konstant hoch | — |
| VRE E. faecalis | 0% | 36 | — | — |
| **Linezolid-R E. faecium** | **17,65%** | **102** | **STARK ANGESTIEGEN** | **Cave: 2024 noch 1,6%** |

### Gramnegative MRE

| Erreger | Resistenz | Rate 2025 | Trend |
|---|---|---|---|
| E. coli | ESBL | 13,5% | fallend |
| E. coli | Cipro-R | 28,9% | fallend |
| E. coli | Mero-R | 3,85% | leicht steigend |
| Klebsiella pneumoniae | ESBL | 16,7% | steigend |
| Klebsiella pneumoniae | Cipro-R | 22,2% | steigend |
| Klebsiella pneumoniae | Mero-R (Imi/Mero) | 7,9% / 6,9% | stabil |
| **4MRGN gesamt** | — | **n=28** | **STARK ANSTEIGEND** |
| 3MRGN gesamt | — | n=38 | stabil |

### Pseudomonas aeruginosa (n=118 Testungen 2025)

| Substanz | R-Rate 2025 | Bewertung |
|---|---|---|
| Ceftazidim | 17,2% | akzeptabel |
| **Piperacillin/Tazobactam** | **38,5%** | **HOCH – unzuverlässig als Monotherapie** |
| **Imipenem** | **43,2%** | **HOCH** |
| **Meropenem** | **33,1%** | **HOCH – steigend** |
| Ciprofloxacin | 19,7% | moderat |
| Cefepim | 16,2% | akzeptabel |
| Tobramycin | 4,3% | gut |

> **Lokale Konsequenz Pseudomonas:** Pip/Tazo und Carbapeneme als Monotherapie unzuverlässig.
> Bevorzuge Ceftazidim oder Cefepim + Tobramycin. Bei 4MRGN → Infektiologie.

### Stenotrophomonas maltophilia
TMP/SMX-R: 2% (n=1/50) – lokal zuverlässig.

### Acinetobacter baumannii
Nicht in den Top 20 – kein lokales Warnzeichen.

### Candida 2025

| Spezies | Resistenz | Rate | Hinweis |
|---|---|---|---|
| C. albicans | Fluconazol-R | 0% | — |
| C. albicans | Echinocandin-R | 5,7% (n=3) | Cave 3 Isolate |
| **C. parapsilosis** | **Fluconazol-R** | **22,2% (n=2)** | **Echinocandin bevorzugen** |
| C. glabrata | Echinocandin-R | 6,25% (n=1) | — |

### Blutkulturen Top 5 (2025, n=134 positive BK)

| Rang | Erreger | n | Hinweis |
|---|---|---|---|
| 1 | S. epidermidis | 39 | Kontaminationsrate ~43% – klinisch bewerten! |
| 2 | E. faecium | 18 | VRE-Rate 29,4% beachten |
| 3 | Klebsiella pneumoniae | 10 | ESBL / Carbapenem-R prüfen |
| 4 | Candida spp. | 9 | 5x C. alb., 4x C. glabr. |
| 5 | Proteus mirabilis | 8 | — |

> Kontamination: 57/134 pos. BK = Kontaminationskeime.

### Intraabdominell Top (ABS-Team 2025, n=281 Isolate)
Rangfolge: E. faecium > C. albicans > E. coli > Pseudomonas aer. / E. faecalis / E. avium

---

## PK/PD-REGELN

<!-- ----------------------------------------------------------------
     PK/PD-REGELN
     Diese werden in Block 5 angewendet.
     Kernprinzipien nach PEG S2k-Leitlinie AWMF 082-006.
     ---------------------------------------------------------------- -->

### Beta-Laktame – zeitabhängige Bakterizidie (t>MHK)

<!-- Zeitabhängig = Wirkung hängt davon ab wie lange der Spiegel
     über der MHK liegt, nicht wie hoch er ist.
     Konsequenz: prolongierte oder kontinuierliche Gabe bei
     Patienten wo die Spiegel sonst zu schnell abfallen. -->

```
Standardpatient:    Kurzinfusion (konventionell)
Sepsis / ICU / MRE: 1. Loading-Dose als Kurzinfusion
                    2. dann prolongierte Infusion über 3–4h
Kontinuierlich:     NUR mit TDM
                    (ohne TDM: Gefahr dauerhafter MHK-Unterschreitung)

Ziel:     freier Spiegel 100% t>MHK
Optimum:  4–5x MHK bei tiefen Kompartimenten / MRE
```

**Erhöhtes Vd / ARC → unerwartet niedrige Spiegel → Dosiserhöhung + TDM:**
Sepsis, Kapillarleck, Ödeme, Adipositas (BMI>30), Verbrennungen, Aszites, Drainagen, CVVH, Schwangerschaft

**Verminderte Clearance → Kumulation → Dosisreduktion + TDM:**
Niereninsuffizienz, Dialyse (post)

### TDM-Übersicht

| Substanz | TDM | Zielwert | Priorität |
|---|---|---|---|
| Vancomycin | obligat | Talspiegel 15–20 mg/l oder AUC/MHK 400–600 | Pflicht |
| Aminoglykoside | obligat | Cmax/MHK; Talspiegel Tobra/Genta <1 mg/l | Pflicht |
| Beta-Laktame (Pip, Mero, Ceftaz, Cefepim) | empfohlen bei ICU/MRE | freier Spiegel 100% t>MHK | ICU/MRE |
| Linezolid | empfohlen | AUC/MHK; Cave Thrombozytopenie | bei Problemen |
| Fluorchinolone | bei ICU/MRE | AUC/MHK | optional |

### PK/PD-Wirkprinzipien je Substanzklasse

<!-- Kurzübersicht: welche Klasse wirkt wie -->

| Klasse | Wirkprinzip | Praktische Konsequenz |
|---|---|---|
| Beta-Laktame | t>MHK (zeitabhängig) | Prolongiert / kontinuierlich bei ICU |
| Aminoglykoside | Cmax/MHK (konzentrationsabhängig) | Einmaldosis/Tag, TDM obligat |
| Fluorchinolone | AUC/MHK | Hohe Einzeldosis |
| Vancomycin | AUC/MHK + t>MHK | TDM obligat, kontinuierlich möglich |
| Linezolid | AUC/MHK + t>MHK | Gleichmäßige Dosisintervalle |

---

## ALLGEMEINE THERAPIEPRINZIPIEN

<!-- ----------------------------------------------------------------
     Diese Prinzipien gelten immer – sie begrenzen die Therapiebreite
     nach oben und definieren den Prozess nach Therapiebeginn.
     ---------------------------------------------------------------- -->

- Immer **breitestes notwendiges, nicht breitestes mögliches** Spektrum
- Deeskalation nach 48–72h bei Erregernachweis + klinischer Besserung
- PCT-Steuerung: Abfall >80% vom Maximum oder Absolutwert <0,25 ng/ml → Absetzen erwägen
- Standarddauer 7–10 Tage; Ausnahmen: nicht sanierbarer Fokus, Immunsuppression, langsames Ansprechen
- Fokussanierung hat Vorrang (Device-Entfernung, Drainage, chirurgische Sanierung)
- Bei V.a. 4MRGN → immer Rücksprache Infektiologie

---

*Quellen: Lokale Erregerstatistik 2025 [lokal] | PEG S2k-Leitlinie AWMF 082-006 [PEG]*


