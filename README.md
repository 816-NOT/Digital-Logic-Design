# Digital-Logic-Design
# Digital Logic Design - 4-Bit Cascading Subtractor

## Project Overview
This project implements a structural **4-Bit Cascading Binary Subtractor** designed and verified within CircuitVerse. The architecture utilizes a modular hierarchy, packaging a custom 1-bit full subtractor cell into a reusable block component and cascading four instances to compute multi-bit binary subtraction. 

The layout incorporates consolidated input and output buses to optimize workspace scannability and simulation efficiency.

## Circuit Architecture & Specifications
- **Logic Design Style:** Structural, modular hierarchical cascade (Ripple-Borrow).
- **Core Component:** 1-Bit Full Subtractor sub-circuit module.
  - *Difference Formula:* $D = A \oplus B \oplus B_{in}$
  - *Borrow-Out Formula:* $B_{out} = (\overline{A} \cdot B) + (\overline{A} \cdot B_{in}) + (B \cdot B_{in})$
- **Inputs:** Consolidated 4-bit binary data streams ($A[3..0]$ and $B[3..0]$) managed via multi-bit interactive numeric blocks and splitters.
- **Outputs:** A combined 4-bit bus ($S[3..0]$) routed through an output splitter directly into a Hexadecimal LED Display for clear, single-digit real-world value tracking.
- **Status/Sign Flag:** A standalone 1-bit final Borrow-Out ($B_{final}$) indicator linked to the MSB block to serve as a negative sign identifier (active during Two's Complement wrap-around operations).

## Verification & Test Bench Results
The system was verified across all operational quadrants to confirm accurate borrow propagation. The data path ripples natively from the Least Significant Bit (Block 0) to the Most Significant Bit (Block 3):

1. **Positive Range test ($12 - 4$):** Inputs `1100` and `0100` return a hex display value of `8`. Sign bit reads `0`.
2. **Identity Zero test ($9 - 9$):** Inputs `1001` and `1001` completely clear the data path, returning a hex display value of `0`. Sign bit reads `0`.
3. **Two's Complement Boundary test ($0 - 1$):** Inputs `0000` and `0001` force a continuous cascade of borrow requests through every block layer. The system correctly outputs `F` (`1111` in binary, representing $-1$ in 4-bit Two's Complement notation) and successfully drives the standalone sign flag to `1`.
