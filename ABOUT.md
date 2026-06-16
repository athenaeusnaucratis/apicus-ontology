# About Apicus AI

## The project

**Apicus AI** is a modular agentic culinary assistant and catering management system being built around a knowledge-graph backbone. Its purpose is to model the *mind of a chef* in software: knowledge of substances, transformations, equipment, composition grammars, sensory outcomes, and cultural context — and the reasoning that combines them.

Apicus AI is anchored in the operations of a working Levantine/Mediterranean bistro & catering business in San Francisco, California, but its architecture is designed from the start for multi-cuisine extensibility. The Levantine instance set is the first; it is not the boundary.

## What's built (as of the publication of this ontology)

| Component | Status |
|-----------|--------|
| Neo4j knowledge graph | ~5,000 classified ingredients, 477 indexed recipes, 7 documented dish grammars (Levantine corpus) |
| 20-role culinary ingredient taxonomy | corrected and applied to the graph; covers role distinctions like `legume`, `paste_condiment`, `liquid_base`, `wrap_bread`, `grain_starch` (rather than collapsing these into `protein` or `starch`) |
| Fine-tuned culinary pairing model | QLoRA adapter on Phi-3.5-mini, trained on ~2,200 prediction-task examples from clean graph data |
| Agent pipeline | inquiry parser, catalog matcher, chef agent, sales agent, response synthesizer, knowledge agent — all reading from the graph |
| OWL ontology (this repository) | Layer 2 (Transformation) — v0.1.0 |

## What this ontology represents within the larger project

Apicus AI was initially built pragmatically: graph-first, agents wired up, working dishes flowing through the system. Mid-project, a realization emerged that without a formal ontological backbone, the system would scale into incoherence. Different cuisines would need different ad-hoc patches. The solution was to step back and formalize the schema — to define *what exists* in the system in a way that future cuisines, contributors, and reasoning agents can navigate consistently.

The Layer 2 work published here is the first formal artifact of that effort.

## Practitioner background

**Numan Karabıyık** is a trained chef (Culinary Arts, 2013) and co-founder of Boochmania / Boochman Kombucha, a Levantine/Mediterranean bistro with a fermentation specialty in SoMa, San Francisco, California. He maintains a personal library of 2,500+ cookbooks and brings a decade of professional kitchen experience to the project's anchor instance set.

He came to ontology engineering through necessity, without prior background in IT or linguistics. The schema published here was built alongside study of:

- Aristotle's *Categories* (the foundational text for Western ontology)
- The canonical Gruber definition of ontology as "explicit formal specification of a shared conceptualization"
- The Manchester Pizza Tutorial (Protégé/OWL teaching corpus)
- Linked Data Engineering and Knowledge Engineering with Semantic Web (open lecture series)
- Sandor Katz, René Redzepi (fermentation reference); Harold McGee (food science)
- Lacan's theory of the symbolic order as a structural-relational analog for how meaning emerges in ontologies

This combination — practitioner-led, philosophically grounded, self-schooled in the formal apparatus — is unusual for ontology work, which is typically led from inside academic or research institutions. The intent of this public release is to invite that community's critique and collaboration.

## Future layers

| Layer | Subject | Status |
|-------|---------|--------|
| Layer 1 | Substance (ingredients, properties, sourcing) | Active development; partial reuse of FoodOn planned |
| Layer 2 | Transformation (cooking actions) | **Published here, v0.1.0** |
| Layer 2.5 | Equipment (tools, capability ranges, kitchen profiles) | Drafted; OWL extraction underway |
| Layer 3 | Composition (dish grammars, slot logic, balance axes) | Informal in graph; formal schema pending |
| Layer 4 | Sensory (flavor pairings, mouthfeel, aroma, balance) | Informal in graph; formal schema pending |
| Layer 5 | Cultural & contextual (cuisine, occasion, format, lineage) | Informal in graph; formal schema pending |

Each layer will be published as it matures.

## Why this is public

Because the framing principle of the project — *that what exists is what can be represented* — cuts both ways. Locked ontologies serve no community. Released schemas can be inspected, adapted, contested, and improved. The intent is to make the Layer 2 schema useful to anyone working on culinary, gastronomic, food-science, or fermentation ontologies — and to make any reuse, attribution, or constructive critique welcome.

## Contact

**Numan Karabıyık**
Boochmania / Boochman Kombucha -
San Francisco, CA
[info@boochmania.com](mailto:info@boochmania.com)
