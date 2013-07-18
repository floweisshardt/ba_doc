## 1. Einleitung
 - Bedeutung von Tests in Softwareenwicklung ( Unit-Test / Functional-Test )

## 2. Problemstellung
 - Zwei Anwedertypen:
 - Problem Applikationsentwickler: 
   + Vielzahl Komponenten in ROS
   + Komponenten verwenden verschieden Konzepte zur Problemlösung -> unterschiedliche Lösungs-Qualität für unterschiedliche Anforderungen
   + Welche Komponente geeignet für sein Szenario
   + Individuelle Gewichtung von: Schnelligkeit / Zuverlässigkeit / Rotation / Kollisionen je nach Szenario
 - Problem von Komponentenentwickler: 
  * Verbessung der eigenen Navigation 
  * Optimierung der Navigation für alle/bestimmte Szenarien


## 3. Lösungsansatz
 - Mit Komponentenkatalog die Arbeit für Komponentenentwicker und Applikationsentwickler vereinfachen
 - Visuelle Aufbereitung von Testergebnissen
 - Alles ros-basiert: Kein Know-How von Web- oder anderen Technologien notwendig: rosmake / roslaunch 
 - Durch Verwendung von git-Repositories als Datenbank: leichte Kollaboration verschiedener Entwickler
 - Testergebisse als Junit-XML: Einbindung in CI Jenkins/Hudson
 - Komponentenbasierter Ansatz ermöglicht leichten Einsatz auf Simulation oder Roboter

 - Vorteile für Applikationsentwickler:
   * Kontinuierliche Vergleichsmöglichkeiten mite alternativen Komponenten
   * Einfaches Testen der verwendeten Komponente mit eigenem Szenario (nur ein Meta-Package benötigt)
   * Durch kontinuierliches Testen (Jenkins) wird sichergestellt, dass die Navigationsaufgabe zuverlässig erfüllt werden kann
   * Durch kontinuierliches Testen werden viele Informationen gesammelt -> Sicherheit gegenüber Varianz

 - Vorteile für Komponentenentwickler:
   * Protokoll über die Entwicklung der Navigationskomponente
   * Analyse einer Komponente in einer Vielzahl von Umgebungen
   * Automatische Benachrichtigung bei Programmierfehlern (unit-tests, jenkins, janniks Arbeit) oder funktionalen Fehlern (Ziel nicht gefunden, Kollisionen verursacht, meine Arbeit)
   * Vergleich mit anderen Komponenten
   * Identifizierung der Anwendugnsmöglichkeiten: Wo geeignet, wo nicht
   * Problemanalyse (z.B. unerklärlichen Kollisionen) in zwei Schritten:
     + Kofortables Playback des aufgezeichneten Videos über Webinterface
     + Bag-File kann vom Server geladen werden und lokal detailiert analysiert werden


## 4. Implementierung
 - Interaktionsdiagramm jenksin + navigation_test Komponenten
 - Test+Analyse: Jenkins + Skeleton + Analysis
 - Visualisierung + Bereitstellung: Github + Component-Catalogue + Video-Server (Modul Teil von Component Catalogue, aber auf anderem Server)

 - Generisch:
   * Skeleton: 
     + Technologie: python mit ros-api
     + Gazebo-Simulation / Camera Roboter-Tracking / Service-Aufruf setupRobot / Aufnehmen Bag-Files ( collisions,tf,... ) / Erste Analyse: Werden Goals erreicht: Success,Failure

   * collisions_detection:
     + hört auf bumper topics und published spezielles collisions topic für skeleton

   * Analyse:
     + Technologie: python mit ros-api
     + Auswertung verschiedener Metriken: Zeit, Rotation, Kollision, Distanz... 
     + Playback von Camera Topics + Aufnehmen Video-File / Push der Ergebisse in Repository

   * component_catalogue: 
     + Technologie: Python (Server) / Coffee-Script Client auf Backbone Framework
     + Component-Catalogue zweigeteilt:
     + Web-Server: Entry-Point / Visualiserung der Ergebisse / Verbindung zu Video-Server
     + Video-Server: Git Informationen über vorhanden Videos zu Bag-Files / Bietet Download von Videos


 - Cob-Spezifisch:
   * Prepare-Robot: Einfahren Roboter-Arm

## 5. Evaluation
 - Beispiel für 10x Sim + 10x real für kleine und große Umgebung
 - Vergleich/Übertragbarkeit sim auf real

## 6. Zusammenfassung und Ausblick
 - Ausblick auf andere Komponenten (Objekterkennung)
 - Weitere Unterstützungsmöglichkeiten für Komponenten-/ und Applikationsentwickler
