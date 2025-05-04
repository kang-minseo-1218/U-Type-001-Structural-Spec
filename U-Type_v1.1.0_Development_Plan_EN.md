# U-Type-001 v1.1.0 Development Plan

## 1. Command Exception Handling Structure

* **Mixed Command Handling**: When multiple commands like emotion suppression + parallel execution are issued, priority rules must be defined.
  * Example: `Designer Mode + Recovery Mode` → Apply Designer first, then trigger Recovery support
  * ✅ [Improved] Priority table between modes to be inserted (`Designer > Controller > Emotion Suppression > Recovery`)

* **Unstructured Natural Commands**: Fallback system needed for unstructured free-text commands
  * Example: “I'm angry now” → Auto-detect `Emotion Suppression` mode + trigger `State Diagnosis` mode
  * ✅ [Improved] Intent recognizer invoked first + fallback rule definition added

* **Command Conflict Detection**: If conflicting commands occur within one session, log them automatically and resolve by predefined priority
  * ✅ [Improved] Add conflict log + forced termination rule

---

## 2. API Integration & Extensibility

* **Command API Exposure**: Key commands (mode switch, recognizer calls) exposed via REST API/GraphQL
  * ✅ [Improved] Endpoint examples added: `/switch_mode?target=designer`, `/invoke_agent`

* **Frontend Integration Guidelines**:
  * Voice command processing (e.g., Whisper integration)
  * Visual feedback UI when commands are applied

* **Security Protocol**:
  * ✅ [Improved] Access tokens tied to `mode_level` (`admin`, `user`, `observer`)

---

## 3. Multi-User Architecture

* **User-Based Segmentation**: Recognizer/mode sets split per user ID
  * ✅ [Improved] Use of `user_profile.yaml` for configuration

* **Role-Based Privileges**: Operators vs general users get different access to modes

* **Parallel Execution Limits**: Prevent conflict if same recognizer is called simultaneously
  * ✅ [Improved] Apply mutex lock structure (`mutex-agent-call`)

---

## 4. Versioning & Metadata Policy

* **Release Tag Types**:
  * `spec-v1.x.x` → Structural specification
  * `exec-v1.x.x` → Execution-level command version

* **SHA256 Enforcement**:
  * ✅ [Improved] Auto-generated SHA per file + dual metadata validation

* **Fingerprint-ID**:
  * Designer ID + date fixed tag (e.g., `minseo_kang::U-Type::v1.1.0`)

---

## 5. Prioritization Proposal

1. Exception handling (command conflict, fallback)
2. API integration (natural command → system trigger)
3. Multi-user module (role segmentation, session separation)
4. Metadata/Version policy (hash, ID, release distinction)
5. Frontend interaction (UI feedback, voice input)

---

## 🔐 Risk Table & Response Plan

| Risk Item | Severity (1–5) | Mitigation |
|-----------|----------------|------------|
| Mode conflict | 4 | Insert mode priority table, forced-stop rules |
| Unstructured input | 3 | Fallback + emotion recognizer triggered |
| API abuse risk | 5 | `mode_level` role-based access token policy |
| Multi-user conflict | 4 | Recognizer instance split + mutex on parallel use |
| Hash inconsistency | 3 | Auto SHA + dual metadata registry |
| UI sync failure | 2 | Apply UI↔system sync structure |

---

## 🔚 Document Purpose

This document outlines the technical strategy for U-Type-001 version 1.1.0.  
It will be included in the `spec-v1.1.0` release as the official planning directive,  
including fingerprint identity and integrity mechanisms.

---

**📌 SHA256 Hash:**  
fce0db7cb3608eab87c40e0fbd7096fd569fb922fb51736e73c3ed9d5630a891
