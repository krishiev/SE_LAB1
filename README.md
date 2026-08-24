# Domain & SSL Certificate Expiry Alert System

## 1. Requirements Table

| ID | Type | Description | Priority | Acceptance Criteria | Rationale |
| :---: | :---: | :--- | :---: | :--- | :--- |
| **FR-001** | Functional | The system shall initiate TLS handshakes against monitored domains daily, extract certificate expiration dates, and trigger alerts at 30, 15, and 3 days before expiry. | High | **Pass:** Alert queued for certificate expiring in 15 days.<br>**Fail:** Expired certificate ignored without notification. | Ensures proactive replacement of SSL certificates to avoid service downtime. |
| **FR-002** | Functional | The system shall perform automated daily WHOIS registration audits for all configured domains to extract domain expiration dates. | High | **Pass:** System correctly extracts expiration date and queues an alert.<br>**Fail:** WHOIS query fails silently or misparses the date. | Prevents loss of domain ownership due to accidental expiration. |
| **FR-003** | Functional | The system shall provide an escalation ladder for alerts, routing notifications to the SysAdmin initially, and escalating to the Security Officer if unacknowledged within 24 hours. | Medium | **Pass:** Notification escalated to Security Officer after 24 hours of no response.<br>**Fail:** Alert remains stale without escalation. | Ensures critical expiration alerts are noticed and acted upon by a higher authority if missed. |
| **FR-004** | Functional | The system shall allow SysAdmins to add, update, and delete domains and SSL endpoints from the monitoring list via a dashboard. | High | **Pass:** New domain added appears in the next daily scan cycle.<br>**Fail:** CRUD operations fail or do not update the active scan list. | Provides administration capabilities to manage the scope of monitored IT assets. |
| **FR-005** | Functional | The system shall log all handshake results, WHOIS data changes, and sent alerts into an audit trail accessible by the Security Officer. | Medium | **Pass:** Security Officer can view a complete log of alerts sent over the past 30 days.<br>**Fail:** Logs are missing or inaccessible to authorized roles. | Essential for compliance and security auditing of IT operations. |
| **NFR-001** | Non-Functional (Performance) | The monitoring engine shall scan a list of 1,000 domains and SSL endpoints in under 3 minutes. | High | **Pass:** Benchmarking tests confirm target latency under simulated peak load.<br>**Fail:** Scanning 1,000 domains takes longer than 3 minutes. | High throughput ensures that the daily monitoring window does not interfere with other operations. |
| **NFR-002** | Non-Functional (Security) | All stored WHOIS and SSL configuration details, as well as communication channels for alerts, must use secure encryption (e.g., AES-256 for storage, TLS 1.3 for transit). | High | **Pass:** Vulnerability scanner verifies all data in transit and at rest is securely encrypted.<br>**Fail:** Cleartext sensitive endpoint data detected in transit. | Protects infrastructure details from eavesdropping and malicious targeting. |

## 2. UML Use-Case Diagram

flowchart LR
    %% Actors
    subgraph Actors
        SysAdmin["SysAdmin"]
        SecOfficer["Security Officer"]
        System["System"]
    end

    %% System Boundary
    subgraph "Domain & SSL Expiry Alert System"
        UC_Auth(["Authenticate User"])
        UC_Manage(["Manage Monitored Assets"])
        UC_Audit(["Audit Scan Results"])
        UC_Receive(["Receive Expiry Alerts"])
        UC_Escalate(["Escalate Alert"])
        UC_Scan(["Perform TLS & WHOIS Scan"])
    end

    %% Actor to Use Case Connections
    SysAdmin --> UC_Manage
    SysAdmin --> UC_Audit
    SysAdmin --> UC_Receive

    SecOfficer --> UC_Audit

    System --> UC_Scan
    System --> UC_Escalate

    %% Include and Extend Relationships
    UC_Manage -.->|«include»| UC_Auth
    UC_Audit -.->|«include»| UC_Auth
    UC_Escalate -.->|«extend»| UC_Receive
