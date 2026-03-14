---
layout: post
title: "Critical Flaw in How We Detect Exoplanets"
date: 2026-01-28
categories: [project, research, space, algorithms]
---

## When Everyone Agrees, But Everyone Is Wrong

What if NASA's most trusted method for confirming exoplanets—getting multiple independent detectors to agree—might be fundamentally broken?

I'm a high school student, and I just spent the last few months building a simulation that proves it. Here's what I found: **five independent detection systems can achieve perfect consensus while being completely, confidently wrong.**

This isn't theoretical. This is a real failure mode that could affect every multi-detector space mission currently operating.

---

## The Problem Nobody Talked About

When NASA discovers an exoplanet, they don't trust a single detector. They use multiple independent systems to confirm the finding. The logic seems bulletproof:

> "If 5 independent detectors all say they found a planet with a 7-day orbit, it's probably real, right?"

**Wrong.**

What if all 5 detectors are on the same spacecraft? What if they're all experiencing the same environmental stress — thermal drift, radiation hits, detector degradation?

**They'll all see the same distorted signal. They'll all agree. And they'll all be wrong.**

I call this **false consensus**, and I've proven it exists.

---

## What I Built

A complete Python simulation framework (1,100+ lines) that:

1. Generates realistic exoplanet transit signals
2. Applies four types of deep-space environmental corruption: thermal drift, radiation noise, signal attenuation, and timing jitter
3. Simulates 5 independent virtual detectors — each with its own noise, but all seeing the same corrupted signal
4. Runs Box Least Squares period-finding detection
5. Measures consensus vs. accuracy — do they agree? Are they right?

I tested 20 different stress levels, from perfectly clean to severely corrupted.

---

## The Results Are Alarming

At moderate environmental stress (stress level 0.2):

```
True orbital period: 5.0 days
Detector 1 found: 7.0 days
Detector 2 found: 7.0 days
Detector 3 found: 7.0 days
Detector 4 found: 7.0 days
Detector 5 found: 7.0 days

Agreement: PERFECT (std = 0.000 days)
Confidence: HIGH (detection power = 6.0)
Error: 40%
```

All five detectors agreed. All five were wrong by 40%. All five were highly confident.

This would pass peer review. NASA would announce it. Telescope time would be scheduled. But the planet isn't where they think it is.

---

## The Danger Zone Isn't Where You Think

Most mission planners worry about extreme conditions. But peak error occurs at **moderate stress**, not extreme. The error curve is U-shaped:

- Stress 0.0 (clean): 0.005 day error ✓  
- Stress 0.2 (moderate): 2.0 day error ✗ ← **PEAK DANGER**  
- Stress 0.5 (medium-high): 0.015 day error ✓  
- Stress 1.0 (extreme): 1.6 day error ✗  

At moderate stress, thermal drift creates a clean, regular false signal at exactly 7 days. This artifact is *more* regular and *more* detectable than the degraded true 5-day signal. All five detectors lock onto the same beautiful, wrong pattern.

At extreme stress, everything is chaos. At moderate stress, they converge.

---

## Why This Matters for Real Missions

This affects every mission with multiple detectors on a single platform:

- **Kepler** — 42 CCDs on one spacecraft, all sharing the same thermal environment
- **TESS** — 4 cameras, currently operational, uses multi-detector consensus for validation
- **JWST** — multiple instruments, shared thermal control, $10 billion mission
- **Roman Space Telescope** — could incorporate protections now, before launch

Current validation assumes: *N detectors agree → confidence scales with √N → reliable.*

My simulation shows: *N detectors with shared corruption → all see the same artifact → false confidence.*

Five detectors seeing the same corrupted signal provide no more information than one. But we treat it as 5× the evidence.

---

## The Code Is Public

Everything is on GitHub: [False-Exoplanet-Detection](https://github.com/advaithmj/False-Exoplanet-Detection)

Run it yourself. Test your own scenarios. Prove me wrong.

Full research paper: [Google Docs](https://docs.google.com/document/d/1hy9v8_LadEMlZ2T_PxcsmGIhGHYbpyKcHZCiOhi9bHo/edit?usp=sharing)

---

## Why I'm Sharing This

I'm not a professional astronomer. I don't have a PhD.

But I found something real — because I asked a question nobody was asking: *what if everyone agrees but everyone is wrong?*

The simulation took months. I learned Python from scratch. I read dozens of papers. I debugged until 2 AM more times than I can count.

This isn't about being smart. It's about asking uncomfortable questions.

If you're a researcher: test my findings. I might be wrong — prove it.  
If you're at NASA or a university: run my code on your mission parameters.  
If you're a student: don't wait for permission to do real science.
