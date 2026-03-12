# Architecture Specification v1.0

## 1. Zero-Cost Infrastructure Model
To ensure the system remains free and accessible forever, Time-Exchange does not rely on centralized cloud providers.

### A. Peer-to-Peer (P2P) Foundation
- **Node Type:** Every participant runs a "Light Node" via mobile or desktop.
- **Discovery:** Uses a Distributed Hash Table (DHT) for peer discovery without a central tracker.
- **Communication:** Gossip protocol for broadcasting service offers and transaction validations.

### B. Distributed Ledger
- **State Management:** A lightweight, append-only ledger synchronized across the network.
- **Consensus:** A custom "Proof of Gratitude" (PoG) or "Proof of Service" (PoS) mechanism that doesn't require energy-intensive mining.

## 2. System Components (Microservices)
The system is divided into modular services to be implemented in their respective repositories:

1. **Exchange Engine:** Handles the matching logic (finding a service provider for a specific need).
2. **Transaction Verifier:** Validates signatures from both parties to authorize a Time Unit (TU) transfer.
3. **Identity & Reputation:** A decentralized identity system (DID) that tracks "Trust Scores" without storing personal data.

## 3. Technology Stack Requirements
- **Core:** Rust (for memory safety and performance on low-power devices).
- **Communication:** libp2p or similar P2P frameworks.
- **Storage:** IPFS or localized SQLite-based state for mobile nodes.
