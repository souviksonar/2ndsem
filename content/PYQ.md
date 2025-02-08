# Q4 Graph (Hypercube) in Mermaid

This README shows how to represent a 4-dimensional hypercube (Q4) graph using Mermaid. A hypercube graph has vertices representing bitstrings of length *n*, and edges connect vertices that differ in only one bit. Q4 has 2^4 = 16 vertices.

```mermaid
graph LR;
    subgraph Layer0
        style Layer0 fill:#f9f,stroke:#333,stroke-width:2px
        V0000["0000"]:::vertex
    end

    subgraph Layer1
        style Layer1 fill:#ccf,stroke:#333,stroke-width:2px
        V0001["0001"]:::vertex
        V0010["0010"]:::vertex
        V0100["0100"]:::vertex
        V1000["1000"]:::vertex
    end

    subgraph Layer2
        style Layer2 fill:#fcf,stroke:#333,stroke-width:2px
        V0011["0011"]:::vertex
        V0101["0101"]:::vertex
        V0110["0110"]:::vertex
        V1001["1001"]:::vertex
        V1010["1010"]:::vertex
        V1100["1100"]:::vertex
    end

    subgraph Layer3
        style Layer3 fill:#cff,stroke:#333,stroke-width:2px
        V0111["0111"]:::vertex
        V1011["1011"]:::vertex
        V1101["1101"]:::vertex
        V1110["1110"]:::vertex
    end

    subgraph Layer4
        style Layer4 fill:#ffc,stroke:#333,stroke-width:2px
        V1111["1111"]:::vertex
    end

    V0000 --> V0001;
    V0000 --> V0010;
    V0000 --> V0100;
    V0000 --> V1000;

    V0001 --> V0011;
    V0001 --> V0101;
    V0001 --> V1001;

    V0010 --> V0011;
    V0010 --> V0110;
    V0010 --> V1010;

    V0100 --> V0101;
    V0100 --> V0110;
    V0100 --> V1100;

    V1000 --> V1001;
    V1000 --> V1010;
    V1000 --> V1100;

    V0011 --> V0111;
    V0011 --> V1011;

    V0101 --> V0111;
    V0101 --> V1101;

    V0110 --> V0111;
    V0110 --> V1110;

    V1001 --> V1011;
    V1001 --> V1101;

    V1010 --> V1011;
    V1010 --> V1110;

    V1100 --> V1101;
    V1100 --> V1110;

    V0111 --> V1111;
    V1011 --> V1111;
    V1101 --> V1111;
    V1110 --> V1111;


   classDef vertex fill:#fff,stroke:#333,stroke-width:1px
```
```