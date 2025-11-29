## Skill #2: Data Architecture Decision-Making
---
What This Means
Selecting the appropriate Epic data tier (Chronicles vs. Clarity vs. Caboodle) based on latency requirements, query complexity, and integration patterns.
Why Hiring Managers Value This Skill
This distinguishes experienced consultants from junior resources:

Junior consultant: "I'll build the dashboard in Clarity SQL"
Senior consultant: "For real-time alerts we need Chronicles FHIR APIs; for historical trending we use Clarity; for population registry submission we use Caboodle dimensional model."
```mermaid
graph TD
    Start["<b>Decision Question 1: How fresh does the data need to be?</b>"] --> SubSecond
    Start --> FourHours
    Start --> TwentyFourHours
    Start --> Nightly
    
    SubSecond["⚡ Sub-second<br/>(real-time alerts, live dashboards)"]
    SubSecond --> UseChronicles["<b>Use: Chronicles via FHIR APIs</b>"]
    UseChronicles --> Example1["Example: Alert cardiologist when<br/>potassium drops below 3.0"]
    
    FourHours["🔄 Less than 4 hours<br/>(tactical operational dashboards)"]
    FourHours --> UseChroniclesHL7["<b>Use: Chronicles via FHIR or HL7 interfaces</b>"]
    UseChroniclesHL7 --> Example2["Example: Show current cath lab<br/>census and queue"]
    
    TwentyFourHours["📊 24 hours<br/>(operational reporting, quality dashboards)"]
    TwentyFourHours --> UseClarity["<b>Use: Clarity (relational SQL)</b>"]
    UseClarity --> Example3["Example: Report yesterday's echo<br/>turn-around times"]
    
    Nightly["📈 Nightly+<br/>(population analytics, registry submission)"]
    Nightly --> UseCaboodle["<b>Use: Caboodle (dimensional model)</b>"]
    UseCaboodle --> Example4["Example: Calculate NCDR CathPCI<br/>mortality risk scores"]
    
    style Start fill:#1a1a2e,stroke:#16213e,stroke-width:4px,color:#ffffff
    style SubSecond fill:#c41e3a,stroke:#8b0000,stroke-width:3px,color:#ffffff
    style FourHours fill:#ff6b35,stroke:#d84315,stroke-width:3px,color:#ffffff
    style TwentyFourHours fill:#0077b6,stroke:#023e8a,stroke-width:3px,color:#ffffff
    style Nightly fill:#7209b7,stroke:#3c096c,stroke-width:3px,color:#ffffff
    style UseChronicles fill:#d62828,stroke:#9d0208,stroke-width:3px,color:#ffffff
    style UseChroniclesHL7 fill:#f77f00,stroke:#dc2f02,stroke-width:3px,color:#ffffff
    style UseClarity fill:#0096c7,stroke:#023e8a,stroke-width:3px,color:#ffffff
    style UseCaboodle fill:#9d4edd,stroke:#5a189a,stroke-width:3px,color:#ffffff
    style Example1 fill:#ffccd5,stroke:#c1121f,stroke-width:2px,color:#000000
    style Example2 fill:#ffe5b4,stroke:#ff8500,stroke-width:2px,color:#000000
    style Example3 fill:#a8dadc,stroke:#1d3557,stroke-width:2px,color:#000000
    style Example4 fill:#e0aaff,stroke:#7209b7,stroke-width:2px,color:#000000
```
```mermaid
graph TD
    Start["Decision Question 1: How fresh does the data need to be?"] --> SubSecond
    Start --> FourHours
    Start --> TwentyFourHours
    Start --> Nightly
    
    SubSecond["⚡ Sub-second - real-time alerts, live dashboards"]
    SubSecond --> UseChronicles["USE: Chronicles via FHIR APIs"]
    UseChronicles --> Example1["Example: Alert cardiologist when potassium drops below 3.0"]
    
    FourHours["🔄 Less than 4 hours - tactical operational dashboards"]
    FourHours --> UseChroniclesHL7["USE: Chronicles via FHIR or HL7 interfaces"]
    UseChroniclesHL7 --> Example2["Example: Show current cath lab census and queue"]
    
    TwentyFourHours["📊 24 hours - operational reporting, quality dashboards"]
    TwentyFourHours --> UseClarity["USE: Clarity - relational SQL"]
    UseClarity --> Example3["Example: Report yesterday's echo turn-around times"]
    
    Nightly["📈 Nightly+ - population analytics, registry submission"]
    Nightly --> UseCaboodle["USE: Caboodle - dimensional model"]
    UseCaboodle --> Example4["Example: Calculate NCDR CathPCI mortality risk scores"]
    
    style Start fill:#000080,stroke:#ffffff,stroke-width:4px,color:#ffffff
    style SubSecond fill:#8b0000,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style FourHours fill:#ff4500,stroke:#000000,stroke-width:3px,color:#000000
    style TwentyFourHours fill:#006400,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style Nightly fill:#4b0082,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style UseChronicles fill:#dc143c,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style UseChroniclesHL7 fill:#ff8c00,stroke:#000000,stroke-width:3px,color:#000000
    style UseClarity fill:#228b22,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style UseCaboodle fill:#9370db,stroke:#ffffff,stroke-width:3px,color:#ffffff
    style Example1 fill:#ffc0cb,stroke:#8b0000,stroke-width:2px,color:#000000
    style Example2 fill:#ffd700,stroke:#8b4513,stroke-width:2px,color:#000000
    style Example3 fill:#98fb98,stroke:#006400,stroke-width:2px,color:#000000
    style Example4 fill:#dda0dd,stroke:#4b0082,stroke-width:2px,color:#000000
```
Worked Example: Echo Lab Dashboard Redesign
Problem Statement: Cardiology leadership wants to monitor echo lab productivity in real-time during business hours.
Consultant's Thought Process:

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#2E7D32','primaryTextColor':'#FFFFFF','primaryBorderColor':'#1B5E20','lineColor':'#F57C00','secondaryColor':'#C62828','tertiaryColor':'#0277BD','noteBkgColor':'#FFF9C4','noteTextColor':'#000000','textColor':'#FFFFFF','fontSize':'16px','fontFamily':'Arial'}}}%%

graph TB
    User["👤 Supervisor<br/>Dashboard User"]
    Dashboard["📊 Web Dashboard<br/>(React/Vue)"]
    FHIR["🔌 FHIR API<br/>Procedure Endpoint"]
    Chronicles["⚡ Chronicles Database<br/>(Real-time Clinical Data)"]
    
    User -->|"Views current shift"| Dashboard
    Dashboard -->|"GET /Procedure?<br/>date=today&<br/>status=in-progress"| FHIR
    FHIR -->|"Queries real-time data"| Chronicles
    Chronicles -->|"Returns:<br/>• Study count<br/>• Average time<br/>• Current status"| FHIR
    FHIR -->|"JSON response"| Dashboard
    Dashboard -->|"Displays live metrics"| User
    
    style User fill:#1976D2,stroke:#0D47A1,stroke-width:4px,color:#FFFFFF
    style Dashboard fill:#388E3C,stroke:#1B5E20,stroke-width:4px,color:#FFFFFF
    style FHIR fill:#D32F2F,stroke:#B71C1C,stroke-width:4px,color:#FFFFFF
    style Chronicles fill:#F57C00,stroke:#E65100,stroke-width:4px,color:#FFFFFF
```
```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#1565C0','primaryTextColor':'#FFFFFF','primaryBorderColor':'#0D47A1','lineColor':'#EF6C00','secondaryColor':'#C62828','tertiaryColor':'#00838F','fontSize':'15px','fontFamily':'Arial'}}}%%

flowchart LR
    subgraph Frontend["🖥️ Frontend Layer"]
        Dashboard["Dashboard UI<br/>(Real-time Updates)"]
    end
    
    subgraph API["🌐 Integration Layer"]
        FHIR["FHIR Server<br/>Procedure Resource"]
        Auth["OAuth 2.0<br/>Authentication"]
    end
    
    subgraph Backend["💾 Data Layer"]
        Chronicles["Chronicles DB<br/>(Live Data)"]
        Clarity["Clarity DB<br/>(❌ Not Used:<br/>24hr delay)"]
    end
    
    Dashboard -->|"Authenticated Request"| Auth
    Auth -->|"Token Valid"| FHIR
    FHIR <-->|"Real-time Query"| Chronicles
    FHIR -.->|"Not used for<br/>real-time"| Clarity
    FHIR -->|"JSON Response<br/>(&lt;1 sec)"| Dashboard
    
    style Dashboard fill:#2E7D32,stroke:#1B5E20,stroke-width:4px,color:#FFFFFF
    style FHIR fill:#1565C0,stroke:#0D47A1,stroke-width:4px,color:#FFFFFF
    style Auth fill:#6A1B9A,stroke:#4A148C,stroke-width:4px,color:#FFFFFF
    style Chronicles fill:#EF6C00,stroke:#E65100,stroke-width:4px,color:#FFFFFF
    style Clarity fill:#757575,stroke:#424242,stroke-width:3px,color:#FFFFFF,stroke-dasharray: 5 5
    
    style Frontend fill:#E3F2FD,stroke:#1976D2,stroke-width:2px,color:#000000
    style API fill:#FFF3E0,stroke:#F57C00,stroke-width:2px,color:#000000
    style Backend fill:#E8F5E9,stroke:#388E3C,stroke-width:2px,color:#000000
```
```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#0277BD','primaryTextColor':'#FFFFFF','primaryBorderColor':'#01579B','lineColor':'#D84315','fontSize':'16px'}}}%%

flowchart TD
    subgraph User_Layer["👤 User Layer"]
        Supervisor["Supervisor<br/>Monitoring Dashboard"]
    end
    
    subgraph Application_Layer["🌐 Application Layer"]
        WebApp["Web Application<br/>(React/Vue)"]
        API["FHIR API Gateway"]
    end
    
    subgraph Data_Layer["💾 Data Layer"]
        Chronicles["Chronicles DB<br/>⚡ Real-time"]
        Clarity["Clarity DB<br/>📊 Reporting Only"]
    end
    
    Supervisor -->|"Accesses"| WebApp
    WebApp -->|"REST Call"| API
    API -->|"Live Query"| Chronicles
    API -.->|"❌ Bypassed<br/>(too slow)"| Clarity
    Chronicles -->|"Results"| API
    API -->|"JSON"| WebApp
    WebApp -->|"Display"| Supervisor
    
    style Supervisor fill:#1976D2,stroke:#0D47A1,stroke-width:4px,color:#FFFFFF
    style WebApp fill:#388E3C,stroke:#1B5E20,stroke-width:4px,color:#FFFFFF
    style API fill:#D32F2F,stroke:#B71C1C,stroke-width:4px,color:#FFFFFF
    style Chronicles fill:#F57C00,stroke:#E65100,stroke-width:4px,color:#FFFFFF
    style Clarity fill:#616161,stroke:#424242,stroke-width:3px,color:#FFFFFF,stroke-dasharray: 5 5
    
    style User_Layer fill:#E3F2FD,stroke:#1976D2,stroke-width:3px,color:#000000
    style Application_Layer fill:#FFF3E0,stroke:#F57C00,stroke-width:3px,color:#000000
    style Data_Layer fill:#E8F5E9,stroke:#388E3C,stroke-width:3px,color:#000000
```

## Diagram Overview

The diagrams above illustrate the real-time data flow architecture for a supervisor dashboard system that monitors clinical procedures. They demonstrate how live operational data is accessed and displayed to healthcare supervisors.

### Key Components

### 1. 👤 User Layer

**Supervisor/Dashboard User:** The end-user who monitors current shift activities, study counts, and procedure statuses in real-time through a web interface.

### 2. 🖥️ Frontend Layer

**Web Dashboard (React/Vue):** The user-facing application that displays live metrics and provides an interactive interface for monitoring procedures. Updates dynamically as new data becomes available.

### 3. 🌐 Integration/API Layer

**FHIR API Server:** Serves as the integration middleware using the Procedure resource endpoint. Handles REST API calls and translates requests between the frontend and backend databases.

**OAuth 2.0 Authentication:** Provides secure access control, ensuring only authorized users can access real-time clinical data.

### 4. 💾 Data Layer

**Chronicles Database (⚡ Real-time):** The operational database that stores live clinical data with immediate updates. This is the primary data source for the dashboard, providing sub-second response times.

**Clarity Database (❌ Not Used):** A reporting database with a 24-hour data delay. Explicitly bypassed for real-time monitoring due to latency issues, though it may be used for historical reporting and analytics.

### Data Flow Process

1. Supervisor accesses the web dashboard
2. Dashboard sends authenticated request through OAuth 2.0
3. FHIR API receives the request and queries Chronicles database
4. Chronicles returns real-time data (study count, average time, current status)
5. FHIR API formats response as JSON
6. Dashboard displays live metrics to the supervisor

**Key Design Decision:** The architecture prioritizes Chronicles over Clarity specifically to achieve real-time performance, as Clarity's 24-hour delay makes it unsuitable for operational monitoring.
---

Resulting Dashboard Architecture:

```mermaid
graph LR
    A["Epic Chronicles"] -->|"FHIR API<br/>Procedure Resource"| B["Dashboard<br/>Backend"]
    B -->|"Query every<br/>30 seconds"| C["Real-Time<br/>Display"]
    C -->|"Current status"| D["Supervisor<br/>View"]
    
    style A fill:#E63946,stroke:#A4161A,stroke-width:4px,color:#FFFFFF
    style B fill:#06D6A0,stroke:#048A81,stroke-width:4px,color:#000000
    style C fill:#FFD166,stroke:#F77F00,stroke-width:4px,color:#000000
    style D fill:#118AB2,stroke:#073B4C,stroke-width:4px,color:#FFFFFF
```
```mermaid
graph TB
    A["📊 Epic Chronicles<br/>EMR System"] -->|"FHIR API<br/>Procedure Resource"| B["⚙️ Dashboard<br/>Backend Engine"]
    B -->|"Auto-refresh<br/>every 30 sec"| C["📺 Real-Time<br/>Display Monitor"]
    C -->|"Live Status<br/>Updates"| D["👥 Supervisor<br/>Control Panel"]
    
    style A fill:#D90429,stroke:#8D0801,stroke-width:5px,color:#FFFFFF,font-weight:bold
    style B fill:#00B4D8,stroke:#023E8A,stroke-width:5px,color:#FFFFFF,font-weight:bold
    style C fill:#FFB703,stroke:#C17900,stroke-width:5px,color:#000000,font-weight:bold
    style D fill:#06D6A0,stroke:#028A5E,stroke-width:5px,color:#000000,font-weight:bold
```
