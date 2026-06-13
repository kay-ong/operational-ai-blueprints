%%{init: {
'theme': 'base',
'themeVariables': {
'lineColor': '#64748B'
}
}}%%
graph TD
%% Define Styles
classDef inputs fill:#161F30,stroke:#24324D,stroke-width:2px,color:#fff;
classDef agent1 fill:#3F1D24,stroke:#EF4444,stroke-width:1px,color:#FCA5A5;
classDef agent2 fill:#0B6F19,stroke:#7C3AED,stroke-width:2px,color:#fff;
classDef agent3 fill:#10B981,stroke:#059669,stroke-width:2px,color:#fff;

    A[Inbound Vendor Email] --> B[1. Ingestion Agent]
    B -->|"JSON Payload + Confidence Score"| C{Confidence Threshold Check}
    C -->|Below 0.92 | D[Human-in-the-Loop Sandbox]
    C -->|Above 0.92 | E[2. Validation Agent]
    E -->|Skill Binding: Query ERP & IMS | F{Anomaly Detected?}
    F -->|Yes | G[3. Resolution & Routing Agent]
    F -->|No | H[Standard Pass-Through Receipt]
    G -->|Skill Binding: Execute State Mutate | I[ERP / WMS Live Patch]

    %% Apply Styles
    class A,D,H inputs;
    class B,C agent1;
    class E,F agent2;
    class G,I agent3;
