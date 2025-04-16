## 1. Analyse der Stakeholder & Anforderungen

### a) Stakeholder-Übersicht

- **Geschäftsführung (GF)**
  - **Anforderungen:**  
    - Wöchentliche KPI-Dashboards (Absatz, Umsatz, Retouren, Lagerbestände)  
    - Frühwarnsystem bei sinkender Marge oder Materialverknappung  
    - Vergleich zwischen Filialumsätzen und Online-Shop  
  - **Ziel:** Datenbasierte, automatisierte Entscheidungsfindung und strategische Planung.

- **Marketing**
  - **Anforderungen:**  
    - Echtzeit-Analyse der Kampagnen-Performance  
    - Zielgruppenanalysen aus Online-Shop- und CRM-Daten  
    - Schnittstellen zu Social Media Ads & Google Analytics  
  - **Ziel:** Optimierung der Kampagnen, gezielte Ansprache der Zielgruppen und stetige Performance-Verbesserung.

- **Vertrieb**
  - **Anforderungen:**  
    - Regionale Verkaufsstatistiken  
    - Analyse der Umsatzentwicklung nach Kundensegmenten  
    - Prognose-Tool für saisonale Schwankungen (z. B. Oktoberfest)  
  - **Ziel:** Umsatzsteigerung durch genaue Marktanalysen und präzise Prognosemodelle.

- **Produktion**
  - **Anforderungen:**  
    - Anbindung von Produktionssystemen (z. B. Sensorik, IoT-Temperatursensoren)  
    - Optimierung der Chargenplanung anhand von Absatzprognosen  
    - Rückverfolgbarkeit bei Qualitätsproblemen  
  - **Ziel:** Effizienzsteigerung der Produktionsprozesse und Sicherstellung der Produktqualität.

- **IT & Datenschutz**
  - **Anforderungen:**  
    - DSGVO-konforme Datenverarbeitung  
    - Integration vorhandener Systeme (SAP ERP, Magento-Shop, Excel-Reports, SQL-Server)  
    - Zukunftssicherheit, Skalierbarkeit und einfache Erweiterbarkeit  
  - **Ziel:** Minimierung des Integrationsaufwands und Gewährleistung einer robusten, skalierbaren Infrastruktur.

### b) Zielkonflikte & Kritische Datenquellen

- **Datenqualität & Konsistenz:**  
  Unterschiedliche Abteilungen nutzen variierende Begrifflichkeiten (z. B. „Umsatz“ vs. „Netto-Umsatz“). Es ist entscheidend, eine einheitliche Definition und standardisierte Datenmodelle zu etablieren.

- **Offline- vs. Online-Daten:**  
  Die Zusammenführung von stationären Filialdaten (z. B. aus SAP ERP) und Online-Transaktionsdaten (z. B. Magento E-Commerce, CRM) erfordert einen soliden ETL-Prozess zur Datenintegration und -harmonisierung.

- **Schnittstellen & Legacy-Systeme:**  
  Bestehende Systeme wie SAP ERP, Magento und der ältere SQL-Server müssen angebunden werden.

- **Stakeholder-Misstrauen gegenüber Neuerungen:**  
  Einige Abteilungen könnten gegenüber neuen Tools skeptisch sein. Hier ist eine transparente Kommunikation und Einbeziehung der Endnutzer im Pilotprojekt wichtig.

---

## 2. Vorschlag eines MIS-Technologie-Stacks

### a) Datenbank & Persistenzschicht

- **PostgreSQL:**  
  - **Begründung:**  
    - Hohe Zuverlässigkeit, starke SQL-Compliance und Erweiterbarkeit  
    - Open Source und kosteneffizient  
    - Gut geeignet zur Verwaltung von großen, strukturierten Datenmengen  
  - **Relevanz:** Unterstützt konsistente Datenhaltung aus verschiedenen Quellen und gewährleistet stabile Performance.

### b) Backend

- **Rust:**  
  - **Begründung:**  
    - Hohe Leistung und Sicherheit
    - Steigender Usage in bedeuteten Projekten / Hohes Investment

### c) Messaging & Integration

- **RabbitMQ:**  
  - **Begründung:**   
    - Ermöglicht asynchrone Kommunikation zwischen den Systemkomponenten (z. B. zwischen Produktionssensoren und dem zentralen MIS)  
    - Unterstützt skalierbare und flexible Workflows  
  - **Relevanz:** Erleichtert den Datenaustausch zwischen ERP, E-Commerce, IoT und Analysewerkzeugen.

### d) ETL-Schicht

- **Data Pipelines:**  
  - Einsatz von z. B. Apache NiFi oder Airbyte zur Anbindung und Harmonisierung der Daten aus SAP, Magento, Excel-Reports und IoT-Systemen.  
  - **Begründung:** Datenflusssteuerung und vereinfacht das Daten-Mapping.

### f) Präsentationsschicht

- **NextJS / Vue / Angular**
    - **Begründung:**
        - Schneller Workflow
        - Schnelles Prototyping

### Erweiterte Tabelle

Komponente | Technologie | Beschreibung | Stakeholder-Bezug
Datenbank & Persistenz | PostgreSQL | Stabile, performante Datenhaltung, Open Source Lösung | GF, IT, Marketing, Vertrieb, Produktion
Backend & Programmiersprache | Rust | Hohe Performance und Sicherheit, ideal für ETL-Prozesse und IoT-Integration | IT, Produktion, Vertrieb
Messaging & Integration | RabbitMQ | Sicherer, asynchroner Nachrichtenaustausch, Integration heterogener Systeme | IT, Produktion, Vertrieb
ETL- & Datenintegrationsschicht | Apache NiFi / Airbyte | Harmonisierung und Zusammenführung diverser Datenquellen | IT, GF, Vertrieb
Präsentationsschicht | React / Vue.js / Angular | Moderne, responsive Weboberflächen für Dashboards und Reporting-Tools, intuitive Benutzerführung | GF, Marketing, Vertrieb, IT

## 3. 3-Minuten-Pitch an die Geschäftsführung



## 4. Reflexion & Einführungskonzept

### a) Einführung & Change Management

- **Schrittweise Implementierung:**
  - **Proof of Concept (PoC):** Testlauf in einem kleinen, kontrollierten Umfeld.
  - **Pilotphase:** Erweiterung auf mehrere Abteilungen, intensive Schulungen und Einbeziehung von Endnutzern.
  - **Rollout:** Stufenweiser Einsatz im gesamten Unternehmen
- **Kommunikationsstrategie:**
  - Regelmäßige Updates und Informationsveranstaltungen

### b) Erwartete Widerstände

- **Sturer Widerstand und Misstrauen gegenüber neuen Tools:**  
  - Enge Einbindung der Endnutzer in den Entwicklungsprozess um das Eis zu brechen.
- **Datenqualität und Integrationsprobleme:**  
  - Zeitaufwändige Datenharmonisierung und Standardisierung; Investition in ETL-Prozesse.
- **Ressourcenknappheit im IT-Team:**  
  - Einsatz von cloudbasierten Lösungen und gegebenenfalls externe Unterstützung in der Pilotphase.

### c) MVP (Minimum Viable Product)

- **Dashboard und Reporting:**  
  - Erstes MVP könnte ein Dashboard-Modul für die Geschäftsführung sein, das wöchentliche KPIs (Absatz, Umsatz, Lagerbestände) konsolidiert.
- **ETL-Pipeline für kritische Datenquellen:**  
  - Integration der wichtigsten Daten aus SAP ERP, Magento und Sensoren, um verlässliche Datenbasis für die Analysen zu schaffen.
- **Alerting und Frühwarnsystem:**  
  - Ein grundlegendes Frühwarnsystem zur Erkennung von Margenrückgängen oder Materialverknappungen, das auf einfache Trigger-Regeln setzt.
