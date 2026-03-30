# Noe

**A deterministic symbolic protocol for representing bounded meaning across agents, runtimes, and modalities.**

Noe is a symbolic protocol for expressing compact, machine-interpretable structures with stable grammar, explicit context dependence, and replayable semantics. It is designed for systems that need meaning to remain inspectable, portable, and deterministic across implementations.

Noe is not a natural language, a planner, or a product surface. It is a protocol layer: a canonical symbolic substrate for representing relations, evidentiary status, conditions, actions, and other bounded semantic structures under explicit context.

A canonical Noe chain is authoritative. English glosses are display-only reading aids and are never used for parsing or evaluation.

<br />

## Why Noe exists

Modern intelligent systems do not share a stable substrate for meaning.

Humans communicate through natural language, which is expressive but ambiguous. A sentence like "I saw him with binoculars" has two valid parses in English, and humans resolve the ambiguity through context, tone, and shared assumptions. Protocols for machine coordination cannot rely on that. Structured software interfaces can move data, but they often leave meaning implicit. Large models operate through opaque latent representations that may appear meaningful while hiding uncertainty, drift, or internal inconsistency. Robots and cyber-physical systems often rely on local control logic and state representations that do not travel cleanly across systems.

This creates a practical Tower of Babel problem. Two systems may exchange the same string, label, or instruction while attaching different structures of meaning to it. A phrase like "the zone is clear" may be treated as a grounded fact by one system, a probabilistic estimate by another, and a user-interface label by a third. As agents become more autonomous and more interconnected, that semantic mismatch becomes a systems problem rather than just a usability problem.

Noe exists to provide a middle layer: not raw data transport, not free-form language, but a deterministic symbolic protocol for expressing bounded meaning in a form that can be parsed, evaluated, replayed, and audited consistently across heterogeneous systems.

<br />

## Design principles

Noe does not prescribe how a system arrives at meaning internally. Different systems may use language, heuristics, control logic, symbolic planning, probabilistic models, or learned representations. Noe does not require internal uniformity. Its role is narrower: to provide a canonical external form for the part of meaning that must be transmitted, interpreted, and evaluated reliably across a boundary. What is written should be what is evaluated. What is not expressed should not be inferred silently by the protocol.

This design is shaped by four competing requirements that cannot all be maximized simultaneously, a design quadlemma:

### Expressivity
The protocol must be able to represent more than simple yes/no values or labeled data fields. It must support structured meaning: evidentiary stance, logical composition, scope, conditions, relations, action emission, and higher-order symbolic structure. Every additional operator or structure increases what can be said, but also increases what must be learned and what must be transmitted.

### Compression
Meaning should be expressible in compact symbolic form. Chains should be short enough to transmit over constrained channels, evaluate efficiently, and remain readable without requiring paragraph-length expressions for simple conditions. But a highly compressed system always risks narrowing what it can express.

### Universality
The same chain should survive movement across agents, runtimes, modalities, and transport channels without semantic drift. Noe is intended to remain stable whether rendered visually, spoken through its phonetic forms, serialized in software, or mapped into constrained channels such as haptics, pulses, or light-based signaling. This shaped the glyph inventory itself: atomic symbols, stable phonetic forms, explicit structure, and low-ambiguity composition were chosen so that meaning can remain stable across channels where rich text may be unavailable or inappropriate. But a system designed to survive many channels will usually be less specialized than one optimized for a single medium or domain.

### Learnability
The protocol must be learnable by humans and implementable by machines without requiring extensive training or domain-specific expertise to read a chain. Symbols should be phonetically distinct, visually distinct, and semantically atomic. But simpler and more learnable systems usually sacrifice some expressive range and some compression.

Noe's design is a deliberate navigation of these tensions rather than an optimization of any single axis. The engineering properties visible in the protocol, such as deterministic parsing, explicit grounding under admitted context, and portable replay across conforming runtimes, are consequences of how the quadlemma is resolved rather than independent design goals.

<br />

## Why symbols, not keywords

Noe uses a purpose-built symbolic vocabulary rather than English keywords such as `KNOW`, `IF`, or `AND`. This is a deliberate design choice with three motivations.

### Language neutrality 
English keywords would make the protocol culturally and linguistically bound. Noe glyphs are registry-defined symbols rather than borrowed natural-language keywords. Like a codepoint in a character set, a glyph carries the meaning the registry assigns it.

### Phonetic discriminability
The phonetic forms are short and chosen for high distinctness in spoken, subvocalized, or constrained-channel settings. English words such as “know,” “no,” and “now” are comparatively confusable. Forms such as `shi`, `vek`, `khi`, and `mek` are intended to reduce that overlap. This was designed not only for speech and software legibility, but also with future constrained interfaces in mind, including BCI-adjacent settings where symbolic discriminability matters more than natural-language fluency.

### Semantic precision
Natural-language words carry connotations and historical baggage. “Know” in English can imply philosophical certainty, justified belief, or personal familiarity. `shi` is narrower: it names a specific protocol-level epistemic role defined by the registry and interpreted under explicit semantics.

Each glyph also has a registered visual form drawn from a dedicated symbol inventory, designed for visual distinctness in the same way the phonetic forms are designed for auditory distinctness. The full registry, including phonetic and visual forms, is defined in the glyph registry specification.

<br />

## Sample glyphs table

A small sample of registered glyphs appears below. Each glyph has a canonical visual form, phonetic form, and protocol role.

| Visual | Phonetic | Role |
|---|---|---|
| 𐌙 | dai | self / I |
| 𐌸 | syl | you / other |
| 𐌡 | sol | we / us |
| 𐍉 | sar | they |
| ʖ | shi | knowledge |
| ϕ | vek | belief |
| φ | sha | certainty |
| 𐌈 | nai | negation |
| ɨ | da | clause introduction / embedded proposition |
| 𐌹 | es | is / be |
| ⟑ | an | and |
| ƿ | ret | past |
| 𐍔 | mel | help |
| 𐌔 | har | want / desire |
| 𐍱 | qua | question marker |
| 𐍰 | vak | distinct / not-similar |
| 𐌵 | fel | joy |
| ⌑ | nem | peace / safety |

<br />

## Example symbolic chains

Simple Statement:
```text
𐌙 𐌹 𐌵
dai es fel
I AM JOY (HAPPY)
```

Negation:
```text
𐌸 𐌹 𐌈 𐌵
syl es nai fel
YOU ARE NOT JOY (HAPPY)
```

Comparison:
```text
𐍉 𐍰 𐌡
sar vak sol
THEY ARE DISTINCT FROM US
```

Temporal qualification:
```text
ƿ 𐌙 𐌹 ⌑
ret dai es nem
PAST SELF IS SAFE (I WAS SAFE)
```

Logic example:
```text
𐌙 𐌹 𐌵 ⟑ 𐌸 𐌹 ⌑
dai es fel an syl es nem
I AM JOY AND YOU ARE SAFE
```

Nested epistemic clause:
```text
𐌙 ʖ ɨ 𐌸 ϕ ɨ 𐌙 𐌈 φ
dai shi da syl vek da dai nai sha
I KNOW THAT YOU BELIEVE THAT I AM NOT CERTAIN
```

Question:
```text
𐍱 𐌸 𐌔 𐍔
qua syl har mel
QUESTION YOU WANT HELP?
```

<br />

## What Noe can represent

Noe is designed to express bounded semantic structures such as:

- Identity and reference
- Epistemic stance
- Nested or higher-order epistemic structure
- Logical composition
- Conditions and guarded actions
- Spatial relations
- Temporal relations
- Deixis and demonstratives
- Valence and affect
- Delivery, receipt, and audit semantics
- Morphological composition over atomic glyphs
- Quantitative and scalar modification
- Typed numeric and comparative structure
- Transport-independent symbolic expressions intended to survive text, speech, software serialization, and constrained channels such as haptics or light-based signaling

Noe is not just a vocabulary. It combines a finite registry of atomic symbols with constrained composition rules, explicit scope, and deterministic evaluation. Part of its design interest lies in how much semantic range can be built from a small, stable symbolic inventory without surrendering parse determinism.

<br />

## What Noe is not

Noe is not:

- a natural language
- a planner
- a controller
- a perception system
- a product
- a full reasoning engine

Noe does not perform sensing, world modeling, or control by itself. It does not replace robot controllers, runtime monitors, or free-form human language. It does not attempt to infer everything that follows from a proposition. It provides a symbolic protocol for representing and evaluating bounded semantic structures once context has been made explicit.

<br />

## Glyphs and literals

Noe does not require a dedicated glyph for every possible word, object, or domain concept. The protocol combines a stable core registry of glyphs with literals and grounded terms supplied by context.

Glyphs carry protocol-level structure and reusable semantic roles: identity, epistemics, logic, deixis, affect, relation, time, action, and other core operators. Literals carry domain-specific reference: objects, zones, channels, reports, entities, identifiers, or grounded predicates such as `@door_open` or `@zone_clear`.

This separation is deliberate. A protocol that attempted to assign a glyph to every concrete concept would become unbounded, brittle, and difficult to learn. Noe instead provides a compact symbolic core that can compose with literals and grounded context when needed.

In practice:
- Glyphs express structure
- Literals express domain-specific content
- Context determines how grounded literals are interpreted

This allows Noe to remain finite and learnable without becoming semantically trivial.

<br />

## Representative examples

The following examples are illustrative rather than exhaustive. English glosses are display-only reading aids. Canonical Noe chains remain authoritative.

### Epistemic stance

```
shi @door_open
KNOW @door_open
```

```
vek @door_open
BELIEVE @door_open
```

Glyphs / phonetics:
- `shi` = knowledge
- `vek` = belief / assumption

These are not the same statement. Noe makes evidentiary stance structurally explicit. A system that receives `shi @door_open` is being told the claim is grounded at the knowledge tier. A system that receives `vek @door_open` is being told it rests on weaker footing.

### Higher-order epistemic structure

```
dai shi da syl vek da dai nai sha
SELF KNOW THAT OTHER BELIEVE THAT SELF NOT CERTAIN
```

Glyphs / phonetics:
- `dai` = self / I
- `da` = that (clause introducer)
- `syl` = you / other
- `nai` = not
- `sha` = certainty

"I know that you believe I am not certain." This is not a flat assertion or a sensor predicate. It is nested symbolic structure over epistemic stance, expressed directly in the protocol rather than paraphrased in natural language or encoded in application metadata.

### Valence and intensity

```
dai es fel
SELF IS JOY

dai es fel´
SELF IS LOW_JOY (scalar 0.3)

dai es fel°
SELF IS STRONG_JOY (scalar 0.9)
```

Glyphs / phonetics:
- `es` = copula / is
- `fel` = joy / positive valence
- `´` (phonetic: -a) = low intensity, scalar 0.3
- `°` (phonetic: -o) = high intensity, scalar 0.9

Noe treats affect as a first-class symbolic domain, not as a tag or emoji. Intensity is scalar and typed: `´` maps to 0.3, unmarked to 0.6, `°` to 0.9. These are fixed scalars defined in NIP-006, not arbitrary weights. Intensity modifies degree but never truth. `fel°` is strong joy. It is not "more true" than `fel´`.

```
dai es dar°
SELF IS STRONG_PAIN
```

```
syl es nem´
OTHER IS LOW_CALM
```

- `dar` = pain / negative valence
- `nem` = calm / neutral valence

The same scalar system works across the valence space. Any affective root can carry intensity without special-casing.

### Questions

```
qua syl es fel° nek
QUESTION: OTHER IS STRONG_JOY? END

qua shi @channel_clear nek
QUESTION: KNOW @channel_clear? END
```

- `qua` = interrogative marker
- `nek` = required to close interrogative chains

The first asks about someone's affective state. The second asks whether a condition is established at the knowledge tier. Both use the same structural mechanism.

### Spatial and temporal relations

```
dai nel syl
SELF NEAR OTHER

ret dai nel syl
PAST SELF NEAR OTHER
```

- `nel` = near / proximal
- `ret` = past / prior

The first chain expresses a spatial relation. The second wraps the same relation in a temporal qualifier: "I was near you." Spatial and temporal operators compose directly with other structure rather than requiring separate annotation layers.

### Delivery and audit

```
vus @report an men @report
SEND @report AND AUDIT @report
```

- `vus` = send / deliver
- `men` = audit / verify

A chain pairing a transmission with an audit requirement. These operators make communication events part of the protocol's semantic surface rather than leaving them implicit in transport.

### Guarded action

```
shi @zone_clear khi sek mek @enter_zone_alpha sek nek
KNOW @zone_clear IF [ DO @enter_zone_alpha ] END
```

- `khi` = if / guard
- `sek` = explicit scope boundary
- `mek` = do / cause
- `nek` = end / chain terminator

A guarded action chain. If `@zone_clear` is admitted as grounded knowledge, emit the action. This is the pattern used most heavily by runtimes like Noe Gate, but it is one application of the protocol rather than its entirety.

### Logical composition

```
shi @temperature_ok an shi @location_ok
KNOW @temperature_ok AND KNOW @location_ok

dai es fel° ur syl es dar°
SELF IS STRONG_JOY OR OTHER IS STRONG_PAIN
```

- `an` = and
- `ur` = or

Logical operators compose over any well-formed subexpression, not only over sensor predicates. The second example shows disjunction over two valence predications with no external literals involved.

<br />

## A worked interaction

The examples above show individual chains. In practice, Noe is intended for symbolic interaction across systems.

A minimal interaction might look like:

```
noq @transmit_request
REQUEST @transmit_request
```

```
shi @channel_clear khi sek mek @transmit sek nek
KNOW @channel_clear IF [ DO @transmit ] END
```

```
vel @packet an men @packet
RECEIVE @packet AND AUDIT @packet
```

Read in sequence:

1. One party issues a structured request.
2. Another system evaluates a guarded action against admitted context.
3. Receipt and audit are expressed explicitly rather than assumed.

This is still a simple toy interaction, but it shows the protocol in motion: not just isolated symbolic statements, but serializable, evaluable structures that can participate in requests, conditional execution, and verifiable handoff.

<br />

## Core model

A Noe evaluation is defined relative to five elements: a chain, a registry, a grammar, a semantics, and an admitted context.

### Chain
The primary unit of expression in Noe is the chain: a canonical sequence of glyph tokens whose structure is determined by fixed grammar, explicit scope, and constrained operator roles. Meaning is serialized into a chain form that can be transmitted, parsed, replayed, and audited consistently across implementations.

### Registry
The registry defines the canonical symbol inventory: operators, glyphs, semantic anchors, phonetic forms, visual forms, and related metadata. Canonical meaning is rooted in the registry, not in informal translation or surface gloss. A core design principle is one-glyph-one-meaning.

### Grammar
The grammar defines which chains are well-formed and how they are parsed. Noe is designed so that valid chains have exactly one valid parse under a fixed formal grammar. Explicit scope and operator roles are part of the protocol, not stylistic conventions.

### Semantics
The semantics define how a parsed chain evaluates. This includes operator behavior, typing behavior, outcome classes, and the treatment of unresolved structure. Noe is designed to preserve distinctions that many systems blur, including the difference between belief and knowledge, between false and undefined, and between first-order claims and higher-order epistemic structure.

### Admitted context
Noe chains are not interpreted in a vacuum. They are evaluated relative to explicit admitted context. This context provides the bounded input surface against which literals, evidentiary claims, deixis, relations, and related structures are interpreted. The existence and semantic role of context are protocol-level. The derivation of that context from sensors, models, APIs, or other systems is implementation- and domain-specific.

### Morphology and bounded composition
Noe includes a constrained morphological layer. Morphological composition is not free-form or idiomatic; it is rule-bound and registry-compatible. This allows the protocol to gain expressive compression without collapsing into natural-language-like ambiguity. For readers coming from linguistics or conlang design: Noe is not merely a bag of tokens, but a deliberately bounded compositional system with explicit control over how meaning can be combined, modified, or scoped.

<br />

## Evaluation outcomes

Noe evaluation is typed. Important outcome classes include:

- Truth
- Action or list[action]
- Undefined
- Error

These are not interchangeable.

**Undefined is not false.** `undefined` means the protocol does not have enough admitted support to produce a defined value. It is not equivalent to false, and it must not be silently coerced into false.

**Undefined is not an exception.** `undefined` is a semantic outcome, not a crash. It is how the protocol represents unresolved, missing, or insufficiently grounded meaning within evaluation.

**Error is different from undefined.** `error` indicates contract rejection or structural failure under a stricter runtime or validation path. A stale required context, malformed structure, or invalid use of an operator may produce an error rather than a semantic undefined.

The exact runtime treatment of undefined and error may differ by implementation, but the protocol distinguishes them conceptually.

<br />

## Historical lineage and divergence

Noe inherits concerns from formal logic, symbolic knowledge representation, structured APIs, and semantic systems that attempted to make meaning explicit. It also responds to the limits of each: natural language is expressive but ambiguous, structured schemas are useful but semantically thin, formal systems are often inference-heavy or brittle, and latent-model communication is powerful but opaque.

Noe differs from ontologies, knowledge graphs, and semantic-web formalisms in several ways. It is chain-native rather than graph-native, evaluation-oriented rather than primarily storage-oriented, and explicitly designed for bounded interpretation under admitted context. It treats epistemic stance as a first-class part of the protocol, preserves undefined as a semantic outcome, and does not rely on implicit inference or open-world completion at the core layer. It is also designed for transport across heterogeneous modalities and runtimes, not just for static knowledge representation.

Noe is not trying to be a universal knowledge base or a semantic web replacement. Its center of gravity is narrower: canonical symbolic expression, explicit context dependence, deterministic parsing, replayable evaluation, and stable transport across multiple media.

<br />

## Protocol and implementations

These layers should be kept distinct:

- **Noe** is the protocol.
- **Noe Gate** is a runtime built on Noe.
- Adapters and integrations such as ROS2 layers are system-specific implementation layers.

The protocol defines symbolic structure and evaluation rules. Runtimes implement those rules. Adapters connect runtimes to concrete systems, transports, policies, sensors, storage layers, or application environments.

<br />

## When Noe is not the right tool

Noe is not the right tool for:

- hard real-time control loops
- low-level motion planning
- free-form conversational language
- unconstrained knowledge inference
- cases where ordinary typed interfaces already solve the problem adequately
- applications where deterministic parsing and explicit semantics do not matter

Its role is narrower: providing a stable symbolic layer where explicit, replayable meaning matters.

<br />

## Governance

Noe is open source under the Apache 2.0 license. The protocol is governed through a NIP (Noe Improvement Proposal) process. Each NIP defines a specific aspect of the protocol: grammar, semantics, morphology, scalar operators, context model, conformance, and so on. Changes to the protocol require a NIP. The current NIP series is the formal source of truth for all protocol behavior.

<br />

## Specification map

This overview is descriptive. The formal source of truth lives in the protocol specifications and supporting artifacts, including:

- Core grammar
- Core semantics
- Core morphology
- Glyph registry
- Context model and safe projection
- Quantitative and numeric logic
- Scalar and intensity operators
- Explained literals and grounding
- Deixis semantics
- Delivery semantics
- Audit semantics
- Reference interpreter and conformance

Readers who need exact operator behavior, parsing rules, context requirements, or conformance details should follow the spec documents rather than relying only on this overview.

<br />

## Current scope

Noe currently aims to provide:

- Deterministic symbolic representation
- Bounded meaning under explicit context
- Stable parsing across conforming implementations
- Replayable evaluation outcomes
- A modality-independent canonical layer for semantic interchange

Noe does not currently attempt to provide:

- Open-ended natural language replacement
- General planning
- Perception
- Control
- Unrestricted inference
- Complete world modeling

Its strength is narrowness. Noe is most appropriate where explicit structure, bounded context, deterministic interpretation, and replayability matter more than maximal expressive freedom.
