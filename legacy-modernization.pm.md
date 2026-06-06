# Legacy Modernization {type="ProductModel"}

Legacy modernization is the process of re-binding decisions that earlier teams already bound - in older languages, against older requirements,
often with the original intent now lost across generations of owners and maintainers.
This model treats that work as a product rather than a one-off migration: the personas below carry distinct, frequently competing concerns,
and the capabilities exist to serve those concerns explicitly rather than by informal consensus.
The aim is to preserve business intent while replacing the runtime, surfacing trade-offs between stakeholders as
deliberate choices instead of side effects of technical decisions.

## Personas

### Business Owners

Have knowledge of business logic and edge cases.
In many cases of legacy modernization such knowledge is lost because the system lived through multiple
generations of business owners, maintainers and other personals.

#### Goals

##### Behaviorial parity

The modernized system must produce the same outputs for the same inputs as the legacy
system - including edge cases and undocumented behavior. 
Because business logic accreted across generations of owners and maintainers and is often no longer written down anywhere,
parity is verified mechanically against captured legacy behavior rather than against specs
that may not exist. 

Phase 1 Direct Semantic Execution preserves legacy semantics exactly, so parity is structural rather than interpretive.

##### SLA continuity

Service levels the business currently depends on - throughput, latency, availability, batch
completion windows - must hold through and after migration.
Modernization changes the runtime, not the commitments made to downstream consumers, so existing SLAs are carried into the target
as constraints rather than renegotiated by the migration.

### Enterprise Architecture

Owns the target state. Concerned that each migrated unit aligns with the target reference architecture and that the modernization
adds the minimum bespoke surface area needed - moving the estate toward a deliberate destination, not just off the legacy stack.

::: Goals {type=Goal}

Below are enterprise architecture goals:

#### Strategic direction

Each modernized deployment unit should move the estate toward the target reference architecture,
not merely off the legacy stack.
Per-unit approach selection is made explicit through structured decision analysis so individual
migration choices compose into the intended end state instead of drifting into incidental, comfort-driven outcomes.

#### Vendor independence

Remove the hard dependency on the legacy vendor's proprietary runtime and formats.
Phase 1 (DSE) achieves this first by executing legacy artifacts AS-IS on an owned model-driven engine - a
defensible end state on its own and a precondition for unconstrained Phase 2 modernization.
Keeping bespoke surface area in the target minimal prevents trading one form of lock-in for another.

:::


### Operations/SRE

Supports the system in production, before and after cutover.
Concerned with retaining observability, troubleshooting access, and valid runbooks, so the modernized system is no harder to keep running than the one it replaces.

#### Goals

##### Observability continuity

Production troubleshooting access and telemetry available on the legacy system must remain
available on the modernized one.
Model-based telemetry emits traces tagged by model element URI, giving operators unified troubleshooting across the model and the running system.

##### Runbook continuity

Existing operational procedures and on-call runbooks must remain valid or be regenerated alongside
the migration, so the system stays supportable in production from cutover onward.

### Security & Risk

Owns control posture and compliance. Concerned that controls have demonstrable equivalents post-migration, that the transition itself is auditable,
and that no control gaps open during phased cutover.

#### Goals

##### Control posture equivalence

Security and compliance controls present in the legacy system must have demonstrable equivalents
post-migration, with no weakening of posture introduced by the runtime change.

##### Audit trail through transition

The migration itself must be auditable - what was translated, how, and verified against what - and
existing audit trails (e.g., for SOX) must survive the transition rather than be broken by it.

##### No control gaps during cutover

Phased cutover must avoid windows where a control present in the legacy system is absent in the
target.

### Delivery Management

Owns timeline and budget. Concerned with time-to-value, visible incremental progress, and predictable milestones - which is why
early removal of the legacy runtime dependency (Phase 1) matters more than a distant big-bang finish.

#### Goals

##### Time-to-value

Deliver removal of the legacy runtime dependency early (Phase 1) to realize value and de-risk
before the longer Phase 2 work, rather than waiting on a single large rewrite.

##### Predictable milestones

Per-deployment-unit phasing produces visible, incremental progress and predictable milestones
instead of a big-bang schedule with a single uncertain finish.

### Maintainers

Will own and evolve the system once the migration team is gone.
Concerned that behavior is captured in a model with regression coverage rather than residing in people's heads, so the system can be changed safely and traceably after cutover.

#### Goals

##### Ability to evolve safely post-migration

After cutover, maintainers must be able to change the system with confidence.
Because behavior is captured in a model with regression coverage and the runtime is owned rather than vendor-controlled,
changes can be validated against preserved semantics — turning a system whose logic lived in
people's heads into one that can be evolved with traceability.

## Capabilities

### Documentation generator

Legacy artifacts may require legacy editors/viewers which will be gone
post-migration.
It is important to have documentation of the system as it was.
For a small system it can be done by taking screenshots.
For a system of non-trivial size it might be more efficient to
write a documentation generator.

