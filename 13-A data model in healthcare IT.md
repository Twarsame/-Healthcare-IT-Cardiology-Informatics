### Data Model Architecture

```mermaid
graph TB
    subgraph DM["<b>Data Model Architecture</b>"]
        Blueprint["<b>Architectural Blueprint</b><br/>Defines structure & semantics"]
        Semantic["<b>Semantic Representation</b><br/>What, How, Why"]
    end
    
    subgraph Core["<b>Core Components</b>"]
        Storage["<b>Clinical Information Storage</b><br/>Persistent data repositories"]
        Organization["<b>Organization</b><br/>Structured relationships"]
        Retrieval["<b>Retrieval</b><br/>Query & access patterns"]
        Exchange["<b>Exchange Across Systems</b><br/>Interoperability standards"]
    end
    
    subgraph Semantics["<b>Semantic Layer</b>"]
        What["<b>What Information</b><br/>Clinical entities & attributes"]
        Relations["<b>How It Relates</b><br/>Relationships & hierarchies"]
        Constraints["<b>Validity Constraints</b><br/>Clinical rules & standards"]
    end
    
    subgraph Systems["<b>Healthcare Systems</b>"]
        EHR["<b>Electronic Health Records</b>"]
        PACS["<b>Picture Archiving Systems</b>"]
        LIS["<b>Laboratory Systems</b>"]
        RIS["<b>Radiology Systems</b>"]
    end
    
    Blueprint --> Semantic
    Semantic --> Storage
    Semantic --> Organization
    Semantic --> Retrieval
    Semantic --> Exchange
    
    Storage --> What
    Organization --> Relations
    Retrieval --> What
    Exchange --> Constraints
    
    What --> Relations
    Relations --> Constraints
    
    Storage -.->|Stores in| EHR
    Storage -.->|Stores in| PACS
    Storage -.->|Stores in| LIS
    
    Exchange -->|Connects| EHR
    Exchange -->|Connects| PACS
    Exchange -->|Connects| LIS
    Exchange -->|Connects| RIS
    
    Organization -->|Structures| EHR
    Retrieval -->|Queries| EHR
    Retrieval -->|Queries| PACS
    Retrieval -->|Queries| LIS
    
    style Blueprint fill:#FF6B6B,stroke:#C92A2A,stroke-width:3px,color:#FFFFFF
    style Semantic fill:#4ECDC4,stroke:#087F5B,stroke-width:3px,color:#000000
    style Storage fill:#FFD93D,stroke:#F59F00,stroke-width:3px,color:#000000
    style Organization fill:#A8DADC,stroke:#1864AB,stroke-width:3px,color:#000000
    style Retrieval fill:#95E1D3,stroke:#087F5B,stroke-width:3px,color:#000000
    style Exchange fill:#F38181,stroke:#C92A2A,stroke-width:3px,color:#FFFFFF
    style What fill:#FAB1A0,stroke:#D63031,stroke-width:3px,color:#000000
    style Relations fill:#74B9FF,stroke:#0984E3,stroke-width:3px,color:#000000
    style Constraints fill:#A29BFE,stroke:#6C5CE7,stroke-width:3px,color:#FFFFFF
    style EHR fill:#00D2D3,stroke:#01A3A4,stroke-width:3px,color:#000000
    style PACS fill:#FF9FF3,stroke:#F368E0,stroke-width:3px,color:#000000
    style LIS fill:#54A0FF,stroke:#2E86DE,stroke-width:3px,color:#FFFFFF
    style RIS fill:#FECA57,stroke:#EE5A6F,stroke-width:3px,color:#000000
    style DM fill:#1A1A2E,stroke:#16213E,stroke-width:4px,color:#FFFFFF
    style Core fill:#2D4263,stroke:#C84B31,stroke-width:4px,color:#FFFFFF
    style Semantics fill:#0F4C75,stroke:#3282B8,stroke-width:4px,color:#FFFFFF
    style Systems fill:#383E56,stroke:#FB9300,stroke-width:4px,color:#FFFFFF
```
### Step-by-Step Diagram Description

1. **Data Model Architecture Foundation:** At the top level, the diagram establishes the foundational concept that a data model serves as an architectural blueprint, defining both structure and semantics of healthcare information systems.
2. **Semantic Representation Layer:** The blueprint flows into semantic representation, which answers three critical questions: What information matters, How it relates to other data, and Why certain constraints exist.
3. **Core Components:** The semantic layer branches into four essential functions: Storage (persistent repositories), Organization (structured relationships), Retrieval (query patterns), and Exchange (interoperability standards).
4. **Semantic Layer Details:** These core components connect to three semantic elements: What Information (clinical entities), How It Relates (relationships and hierarchies), and Validity Constraints (clinical rules ensuring data integrity).
5. **Healthcare Systems Integration:** The diagram shows how these components interact with actual healthcare systems including EHR (Electronic Health Records), PACS (Picture Archiving), LIS (Laboratory Systems), and RIS (Radiology Systems).
6. **Data Flow Patterns:** Solid arrows represent direct conceptual flows (e.g., Blueprint → Semantic → Components), while dotted lines show practical implementations (e.g., Storage stores in EHR/PACS/LIS).
7. **System Interactions:** The Exchange component connects all four healthcare systems, Organization structures the EHR, and Retrieval queries multiple systems (EHR, PACS, LIS), demonstrating the interconnected nature of healthcare IT infrastructure.
8. **Color Coding:** Each component uses distinct vivid colors to enhance visual distinction—from coral reds for blueprints to turquoise for storage, making the complex relationships easier to understand at a glance.
