# Conduit

**A Computational Engineering Model for the Piping Discipline**

*Founding Document — v0.2*

---

## 1. Vision

Conduit encodes the deterministic and heuristic layers of pipe stress engineering as a coherent algorithmic framework. Given a bounded, structured input — a defined system with connection points, process conditions, and a spatial envelope — Conduit produces a stress-validated, supported layout.

The inspiration is [LEAP 71's Noyron](https://leap71.com/Noyron/) — a Large Computational Engineering Model for rocket propulsion that encodes domain physics, manufacturing rules, and engineering heuristics in a coherent framework. Noyron is not machine learning. It is explicit, deterministic algorithmic logic written by domain experts. The thesis: engineering expertise is largely a collection of physics, heuristics, design rules, manufacturing constraints, and judgement calls — most of which can, in principle, be written down as code. Do that work, and you get a system that turns abstract inputs into manufacturable, validated designs in minutes rather than months.

Conduit applies the same thesis to industrial piping. Distilled expert knowledge, encoded as code, validated against physics.

Caesar II acts as the physics oracle in the feedback loop — at least initially. As Conduit matures and its own stress predictions are validated, this dependency may reduce.

---

## 2. Scope

The Noyron analogy is useful but it breaks in specific places. The honest scope must reflect that.

### 2.1 In scope

**Physics and code logic** — allowable stress calculations per B31.3 (and eventually other codes), nozzle load assessment against WRC 297/537 or vendor allowables, flange leakage criteria, displacement and reaction limits. Standards-based, deterministic.

**Component and configuration logic** — support type selection (rest, guide, anchor, spring, snubber), support placement reasoning, expansion provision via loops, bellows, or offsets, flexibility analysis heuristics. Rule-based with judgement encoded.

### 2.2 Out of scope

**System-level interactions across a plant.** Conduit handles individual systems, not the interaction of thousands of interconnected lines with equipment, structures, and other disciplines. That layer is not encodable in the Noyron sense — no individual engineer holds it in their head.

**Project context.** Client specifications, jurisdictional amendments, company standards, vendor requirements, project philosophies — the unstructured layer of real projects. Conduit assumes a clean input. Assembling that input remains human work.

**Non-stress constraints on routing.** Access, maintenance, constructability, operability, aesthetic and plant philosophy decisions. Conduit can satisfy stress and spatial constraints; it cannot decide whether a route is sensible from a plant operations perspective.

**Cross-discipline coordination.** Civil, structural, instrumentation, electrical, process — Conduit lives inside the piping discipline.

### 2.3 Where the Noyron analogy holds, and where it breaks

| Dimension | Noyron (rockets) | Conduit (piping) |
|---|---|---|
| Problem domain | Bounded — one engine | Vast — interconnected plant systems |
| Inputs | Clean engineering parameters | Messy, unstructured, project-specific |
| Output | Self-contained object | Interconnected with adjacent systems |
| Standards | Largely physics-driven | Physics plus project, client, jurisdictional layers |
| Validation | Tight internal coupling | External commercial tool via file interface |

Conduit is not "Noyron for piping" in the marketing sense. It is not "generate a refinery." It is a smaller, achievable thing that is still genuinely valuable, because most stress engineering hours are spent in exactly the bounded layers Conduit targets.

---

## 3. Optimisation targets

Conduit's feedback loop iterates against the following criteria:

- **Pipe stresses** — sustained, occasional, expansion, per applicable code
- **Nozzle loads** — against WRC 297/537 or vendor-specified allowables
- **Flange leakage** — per NC-3658.3 or equivalent
- **Displacements and reactions** — within tolerances of supports, equipment, and structure
- **Support utilisation** — spring travel, rod angle, gap maintenance

Additional targets may be added as the system matures.

---

## 4. Build sequence

### Stage 1 — Support optimisation (MVP)

Given a predetermined piping layout in Caesar II neutral file format, Conduit suggests optimal support positions and types, writes them back to the neutral file, triggers Caesar II analysis, and iterates until all optimisation targets are satisfied.

- **Input:** Caesar II neutral file (`.c2`)
- **Logic:** encoded span rules, support type heuristics, load path reasoning
- **Feedback loop:** Caesar II stress and nozzle load reports
- **Output:** modified neutral file with supports placed and stresses passing

### Stage 2 — Routing automation

Given two or more connection points and spatial constraints, Conduit generates a pipe route that satisfies stress, nozzle load, and flange leakage requirements — with supports placed automatically. Layout heuristics encode the routing logic a stress engineer would apply manually.

### Stage 3 — Full system generation

Given process data, equipment specifications, and spatial boundary conditions, Conduit generates a complete piping and equipment layout for a defined system — routing, supports, and stress validation included.

Note: "full system" here means a bounded engineering system, not a full plant. The plant-level layer remains out of scope.

---

## 5. Technical foundation

- **Language:** C#
- **Environment:** Visual Studio Community
- **Interface to Caesar II:** neutral file (read, modify, write)

---

## 6. IP considerations

Conduit must be built as a clean-room implementation. No proprietary project files, employer data, or work-time development may be used.

---

## 7. Open questions

- First external user — consultant contact not yet approached
- Synthetic or public dataset for validation without proprietary files
- Caesar II licence access for development and testing

---

## 8. Status

- Hello World in C# — committed to GitHub ✓
- Caesar II neutral file parser in C# — in progress
- Node list extraction — next concrete milestone

---

*Conduit — Founding Document v0.2 — Adrian*