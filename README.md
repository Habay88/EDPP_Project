
# PROJECT CHARTER

Project Name: Enterprise Digital Payments Platform (EDPP)
Duration: 13 Jan – 13 Mar 2026
Project Manager / Lead Developer: Banjoko Abiodun Lateef
Project Type: Enterprise-grade fintech application

#BUSINESS GOALS,
1. Enable fast, secure digital payments

     #Simulate card, wallet, and merchant transactions in compliance with payment standards.

2. Provide end-to-end transaction visibility

     #Real-time tracking of transaction status, audit logs, and reconciliation reports.

3. Integrate card-industry standards

     #EMV simulation and ISO 8583 message processing to mimic real-world banking/payment systems.

4. Deliver production-quality code and architecture

     #Modular Spring Boot services, containerized with Docker.

5. Develop leadership & delivery experience

     #Execute project management, sprint planning, backlog prioritization, and stakeholder reporting.
#SUCCESS METRICS

| Category                   | Metric                            | Target                                                 |
| -------------------------- | --------------------------------- | ------------------------------------------------------ |
| **Functional**             | Core transaction flow operational | 100% of CRUD + transaction lifecycle working           |
|                            | EMV simulation implemented        | At least ARQC generation + response mapped to ISO 8583 |
|                            | ISO 8583 message handling         | Request & response simulation operational              |
| **Quality**                | Unit test coverage                | ≥ 60% across services                                  |
|                            | Code review & refactoring         | Zero critical bugs on final review                     |
| **Delivery / TPM**         | Milestone adherence               | All major milestones delivered on time                 |
|                            | Documentation completeness        | Architecture, API specs, TPM reports delivered         |
| **Performance & Security** | Response times                    | <500ms for main API calls under mock load              |
|                            | JWT & role-based security         | Enforced across all APIs                               |
| **Operational / UX**       | Reconciliation accuracy           | ≥ 99% simulated transaction correctness                |
|                            | Settlement job success rate       | 100% successful run on mock batch data                 |

# Define payment platform scope (issuer, merchant, wallet)
Merchant → ISO 8583 / Wallet API → Issuer Authorization Engine
        → EMV Validation (simulated)
        → Wallet Balance Check
        → Authorization Response
        → Settlement & Reconciliation
   #ISSUER (BANK OR FINTECH)
      → Issues payment instruments (cards / wallets)
        Authorizes transactions
        Manages balances, limits, and risk rules
       In-Scope (Issuer Responsibilities)
Account & Instrument Management

Issue virtual payment instruments (wallet-linked card simulation)

Maintain customer account status (ACTIVE, BLOCKED, SUSPENDED)

Manage transaction limits (daily, per-transaction)
 Authorization & Decisioning

Validate incoming transaction requests

Perform balance checks

Apply authorization rules:

Sufficient funds

Velocity checks

Account status validation

Generate authorization response:

APPROVED

DECLINED (with reason codes)

EMV & ISO 8583 Simulation

Parse ISO 8583 authorization requests (MTI 0200)

Interpret EMV data (DE55 simulation)

Validate:

Amount (DE4)

PAN (masked)

STAN (DE11)

Generate authorization response (MTI 0210)

Produce response codes (DE39)

Risk & Controls

Basic fraud simulation rules:

Amount threshold breaches

Duplicate STAN detection

Transaction velocity checks
#MERCHANT 
 Merchant Definition

The Merchant represents any business entity that:

Accepts payments

Initiates payment requests

Receives settlement funds

In-Scope (Merchant Responsibilities)
Merchant Onboarding

Merchant registration & profile creation

Assign:

Merchant ID

Terminal ID

Merchant status management (ACTIVE / SUSPENDED)

Transaction Initiation

Initiate payment requests:

Card-based (ISO 8583 simulation)

Wallet-based (internal API)

Send transaction data:

Amount

Currency

Terminal ID

Merchant category

Transaction Monitoring

View transaction status:

INITIATED

AUTHORIZED

SUCCESS

FAILED

Query transaction history & reports

Settlement & Reporting

Participate in end-of-day settlement

View settlement reports:

Gross amount

Fees (simulated)

Net settlement
# WALLET DOMAIN SCOPE 
Wallet Definition

The Wallet represents a stored-value account that:

Holds customer funds

Acts as a funding source for transactions

Links to simulated card credentials

In-Scope (Wallet Responsibilities)
Wallet Lifecycle

Wallet creation

Wallet activation / deactivation

Wallet-to-user linking

Balance Management

Wallet funding (top-up simulation)

Wallet debit for transactions

Balance integrity & locking

Available vs ledger balance handling

Transaction Support

Support:

Wallet payments

Card-linked wallet payments

Maintain transaction history per wallet

Controls

Prevent overdraft

Enforce wallet limits

Ensure idempotent debits

| Domain   | Primary Owner         | Key Outputs       |
| -------- | --------------------- | ----------------- |
| Issuer   | Authorization Service | Approval/Decline  |
| Merchant | Merchant Service      | Payment Requests  |
| Wallet   | Wallet Service        | Balance Integrity |

 