# Apicus Layer 2 — Transformation Ontology

A formal OWL ontology modeling **culinary transformations** — the actions a cook performs on a substance to change its structure, composition, texture, flavor, or microbial state. Designed for multi-cuisine extensibility, with practitioner-verification, cultural lineage, and adaptation under equipment constraint as first-class concerns.

This is one layer (Layer 2) of a larger ongoing project — **Apicus AI** — that aims to model culinary intelligence end-to-end: substance (Layer 1), transformation (Layer 2, this repo), composition (Layer 3), sensory outcomes (Layer 4), and cultural/contextual reasoning (Layer 5).

---

## What this is

A culinary transformation in this schema is a structured entity carrying:

- **Multi-family classification** — thermal, mechanical, chemical, biological — as multi-valued tags rather than rigid subclasses. A single transformation can belong to multiple families (e.g., miso enzymatic action is both Chemical and Biological).
- **Provenance wrapper** — every instance declares its practitioner of record, review status, source document, and confidence level. Nothing anonymous.
- **Cultural lineage** — named traditions a technique descends from or with which it is associated.
- **Adaptation as a first-class entity** — explicit modeling of equipment-constrained substitutions that preserve cultural identity. When a clay-pit tandoor becomes a hotel-pan double-sealed braise, the substitution is structured data, not a footnote.
- **Personal opinion as attributed data** — practitioner stances with full attribution, not flattened into facts.
- **Declared gaps** — explicit acknowledgment of techniques the practitioner does not perform. The system knows what it does not know.

---

## Repository contents

| File | Purpose |
|------|---------|
| `docs/ontology/layer2_transformation.owl` | OWL/RDF schema (~460 lines), Protégé-ready |
| `docs/ontology/layer2_transformation.md` | Human-readable documentation of every class, property, and design decision |
| `ABOUT.md` | Project context and practitioner background |
| `LICENSE` | CC BY 4.0 |

The OWL file includes **five fully-populated example instances** drawn from working kitchen practice: a fermented hummus (chemical + biological), a hotel-pan tandoor-substitute braise (thermal, with full adaptation linkage), the original clay-pit tandoor as a declared gap, the adaptation entity itself, and whole-lamb carcass butchering with `generalizesTo` cascade. These anchor instances demonstrate the schema can host real practitioner content with full provenance.

---

## What is **not** in this repository

This is a single layer of a larger system, deliberately scoped for public release. The following are kept private at this stage:

- Layers 1, 3, 4, 5 (substance, composition, sensory, cultural — under active development)
- The Apicus AI agent pipeline and fine-tuned culinary pairing model
- The Neo4j runtime instance and ~5,000-ingredient classified graph
- The Boochmania catalog, recipe corpus, and business-side data

This repository exists to share the formal ontology schema with the BMIR / ontology community for inspection, critique, and potential adaptation.

---

## Design principles

1. **Just rich enough.** Every slot in the schema is justified by something documented in practitioner contribution. No speculative slots.
2. **Multi-family allowed.** Family is a multi-valued tag. Real cooking transformations cross categorical boundaries.
3. **Provenance is mandatory, not optional.** Every Transformation instance must declare its practitioner of record, review status, and source.
4. **Adaptation is first-class.** When equipment forces a workaround, the substitution becomes a structured entity with quality compromises and gains explicit.
5. **Cultural lineage is a property, not a separate layer.** Traditions touch transformations directly. No artificial separation between technique and origin.
6. **Practitioner verification over textbook abstraction.** The review status taxonomy (`Practiced` / `Scaffolded` / `DeclaredGap` / `Theoretical` / `Unreviewed`) distinguishes firsthand knowledge from secondhand. The ontology gains integrity from honest scope, not heroic length.

---

## How to use this

Open `docs/ontology/layer2_transformation.owl` in [Protégé](https://protege.stanford.edu/) (v5.5 or later). The class hierarchy and property panel populate immediately. Five named individuals appear under their respective classes for inspection.

Run the bundled HermiT reasoner to verify logical consistency. The companion markdown documentation walks through each class with rationale and example mappings to working kitchen practice.

---

## Status

- **Version:** 0.1.0 (initial public release)
- **Practitioner of record (anchor instance set):** Numan Karabıyık, Boochmania (San Francisco, CA)
- **Last updated:** 2026-06-15

This is an active ontology. The schema is expected to evolve as additional practitioners contribute and as adjacent layers (Substance, Composition, Sensory, Cultural) come online.

---

## License

Released under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You may use, adapt, and distribute the schema and documentation for any purpose, including commercial, provided you give appropriate credit and indicate any changes.

This is the licensing convention used by Gene Ontology, FoodOn, ChEBI, and other major open biomedical and scientific ontologies.

---

## Citation

If you reference this work in academic, applied, or commercial settings:

> Karabıyık, N. (2026). *Apicus Layer 2: Transformation Ontology* (Version 0.1.0). Apicus AI. https://github.com/athenaeusnaucratis/apicus-ontology 


---

## Contact

**Numan Karabıyık**
Co-founder & Chef — Boochmania / Boochman Kombucha
San Francisco, California
[info@boochmania.com](mailto:info@boochmania.com)

For collaboration inquiries, schema critique, or practitioner contributions to future versions, please open an issue on this repository or reach out by email.
