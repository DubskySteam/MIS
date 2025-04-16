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

#### **1. Datenqualität & Konsistenz**  
- Unterschiedliche Definitionen von Kennzahlen (z. B. „Umsatz“ vs. „Netto-Umsatz“) führen zu abteilungsübergreifenden Inkonsistenzen.  
- Historische Excel-Reports vs. strukturierte SAP-Daten erfordern eine Harmonisierung.  

#### **2. Offline- vs. Online-Daten**  
- Filialumsätze (SAP) und Online-Shop-Daten (Magento) müssen zusammengeführt werden, ohne Verzerrungen zu erzeugen.  
- Unterschiedliche Datenformate (z. B. Transaktionsdaten vs. CRM-Segmente).  

#### **3. Echtzeit vs. Ressourcen**  
- Marketing fordert Echtzeit-Analysen, aber das kleine IT-Team (3 Personen) hat begrenzte Kapazitäten für komplexe Streaming-Architekturen.  
- IoT-Daten (Produktion) benötigen schnelle Verarbeitung, aber Legacy-Systeme bremsen.  

#### **4. Datenschutz (DSGVO) vs. Datenzugriff**  
- Social-Media-/Google Analytics-Anbindung vs. lokale Compliance-Anforderungen.   

#### **5. Skalierbarkeit vs. Kosten**  
- Cloud-Lösungen sind schneller und einfacher skalierbar, koennen aber schnell zu hohen Rechnungen beitragen (AWS S3 Drama als Beispiel)  

#### **6. Legacy-Systeme vs. Modernisierung**  
- Anbindung alter Systeme (SQL-Server, SAP) an moderne (Cloud-)Tools erfordert Middleware.  
- Risiko von Datenbrüchen bei Migration.  

#### **7. Akzeptanz vs. Veränderungsdruck**  
- Misstrauen einzelner Abteilungen gegenüber neuen Tools („Excel reicht uns“).  
- Schulungsaufwand für die neue Software.  


### **Kritische Datenquellen**  
- **SAP ERP**: Kerndaten zu Filialumsätzen, Lagerbeständen.  
- **Magento**: Online-Shop-Daten (Customer Journey, Retouren).  
- **IoT-Sensoren**: Produktionsdaten (Temperatur, Chargenqualität).  
- **Excel**: Historische Reports (manuelle Pflege → Fehleranfälligkeit).  
- **CRM/Google Analytics**: Externe Daten (Zielgruppen, Kampagnenperformance).

## 2. Vorschlag eines MIS-Technologie-Stacks

### a) Datenbank & Persistenzschicht

- **PostgreSQL:**  
  - **Begründung:**  
    - Hohe Zuverlässigkeit, starke SQL-Compliance und Erweiterbarkeit  
    - Open Source und kosteneffizient  
    - Gut geeignet zur Verwaltung von großen, strukturierten Datenmengen 
    - Bewährte Integration mit SAP und Magento. 
  - **Relevanz:** Unterstützt konsistente Datenhaltung aus verschiedenen Quellen und gewährleistet stabile Performance.

### b) Backend

- **Rust (Framework: Rocket/Actix):**  
  - **Begründung:**  
    - Hohe Leistung (Kein LLVM Backend)
    - Memory Safety für kritische Prozesse (z.B. ETL, IoT-Datenverarbeitung).
    - Steigender Usage in bedeuteten Projekten (Linux & Windows Kernel) -> Hohes Investment in Weiterentwicklung
    - Einfaches cross-compilen auf jede Architektur

### c) Messaging & Integration

- **RabbitMQ:**  
  - **Begründung:**   
    - Ermöglicht asynchrone Kommunikation zwischen den Systemkomponenten (z. B. zwischen Produktionssensoren und dem zentralen MIS)  
    - Unterstützt skalierbare und flexible Workflows  
    - Erleichtert den Datenaustausch zwischen ERP, E-Commerce, IoT und Analysewerkzeugen.

### d) ETL-Schicht

- **Data Pipelines:**  
  - Einsatz von z. B. Apache NiFi oder Airbyte zur Anbindung und Formatierung der Daten aus SAP, Magento, Excel-Reports und IoT-Systemen.  
  - **Begründung:**
    - Datenflusssteuerung und vereinfacht das Daten-Mapping.
    - Visuelle Orchestrierung von Datenflüssen zwischen SAP, Magento, Excel und PostgreSQL.

### f) Präsentationsschicht

- **NextJS**
    - **Begründung:**
        - Schnelle Ladezeiten für Echtzeit-Dashboards (Marketing/GF).
        - Schnelles Prototyping
        - Gutes Basispaket an UI Elementen (Charts, Auth etc.)

### Erweiterte Tabelle

Hier ist die Tabelle im kopierfähigen Format:

| **Komponente** | **Technologie**  | **Beschreibung** | **Stakeholder-Bezug** |
|---------------|-------|-----|--------------|
| **Datenbank & Persistenz** | PostgreSQL | Skalierbare SQL-Datenbank für strukturierte Daten (Filialumsätze, IoT-Sensoren). | **GF** (KPIs), **IT** (Wartung), **Produktion** (IoT-Daten), **Vertrieb** (Lagerbestände). |
| **Backend & Integration** | Rust (Rocket/Actix) | Hochperformante Backend-Logik für ETL, IoT und SAP/Magento-Schnittstellen.      | **IT** (Entwicklung), **Produktion** (Echtzeitverarbeitung), **Vertrieb** (Prognose-Tools). |
| **Messaging** | RabbitMQ | Asynchrone Kommunikation zwischen IoT, ERP und Analyse-Tools.                   | **Produktion** (Sensor-Daten), **IT** (Systemstabilität), **Vertrieb** (Bestellungen).       |
| **ETL & Datenintegration** | Apache NiFi | Automatisierte Harmonisierung von SAP, Magento, Excel und IoT-Daten.            | **IT** (Pipeline-Orchestrierung), **GF** (Datenkonsistenz), **Marketing** (Zielgruppendaten). |
| **Präsentationsschicht** | Next.js| Interaktive Dashboards mit Echtzeitdaten | **GF** (KPIs), **Marketing** (Kampagnenanalysen), **Vertrieb** (Regionale Statistiken).       |

## 4. Reflexion & Einführungskonzept

### a) Einführung & Change Management

- **Schrittweise Implementierung:**
  - **Proof of Concept (PoC):** Testlauf in einem kleinen, kontrollierten Umfeld. Eventuell unter Einbezug eines Mitarbeiters.
  - **Pilotphase:** Erweiterung auf mehrere Abteilungen, intensive Schulungen und Einbeziehung von Endnutzern.
  - **Rollout:** Stufenweiser Einsatz im gesamten Unternehmen
- **Kommunikationsstrategie:**
  - Regelmäßige Updates und Informationsveranstaltungen

### b) Erwartete Widerstände

- **Sturer Widerstand und Misstrauen gegenüber neuen Tools:**  
  - Enge Einbindung der Endnutzer in den Entwicklungsprozess um das Eis zu brechen.
- **Datenqualität und Integrationsprobleme:**  
  - Zeitaufwändige Datenaufbereitung und Standardisierung ->  Investition in ETL-Prozesse.
- **Ressourcenknappheit im IT-Team:**  
  - Einsatz von cloudbasierten Lösungen und gegebenenfalls externe Unterstützung in der Pilotphase.
  - Temporaere Einstellung von Software-Entwicklern, falls das Team den Aforderungen nicht gerecht werden kann.

### c) MVP (Minimum Viable Product)

- **Dashboard und Reporting:**  
  - Erstes MVP könnte ein Dashboard-Modul für die Geschäftsführung sein, das wöchentliche KPIs (Absatz, Umsatz, Lagerbestände) abbildet.
- **ETL-Pipeline für kritische Datenquellen:**  
  - Integration der wichtigsten Daten aus SAP ERP, Magento und Sensoren, um verlässliche Datenbasis für die Analysen zu schaffen.
- **Alerting und Frühwarnsystem:**  
  - Ein grundlegendes Frühwarnsystem zur Erkennung von Margenrückgängen oder Materialverknappungen, das auf einfache Trigger-Regeln setzt.
