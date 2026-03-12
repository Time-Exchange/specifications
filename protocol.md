# Time-Exchange Protocol v1.0

This document defines the data structures and communication sequences for the Time-Exchange network.

## 1. Data Structures

### A. The Time Unit Transfer (TUT)
Every exchange must be encapsulated in a TUT object.

```json
{
  "header": {
    "version": "1.0",
    "network_id": "time-exchange-mainnet"
  },
  "payload": {
    "transfer_id": "UUID-v4",
    "timestamp": "ISO-8601-UTC",
    "sender_address": "Ed25519_Public_Key",
    "receiver_address": "Ed25519_Public_Key",
    "amount_tu": 1.0, 
    "service_hash": "SHA-256-Hash-of-Service-Description"
  },
  "signatures": {
    "sender_sig": "Signature_Hex",
    "receiver_sig": "Signature_Hex"
  }
}

```

### B. Service Offer (Broadcast)

Used to notify the network of available skills or needs.

* **Type:** `OFFER` or `NEED`
* **Location:** Geohash (optional for local matching)
* **TTL:** Time-to-live for the broadcast.

## 2. Communication Sequence (Handshake)

To prevent double-spending of time and ensure mutual consent, the protocol follows a 3-way handshake:

1. **PROPOSE:** Sender sends a `DirectRequest` to the Receiver.
2. **ACKNOWLEDGE:** Receiver accepts and signs a `PendingTransfer`.
3. **COMMIT:** Once the service is rendered, both parties provide a final signature, and the node broadcasts the `TUT` to the network for ledger inclusion.

## 3. Cryptography

* **Identity:** All addresses are generated using **Ed25519** key pairs.
* **Hashing:** **SHA-256** is used for all content and block hashing.
* **Verification:** A transfer is only valid if both signatures match the public keys in the payload.

## 4. Anti-Spam (Rate Limiting)

Since the system is zero-cost, it is vulnerable to spam.

* **Rule:** A single Node ID cannot broadcast more than 5 `OFFER/NEED` messages per hour.
* **Rule:** A cüzdan can only have one `PENDING` transaction at a time with the same peer.

---
