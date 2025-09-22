# Flowchart of SM ab paper

Still incomplete but a decent start. 

```mermaid
graph TD
    subgraph Source calculation
        A1[Human excretion calculation]
        A2[Livestock excretion calculation]
        A3[Aquaculture emission calculation]
    end

    subgraph Pathways to river
        B1{Human waste treatment}
        B2{Livestock manure management}
        B3{Application to land}
        B4{Land-to-river transport}
    end

    subgraph In-river processes
        C1[Partitioning between water & particles]
        C2[Settling of particle associated antibiotics]
        C3[Decay of dissolved antibiotics]
    end

    subgraph Final calcs
        D1[Calculate total amount after removal At]
        D2[Get Monthly River discharge Qm]
        D3((Final monthly river concentration Cm))
    end

    A1 --> B1
    A2 --> B2
    A3 --> E[Total emission to rivers]

    B1 -- treated/untreated discharge --> E
    B1 -- Sludge application --> B3

    B2 -- Direct discharge --> E
    B2 -- Manure application --> B3

    B3 --> B4
    B4 -- Surface runoff & soil erosion --> E

    E --> C1
    C1 --> C2
    C1 --> C3

    C2 & C3 --> D1
    D1 & D2 --> D3
```

# Flowchart of risk part

Also added this risk part. I found it difficult to make.

```mermaid
graph LR
    subgraph Step 1: Gather Inputs
        A["`Modeled antibiotic concentration (PEC)`"]
        B["`Community PNEC data`"]
        C["`Pathogen MIC data`"]
    end

    subgraph Step 2: Tier 1 Individual Risk Assessment
        A & B --> T1a_Calc{"`Tier 1a: Calculate community RQ`"}
        T1a_Calc --> T1a_Out(("\`Community risk classification\`"))

        A & C --> T1b_PNEC{"`Tier 1b: Derive pathogen-specific PNEC`"</pre>}
        T1b_PNEC --> T1b_Calc{"`Calculate pathogen RQ`"}
        T1b_Calc --> T1b_Out(("\`Pathogen-specific risk assessment\`"))
    end

    subgraph Step 3: Tier 2 Mixture Risk Assessment
        T1a_Calc & T1b_Calc --> T2a_Calc{"`Tier 2a: Sum RQs for mixtures using concentration addition`"}
        T2a_Calc --> T2a_Out(("\`Screening-level mixture risk\`"))
        
        T2a_Out --> T2b_Input["`Input for refined analysis: E. coli & Fluoroquinolones`"]
        T2b_Input --> T2b_TU{"`Tier 2b: Calculate toxic units (TU)`"}
        T2b_TU --> T2b_PAF{"`Calculate multi-substance PAF`"}
        T2b_PAF --> T2b_Out(("\`Refined risk: Potentially affected fraction of E. coli\`"))
    end
```
