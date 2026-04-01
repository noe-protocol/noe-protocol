# AGENTS.md — noe-protocol

> This file is for AI coding assistants (Claude Code, Copilot, Cursor, etc.).
> It describes the constraints you must respect when working in this repository.
> This is a specification repository, not an implementation. The rules here
> protect the normative integrity of the protocol.

---

## Global safety invariant

**Undefined chains never produce actions.**

This is the foundational safety property of the entire Noe protocol. If
evaluation cannot determine truth, the result is Undefined and the proposed
action is NOT executed. This invariant must never be violated — not in
specification text, not in examples, not in operator definitions, not in
any edit to any file in this repository.

Concretely:
- `kra` with a non-True guard returns Undefined, not the action.
- `mek` requires a True guard to execute. Undefined guard = no execution.
- `nai Undefined = Undefined` (not True — negating uncertainty does not
  produce certainty).
- Missing context literals resolve to Undefined, never False.

Any change that would allow an action to execute under Undefined evaluation
violates this invariant and must be rejected.

---

## The single most important rule

**Do not paraphrase, "clarify," or "improve" normative language.**

The NIP documents and README use specific, deliberate language. Every word in
a normative statement — operator names, evaluation rules, domain names, type
signatures — was chosen precisely. If something reads awkwardly, that is
intentional. Protocol specifications are not prose to be polished. They are
contracts to be preserved.

**If a requested change would modify normative language without a NIP
reference, you must refuse to perform the change.** Do not comply and hedge.
Do not rewrite and add a comment. Do not suggest improvements inline. Refuse,
explain why, and ask the human to provide a NIP reference or confirm the
change is intentional.

**"Flag" means:** do not modify any file. Instead, respond with an explanation
of the issue, quote the exact text in question, and ask the human how to
proceed. Every use of "flag" in this document means this — no exceptions.

---

## Normative vs non-normative text

Not all text in this repository carries the same weight. You must know
the difference.

**Normative** — text that defines protocol behavior. Changes to normative
text change what the protocol IS. Normative text includes:
- Operator evaluation rules (what `an`, `ur`, `nai`, `shi`, etc. produce
  for given inputs)
- Type signatures and domain definitions
- Context model structure (C.literals, C.modal, C.temporal, etc.)
- Grammar production rules
- Truth tables and K3 semantics
- Registry entries (phonetic, domain, type_sig, conflicts_with)
- Any sentence containing "MUST", "MUST NOT", "SHALL", "SHALL NOT"

**Non-normative** — text that explains, motivates, or illustrates. Changes
to non-normative text do not change protocol behavior, but can still mislead
if done carelessly. Non-normative text includes:
- Rationale paragraphs ("The reason for this choice is...")
- Commentary and design notes
- Section introductions and overviews
- English glosses in the registry (`semantic` field)

**Examples are normative-adjacent.** They are not definitions, but they are
semantically binding — an example that contradicts a normative rule creates
an internal inconsistency in the specification. Treat examples with the same
care as normative text. Do not add, modify, or remove examples unless
explicitly requested, and verify that any example is consistent with K3
evaluation semantics before including it.

---

## What this repository is

noe-protocol is the specification home for the Noe protocol — a deterministic
symbolic protocol for representing bounded meaning across agents, runtimes,
and modalities. It contains (or will contain) the NIP (Noe Improvement
Proposal) documents, the glyph registry specification, and the protocol's
governing README.

The reference implementation lives in a separate repository (noe-gate).
This repository defines what the protocol IS. noe-gate defines how it RUNS.

---

## Glyph constraints

### One glyph, one meaning

Every glyph in the Noe protocol has exactly one phonetic form, one semantic
role, and one evaluation behavior. There are no synonyms. There are no
contextual reinterpretations. The `conflicts_with` field in the registry
exists specifically to prevent semantic overlap.

**Rules:**
- Never introduce a new glyph without a NIP.
- Never change the phonetic form of an existing glyph.
- Never add "aliases" or "shorthand" for existing glyphs.
- Never merge two glyphs into one or split one glyph into two.

### English glosses are display-only

The `semantic` field in registry entries (e.g., `"semantic": "Knowledge"` for
`shi`) is a human-readable hint. It is NOT the definition. The definition is
the evaluation behavior specified in the relevant NIP and implemented in
noe-gate.

**Rules:**
- Do not treat glosses as authoritative definitions.
- Do not change glosses to "better" English words.
- Do not derive implementation behavior from glosses.
- If a gloss says "Knowledge" and the NIP says "checks C.modal.knowledge for
  literal membership," the NIP wins. Always.

### The registry is frozen at V1.0.0

The current registry version is `1.0.0` with status `Canonical`. Changes to
the registry require a NIP and a version bump. Do not modify registry entries
without understanding the downstream impact on:
- The PEG grammar (which matches phonetic tokens)
- The evaluation engine (which dispatches on operator identity)
- The conformance test suite (which locks expected outputs)
- The Rust implementation (which must maintain parity)

---

## Operators you must know

These are the operators most likely to cause confusion:

| Phonetic | Role | Common mistake |
|----------|------|----------------|
| `an` | Conjunction (AND) | Confusing with `kel` (which is NOT conjunction) |
| `ur` | Disjunction (OR) | Confusing with `dom` (which is NOT disjunction) |
| `nai` | Negation | Assuming `nai Undefined = True` (it's Undefined) |
| `shi` | Epistemic knowledge | Assuming it's a truth-value operator (it gates on context) |
| `sek` | Scope delimiter | Assuming it's invisible (it wraps results in a structural list) |
| `kra` | Guard | Assuming False guard returns False (it returns Undefined) |
| `mek` | Action execution | Assuming it always executes (it requires True guard) |

The evaluation semantics are K3 Strong Kleene, not classical boolean logic.
The key difference: `False AND Undefined = False` and
`True OR Undefined = True`. Undefined does NOT universally propagate.

---

## Cross-file consistency

This repository may contain a README, NIP documents, and registry data.
These files must not contradict each other. Before making any change, verify
that it does not create inconsistencies across files.

Specifically:
- If a NIP defines operator behavior, the README must not describe different
  behavior for the same operator.
- If the registry defines a glyph's domain and type signature, NIP text must
  not imply a different domain or signature.
- If one NIP references a rule defined in another NIP, the reference must
  match the source exactly.

**If you discover an existing inconsistency between files, do not resolve it
yourself.** Flag it to the human with the specific conflicting passages.
Resolving cross-file inconsistencies requires judgment about which source is
authoritative, and that decision belongs to the protocol maintainer.

---

## NIP document structure

NIPs follow a specific structure. If editing or creating NIPs:

- **Do not invent new section headings.** Follow the established pattern.
- **Do not add implementation details.** NIPs specify behavior, not code.
- **Do not reference specific line numbers** in noe-gate. NIPs must be
  implementation-independent.
- **Use the protocol's own notation** (glyph phonetics, operator names) rather
  than mathematical symbols or programming language syntax when describing
  evaluation behavior.
- **Do not add examples unless explicitly requested.** Examples are
  normative-adjacent and must be verified against K3 semantics before
  inclusion. An incorrect example is worse than no example.

---

## What NOT to do

- **Do not "fix grammar" in NIP text.** What looks like awkward phrasing may
  be deliberate precision. Flag it to the human as a comment or note — do not
  change the text, suggest inline rewrites, or add annotations to the file.
- **Do not add examples that change semantics.** An example that implies
  `nai Undefined = True` would contradict K3 and mislead implementers.
- **Do not reorganize the README for "clarity."** The structure reflects the
  protocol's conceptual hierarchy. It is not a blog post.
- **Do not add operator definitions based on English intuition.** "Knowledge"
  does not mean what it means in English. It means "literal membership in
  C.modal.knowledge." Always defer to the formal definition.
- **Do not create implementation files.** This is a specification repository.
  Implementation belongs in noe-gate.
- **Do not merge `kel`/`dom` references as conjunction/disjunction.** The
  grammar's binary connectives are `an` (AND) and `ur` (OR). `kel` and `dom`
  are separate registry entries with different roles.
- **Do not resolve ambiguities by guessing.** If the spec is unclear about
  whether a rule applies, flag it. Do not pick the interpretation that "makes
  more sense" and silently encode it.
- **Do not perform partial edits that depend on a refused normative change.**
  If a request involves both normative and non-normative changes, and you must
  refuse the normative part, do not apply the non-normative part if it only
  makes sense in the context of the refused change. Either the full edit is
  valid or none of it is.

---

## Pre-edit invariant check

Before completing any edit to any file in this repository, verify:

1. **Safety invariant:** Does this change introduce any path where Undefined
   evaluation could result in action execution? If yes, reject the change.
2. **Cross-file consistency:** Does this change contradict anything in other
   files (README, NIPs, registry)? If yes, flag the contradiction.
3. **Normative integrity:** Does this change alter normative text? If yes,
   is there a NIP reference? If no, refuse.

This is not optional. Treat it as a checklist that runs on every edit.

---

## Governance

Changes to the protocol require a NIP. This includes:
- New glyphs or operators
- Changes to evaluation semantics
- Changes to the registry
- New domain types
- Changes to the context model

The NIP process exists to ensure that every change is deliberate, reviewed,
and traceable. An AI assistant should never make protocol-level changes without
explicit human instruction and a NIP reference.

**Hard rule:** If asked to make a change and no NIP is referenced, ask for
one. If told to proceed without a NIP, you may comply for non-normative text
only. For normative text, refuse and explain that normative changes require
a NIP.
