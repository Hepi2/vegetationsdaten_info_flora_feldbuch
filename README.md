# Vegetationsaufnahmen aus Info Flora Online-Feldbuch von exportieren in R oder VEGEDAZ importieren


<a name="inhalt"></a>
### Inhalt
- [1. Exportieren von Vegetationsaufnahmen aus dem Online-Feldbuch von Info Flora](#export)
- [2. Vegetationsdaten vom Info Flora Online-Feldbuch mit R transformieren](#Rtransformieren)
- [3. Vegetationsdaten vom Info Flora Online-Feldbuch mit VEGEDAZ transformieren](#VEGEDAZtransformieren)
<br />

<a name="export"></a>
## 1. Exportieren aus Online-Feldbuch

1. Login im [Info Flora Online-Feldbuch](https://auth.infoflora.ch/de/login).

2. Auf «Beobachtungen» klicken.
   
3. Im Drop-Down Menü von Maske: «Vegetationsaufnahmen» wählen.
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/c1c31b31-7b5a-4050-95c8-7f5cc708dba9)
   
   <br />

5. Mit gedrückter Ctrl- oder Shift-Taste Vegetationsaufnahmen, die exportiert werden sollen, markieren.

6. Auf «Export Aufnahmen» klicken -> Neues Fenster erscheint.
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/66779fcc-d582-425f-a94e-e7caab2e9ce3)
   
   <br />
   
8. «Export der Vegetationsaufnahmen» anklicken, um die Kopfdaten zu speichern. «Export der Beobachtungen» anklicken, um die Artdaten zu speichern. <br />
   (Hinweis: Die Artdaten der Vegetationsaufnahmen können auch über die Maske «Standard» heruntergeladen werden. Vorteil: Die Beschränkung auf 50 Aufnahmen entfällt. Nachteil: Die Selektion der zu den gewünschten Aufnahmen gehörenden Artdaten mit der Filter-Funktion ist etwas umständlich.)
   

10. Mit EXCEL die exportierten Dateien öffnen, als «CSV UTF-8 (durch Trennzeichen-getrennt) (*.csv)» speichern und wieder schliessen. Nun sind die Daten parat zur weiteren Bearbeitung mit R oder VEGEDAZ.
<br />


<a name="Rtransformieren"></a>
## 2. Vegetationsaufnahmen in R importieren
Vorgängig: Export aus Online-Feldbuch wie oben beschrieben.
#### Artdaten in R importieren und zu Kreuztabelle umwandeln 
Dieses [R-Skript](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/blob/main/Artendaten_Info_Flora_FB_de_v.1.2.R) beschreibt den Import der Artdaten und ihre Umwandlung in eine Kreuztabelle in R. Als Plot-ID wird die vom Feldbuch generierte "releve_id" verwendet.


#### Kopfdaten in R importieren
[R Skript](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/blob/main/Vegetationsdaten_Info_Flora_FB_de_v.1.2.R) beschreibt den Import der Kopfdaten in R.
Als Plot-ID wird der in der FlorApp erfasste "Name der Vegetationsaufnahme" verwendet
<br />
<br />


<a name="VEGEDAZtransformieren"></a>
## 3.Vegetationsaufnahmen in VEGEDAZ importieren
Vorgängig: Export aus Online-Feldbuch wie oben beschrieben.
  <br />
***Artdaten importieren***

1. VEGEDAZ öffnen. *Datei > Import*.

2. Im neuen Fenster (siehe unten): *Beobachtungen einzeln*, Trennzeichen *TAB (Tabulator-Zeichen)* wählen, OK klicken, die csv-Datei mit den Artdaten auswählen und OK klicken
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/aee38132-daf0-4ba8-bfc5-96c4ce0f0986)

   <br />

4. Im neuen Fenster (siehe unten) folgendes auswählen:
   - ***erwünschte Kopfdaten:*** <br />
         *"releve_id"* (Das ist die ID mit der die Art- und Kopfdaten verbunden werden)
   - ***Artnamen:*** <br />
         *"taxon_orig"* (Enstpricht dem Artname gemäss Checklist 2017 & addenda ohne Autoren, mit allfälligen "cf" im Namen plus den als Freitext erfassten Arten <br />
         oder <br />
         "taxon.taxon_name" (Entspricht dem Artname gemäss Checklist 2017 & addenda mit Autoren, aber "cf" und "Freitextarten" werden mit dieser option nicht importiert.
   - ***Deckungen:*** <br />
        *"supplements.cover.abs"* (Wenn Deckungen in Prozent geschätzt wurden)
  
   Nach Bedarf, weitere Zusätze:
   - ***erwünschte Art-Zusätze***: <br />
      supplements.releve.stratum (Wenn die Schicht erfasst wurde)
   ...
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/60d328c3-4450-46d8-a740-c5f284080f8b)

   <br />

***Kopf-/Umweldaten importieren***
   <br />
   
4. Cursor in Zelle "releve_id" setzten, danach mit Ctrl + Enter eine neue Zeile einfügen
5. Kopfdaten (releve_export.csv) öffnen mit Ctrl + A alles markieren (alternativ nur relevante Spalten markieren) mit Ctrl + C alles kopieren
6. VEGEDAZ: *Bearbeiten - Einfügen (Optionen) -->*
7. Im neuen Fenster Option *"(+Alt) Transponieren, überschreiben" wählen - "ok"*
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/1f87eec7-499c-49a2-b3c3-b5d11c50e983)
   <br />
   
8. Wenn Schichten Importiert wurden Menü *Bearbeiten* - *Ersetzten* um die Schicht Codes vom Feldbuch durch die Schicht-Codes von VEGEDAZ zu ersetzten
   <br />
   
   Codes Feldbuch:
   ♃ = Krautschicht; v = Strauchschicht;  Y = Baumschicht; ψ = Moosschicht
      <br />
      
   Codes VEGEDAZ:
   /K = Krautschicht; /S = Strauchschicht; /B = Baumschicht; / M = Moosschicht
   <br />
   
   ![grafik](https://github.com/smwidmer/vegetationsdaten_info_flora_feldbuch/assets/89586146/5a9002dd-2d8c-4431-a902-19e9116c5f27)

Wenn zusätzliche Kopfdaten, die nur in den exportierten Artdaten vorhanden sind (z.B. Koordinaten) ins VEGEDAZ importiert werden möchten, können z.B. in Excel die entsprechenden Einträge mit der Funktion EINDEUTIG für jede Aufnahme (releve_id) zusammengestellt werden und dann ebenfalls transponiert ins VEGEDAZ eingefügt werden.
Alternativ kann auch das [R Skript](Vegetationsdaten_Info_Flora_FB_de_v.01.R) verwendet werden und bei Bedarf die Daten anschliessend ins VEGEDAZ importiert werden


   


