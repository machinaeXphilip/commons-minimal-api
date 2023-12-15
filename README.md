Skizze
# Eine Meta-Such-API für zirkuläre Angebote

## Worum geht es?

In einer „Meta-Such-API“ werden Organisationen von gebrauchtem Material und leihbaren Gegenständen verbunden. Die Suche ist nur lokal und gilt (ersteinmal) für Berlin. Die Suchmaschine liest Daten von für sie registrierten Plattformen bzw. Online-Datenbanken aus und integriert sie in einer zentrale Suche für Anfragen.

## Wie soll das funktionieren?
Die Plattformen selbst geben ihre Daten über eine hier zu definierende API (Programmier-Schnittstelle) im JSON Format frei. Die Meta-Suchmaschine, greift bei Suchanfragen dann auf alle verbundenen und erreichbaren Plattform Schnittstellen-Endpunkte zu und bietet Benutzer:innen dann 

## Die Vorteile. Welchen Fortschritt bringt es?

Mit nur einer einzigen Suche können User:innen gleichzeitig in verschiedenen Einrichtungen nach Material und Leihdingen suchen.
Dies führt zu einer Vergrößerung der Zielgruppe, weil im Verbund mehr gefunden wird, als allein.
Wenn User:innen mehr passende Angebote finden, bedeutet das auch mehr Umsatz.

## Die Roadmap. Wie umsetzen?
 
Die beteiligten Plattformen und Einrichtungen bauen eine API-Daten-Schnittstelle ein, die von der Meta-Suchmaschine ausgelesen werden kann.

Auf einer zentralen Seite wird dann ein Suchformular angeboten dass auf die Daten zugreift und sie entsprechend der Suchfilter der Nutzer:in präsentiert und bietet ihnen dann Kurzbeschreibungen der gefunden Dinge als auch Direktlinks zu den Plattformen oder sogar (je nach Plattform) auf die gefundenen Dinge an.

- [x] Definiton der API als minimal Version
    - [x] Research: Wie beschreiben die teilnehmenden Plattformen die Orte ihrer Dinge?
- [ ] Einbindung der API in mind. 3 Platformen
- [ ] Erste Prototypen für UI/UX und Backend service als proof-of-concept mit Real-Daten
- [ ] weitere Iterationen mit mehr Partner-Plattformen, Ausbau des Frontends und Backends mit UserTests
- [ ] Einbindung in schon bestehende Karten die bisher nur Initativen verlinken aber noch keine Dinge.

# Datenfelder (json)

> Jedes Datum beschreibt ein einzelnes Ding das auf der Plattform zu finden ist

1) Suche- Name des Materials oder Gegenstands (text)
2) Beschreibung des Materials oder Gegenstands und zusätzliche informationen über den leihvorgang und regeln, wenn der link des (text)
3) Location: Geo-Daten, wir folgen dem Format eines GEOJSON Features, aber betonen fürs erste dass geography leer sein darf und wir benutzen stattdessen das subfeld properties mit dem von uns dort platzierten (und bis auf weiteres forcierten) Feld `zip` für die Postleitzahl in dem der Gegenstand gefunden werden kann. In späteren Iterationen sollten wir auch geographische Daten erlauben und `properties.zip` nicht mehr erzwingen. 
4) Reuse-Category: kaufen / leihen / schenken / mieten (enum)
5) Policy (vorbedingung zu dingzugriff der jeweiligen plattform. Einige Plattformen werden das pro Ding definieren, andere werden dieselbe Kategorie auf alle dinge anwenden): hinz-und-kunz (alle duerfen anfragen), netzwerk/freund:innen (invite members only), mitglieder (benoetigt account auf der platform), other (für mischungen der vorgenannten oder situationen die anders sind und deshalb in der Beschreibung/description des Items beschrieben werden)
6) URL zum Gegenstand in der anbietenden/verwaltenden Platform. Wenn direktlinks nicht möglich sind: Link zur Plattform/Leihort selbst (url)

# Wichtige Referenzen

1. in der Entwicklung schauen wir immer wieder auf die [Commons API](https://github.com/wielebenwir/commons-api) anschauen, die schon hervorragende Vorarbeit geleistet hat und wahrscheinlich ein umfangreicheres feature-set bietet. Für die ersten Schritte wird das allerdings zu umfangreich sein. Ziel sollte aber sein so kompatibel zu designen wie möglich, um später ggf. von der commons-minimal-api auf die commons-api upzugraden.
