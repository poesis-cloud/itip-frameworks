# ITIP Frameworks

Sourced governance/compliance/architecture/regulatory framework schemas for the **IT Intelligence Platform (ITIP)**, expressed as GSM-compatible ascription statements (JSON Schema archetypes + Directive/Norm instances).

This repository was extracted from `itip/def/frameworks/` to be distributed and versioned independently of the private `itip` design repository, following the same publication posture as GSM's schema/conformance layer (open vocabulary, governed core stays with the product).

> This repository is in a **design-time** phase. It contains framework model schemas and sourced governance instances — no runnable application code.

## What's in here

Every file in `def/` is an **ascription statement** — the JSON content that populates `AscriptionCreationDto.statement` when ingested by the SIE Definition Manager. The ascription archetype (which validates the statement) is encoded in the filename suffix. See [`sie-definition-manager/def/statement/README.md`](https://github.com/poesis-cloud/sie-definition-manager/blob/main/def/statement/README.md) for the full Statement File Naming Convention.

```txt
def/
  README.md                 # Inter-model articulation and composition (P9)
  itip/                      # ITIP domain archetypes & governance mechanisms
    meta-governance/          # SourcedDirective, SourcedNorm, mechanism, appraisal
    technology/                # SoftwareTechnology, etc.
  {authority}/               # e.g. togaf/, iso25000/, nis2/, gdpr/, scap/, http/, ...
    {taxonomy}/                # Model-native domain decomposition (P9)
      {Title}.schema.json        # Archetype schemas
      {ConceptName}{ArchetypeTitle}.json  # Statement instances
    README.md                  # Model-specific documentation
```

## Sourced Models

| Model | Source Standard | Scope |
|-------|----------------|-------|
| **TOGAF** | TOGAF Standard, 10th Edition (The Open Group) | Enterprise Architecture — structures, behaviors, governance, ADM |
| **ISO 25000 (SQuaRE)** | ISO/IEC 25010:2011 + 25011:2017 + 25012:2008 | Quality Models — product, service, and data quality |
| **NIS2** | Directive (EU) 2022/2555 | EU Cybersecurity — entity classification, risk management, incident reporting, supply chain |
| **GDPR** | Regulation (EU) 2016/679 | EU Data Protection — processing principles, lawful basis, data subject rights, controller/processor obligations |
| **SCAP** | NIST SP 800-126 r3 (SCAP 1.3) | Security Identification — CPE, CCE |
| **aDRI-IRN** | Alliance for Digital Resilience Initiative | Open resilience standard (reserved — README only) |
| **HTTP** | RFC 9110 | HTTP protocol semantics quad |
| **gRPC / GraphQL / Kafka / AMQP / WebSocket / JDBC** | Respective protocol specs | Reserved (README only) until first sourced |
| **ITIP** | CRUD (James Martin); SCAP CPE 2.3 | ITIP domain vocabulary — CRUD effector semantics, technology identification, governance sourcing |

See [`def/README.md`](def/README.md) for the full inter-model articulation (how models compose through GSM Directives/Norms rather than within schemas).

## Role in the Poesis architecture

- **GSM** (`gsm` repo) provides the universal governance grammar: Structure, Mechanism, Interaction, Directive, Norm, Ascription, Archetype.
- **ITIP** (`itip` repo, private) is the domain application that consumes these schemas as tenant archetypes, subject to the same Ascription lifecycle and validation rules as all other Archetypes.
- **SIE Definition Manager** (`sie-definition-manager` repo) enforces GSM invariants on all archetypes at ingestion time.
- This repository (`itip-frameworks`) is the **published, versioned source** of the sourced framework vocabulary — schemas here are logically namespaced under `gsmarc://itip/frameworks/...`, independent of which repository physically hosts the files.

## Provenance note

Schemas are derived vocabulary (structure, property names, governance grammar), not reproductions of the source standards' normative text. See `CONTRIBUTING.md` for the sourcing/provenance contribution rule.
