# Apicus Layer 2 — Transformation Ontology

**Version:** 0.1.0 (initial schema)
**Created:** 2026-06-05
**Practitioner of record (anchor):** Numan / Boochmania
**OWL file:** `layer2_transformation.owl`
**Runtime target:** Neo4j (via separate migration script)

---

## What this layer does

Layer 2 formalizes **culinary transformations** — every action a cook performs that changes a substance. Roasting, fermenting, knife-cutting, emulsifying, marinating — all become structured Transformation instances in a shared schema.

The schema is **multi-cuisine extensible**: the structural model is universal; the content that fills it is plural. Boochmania is the first anchor instance set; future practitioners and cuisines populate the same structure without changing it.

## Design principles

1. **Just rich enough** — every slot is justified by something documented in a practitioner's contribution. No speculative slots.
2. **Multi-family allowed** — Family is a multi-valued tag, not a strict class hierarchy. A transformation can be Chemical *and* Biological (miso enzymatic action), or Thermal *and* Mechanical (sear-then-press).
3. **Provenance is mandatory** — every Transformation declares its practitioner-of-record, review status, and source. Nothing anonymous.
4. **Adaptation is first-class** — when equipment forces a workaround, the substitution is its own structured entity, not a footnote.
5. **Cultural lineage is a property, not a layer** — traditions touch transformations directly. No separate "cultural ontology" needed.

---

## Class hierarchy

```
Transformation
├── (has) Family       — Thermal | Mechanical | Chemical | Biological
├── (has) ProcessStep  — ordered actions
├── (has) Parameter    — typed quantitative ranges
│            ├── TemperatureRange
│            ├── TimeRange
│            ├── SaltPercentage
│            ├── PHRange
│            └── Ratio
├── (uses) Equipment
├── (has) CulturalTradition
├── (has) PersonalOpinion
├── (required) Practitioner            ← practitioner-of-record
├── (required) ReviewStatus            ← Practiced | Scaffolded | DeclaredGap | Theoretical | Unreviewed
├── (required) Provenance              ← wrapper
└── (linked) Adaptation                ← when substituted under constraint
              ├── isAdaptationOf       (original Transformation)
              ├── hasAvailableSubstitute (replacing Transformation)
              ├── qualityCompromise / qualityGain
              └── preservesCulturalRoot
```

11 classes total. Two main (Transformation, Adaptation) + nine supporting.

---

## The Transformation class — all 14 slots

| Slot | Type | Required? | Purpose |
|------|------|-----------|---------|
| `name` | string | yes | Identifier |
| `hasFamily` | 1..* Family | yes | Multi-family classification |
| `hasProcessStep` | 1..* ProcessStep | yes | Ordered actions |
| `hasParameter` | 0..* Parameter | encouraged | Typed ranges (temp, time, salt %, pH) |
| `usesEquipment` | 0..* Equipment | encouraged | Tools used |
| `causalMechanism` | string (prose) | encouraged | The "why does this work" |
| `qualityTarget` | string (prose) | yes | What successful execution looks like |
| `failureMode` | 0..* string | encouraged | Failure cases and detection |
| `hasCulturalLineage` | 0..* CulturalTradition | encouraged | Named traditions |
| `hasPersonalOpinion` | 0..* PersonalOpinion | optional | Attributed practitioner stances |
| `generalizesTo` | 0..* string | optional | Where the output applies elsewhere |
| `hasPractitionerOfRecord` | 1 Practitioner | yes (wrapper) | Who documented this |
| `hasReviewStatus` | 1 enum | yes (wrapper) | Epistemological status |
| `hasProvenance` | 1 Provenance | yes (wrapper) | Source document + date + confidence |

**Six required, eight encouraged-or-optional.** That's the honest minimum.

---

## The four Families (controlled vocabulary)

| Family | Definition | Example transformations |
|--------|-----------|------------------------|
| **Thermal** | Applying or removing heat to change a substance | roast, braise, sear, smoke, poach, reduce, freeze |
| **Mechanical** | Physical form change without primary heat or chemistry | chop, grind, knead, emulsify, press, strain, butcher |
| **Chemical** | Substance interaction changing molecular structure | marinate, brine, cure, pickle-vinegar, gel, denature |
| **Biological** | Microbial or enzymatic action over time | lacto-ferment, acetic-ferment, mold-ferment, age, sprout, malt |

A transformation can belong to multiple families. Use `hasFamily` multiple times.

---

## The five ReviewStatus values

| Status | Meaning |
|--------|---------|
| **Practiced** | Actively performed by the practitioner-of-record. Trustworthy. |
| **Scaffolded** | Named with intent to deepen later. Honest placeholder. |
| **DeclaredGap** | Deliberately excluded with reason. Not practiced. The system knows what it doesn't know. |
| **Theoretical** | Known from literature but not personally practiced. Carries less weight than Practiced. |
| **Unreviewed** | Default state before any review. Should never persist. |

The **Scaffolded** and **DeclaredGap** statuses are what make this ontology different from textbook-derived ones. Honest scope > heroic length.

---

## Example mappings — Numan's content as instances

The OWL file ships with three real example instances + one adaptation, drawn from your documents. They prove the schema can host actual practitioner content.

### Example 1 — Fermented Hummus (`c'm.on.txt`)

- **Families:** Chemical + Biological (miso enzymes acting on chickpea substrate)
- **Equipment:** Robocoup
- **Parameter:** 5-7 days cold rest
- **Cultural lineage:** Levantine hummus + Japanese miso (as enzymatic agent)
- **Causal mechanism:** "Enzymes and yeast from miso convert chickpea starches into simple sugars and break proteins into amino acids → umami + slight sweetness"
- **Status:** Practiced

### Example 2 — Hotel-Pan Tandoor Braise (`kitch.on.txt`)

- **Family:** Thermal
- **Equipment:** Turbofan oven, griddle, 2 hotel pans + foil
- **Parameters:** 280F, 5 hours
- **Cultural lineage:** Kuyu Kebabi + broader Tandoor traditions
- **Causal mechanism:** Sealed pan replicates pit-chamber principle; carcass cooks in own juices
- **Personal opinion:** Carcass > pre-cuts (3 reasons documented)
- **Failure modes:** Pre-cut moisture loss; incomplete foil seal
- **Status:** Practiced
- **Adaptation link →** `Adapt_TandoorToHotelPan`

### Example 3 — Original Clay-Pit Tandoor (declared gap)

- **Family:** Thermal
- **Cultural lineage:** Kuyu Kebabi + Tandoor traditions
- **Status:** DeclaredGap (Numan does not have a clay tandoor)
- **Purpose:** Documents the cultural origin to which the adaptation refers

### Example 4 — Tandoor → Hotel-Pan Adaptation

- **isAdaptationOf:** Original Clay-Pit Tandoor
- **availableSubstitute:** Hotel-Pan Tandoor Braise
- **qualityCompromise:** Less aromatic complexity (no ember smoke)
- **qualityGain:** Reproducible exact temperature control
- **preservesCulturalRoot:** Yes → Kuyu Kebabi + Tandoor

This adaptation pattern is **what no cookbook models**. Future contributors can document their own adaptations under different constraints.

### Example 5 — Whole Lamb Butchering (`mek.on.txt`)

- **Family:** Mechanical
- **Quality target:** Minimal cut surface area (preserves moisture for braise)
- **Personal opinion:** Carcass > cuts (same as Example 2)
- **generalizesTo:** Rack, chops, loin/tenderloin, kofte grind substrate
- **Status:** Practiced

The `generalizesTo` slot does real work here — one butchering act yields multiple downstream substrates.

---

## How to open this in Protégé

1. Launch Protégé (already installed).
2. **File → Open** → navigate to `docs/ontology/layer2_transformation.owl` (or use the WSL-mounted path).
3. The class hierarchy appears in the **Classes** tab. You should see:
   - `Transformation` (with the example instances under it)
   - `Adaptation`
   - `Family` (with 4 named individuals — Thermal, Mechanical, Chemical, Biological)
   - `ProcessStep`
   - `Parameter` (with 5 subclasses)
   - `Equipment`, `CulturalTradition`, `PersonalOpinion`, `Practitioner`, `ReviewStatus`, `Provenance`
4. Switch to the **Individuals** tab to see populated examples.
5. **Reasoner → Start reasoner** (HermiT is included) — verifies the ontology is logically consistent. Should pass cleanly.

### First navigation suggestion

In Protégé:
- Click `Tx_HotelPanTandoorBraise` in the Individuals tab.
- See all its properties populated — equipment, parameters, lineage, causal mechanism, the adaptation link.
- Click `Adapt_TandoorToHotelPan` — see how the adaptation references the original technique and the substitute.
- This is the schema *in action*. Future contributions follow the same pattern.

---

## Mapping to Neo4j (runtime alignment)

The OWL ontology defines the **schema**. Neo4j holds the **instances** at runtime.

Each OWL class becomes a Neo4j node label:
- `Transformation`, `Adaptation`, `Family`, `ProcessStep`, `Parameter`, `Equipment`, `CulturalTradition`, `PersonalOpinion`, `Practitioner`, `ReviewStatus`, `Provenance`

Each OWL ObjectProperty becomes a Neo4j relationship type:
- `HAS_FAMILY`, `HAS_PROCESS_STEP`, `HAS_PARAMETER`, `USES_EQUIPMENT`, `HAS_CULTURAL_LINEAGE`, etc.

Each OWL DatatypeProperty becomes a Neo4j node property:
- `name`, `causalMechanism`, `qualityTarget`, `unit`, etc.

A migration script (`scripts/sync_ontology_to_neo4j.py`, to be written next) will:
1. Parse this OWL file
2. Create Neo4j uniqueness constraints on class identifiers
3. Create node labels and relationship types
4. Migrate example instances as starter data
5. Re-run whenever the ontology changes — keeps schema and runtime aligned

This way, **Protégé is the single source of truth for the schema; Neo4j is the runtime store; they never drift.**

---

## What this schema deliberately does NOT include (and why)

To avoid FoodOn-style over-engineering, several plausible-sounding slots were left out:

| Excluded | Why |
|----------|-----|
| Allergen/dietary inference | Belongs in Layer 4–5 (sensory/composition), not Layer 2 (transformation) |
| Time-of-day / season slots | Not in any current document; speculative |
| Cost computation | Dish-level concern (already on `CostTier`); transformations don't carry $ |
| Plating notes | Layer 3 (Composition) territory |
| Sensory output details | Layer 4 (Sensory) — connected via downstream link, not inline |
| Nutritional analysis | Out of scope; that's FoodOn territory |

If real use cases demand any of these later, they get added then. For now: clean.

---

## Next steps after this file

1. **You open it in Protégé.** Browse the class hierarchy, view the example instances, run the reasoner. See if anything feels off.
2. **First feedback pass.** What's missing, what's redundant, what doesn't capture how you actually think about transformations.
3. **Schema iteration.** We adjust the OWL file based on what you saw. Probably 1-2 iterations.
4. **Migration script.** Once schema feels right, I write `sync_ontology_to_neo4j.py` to materialize it in the runtime graph.
5. **Population pass.** Your remaining transformation entries (the scaffolded ones — marinating, Tsukemono, hydrocolloid details) get encoded as instances under the now-stable schema.
6. **Other Layers.** Layer 1 (Substance), Layer 3 (Composition), Layer 4 (Sensory), Layer 5 (Cultural) — each gets the same treatment. Layer 2 is the template for how to structure the rest.

---

## Honest limits of this version

- **Single anchor practitioner.** The schema is designed for plurality, but until other practitioners contribute, the cross-practitioner queries remain unexercised. Architecture ready, data thin.
- **No reasoner-enforced rules yet.** The cardinality constraints (1 hasPractitionerOfRecord, etc.) are declared but not yet aggressively enforced. We'll tighten in iteration 2.
- **Layer 2 only.** Other layers reference Equipment, KitchenProfile, Cuisine, Dish — those exist informally in Neo4j today but aren't formally specified here. Each gets its own OWL file in sequence.
- **OWL Full features unused.** This file is OWL DL clean. We could add SWRL rules later for inference (e.g., "every Adaptation with preservesCulturalRoot=true inherits the cultural lineage of its originalTechnique") but kept simple for v0.1.

---

*This document is itself ontology data. Treat it as canonical alongside the OWL file. Any change to the schema must be reflected in both.*
