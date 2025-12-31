---
marp: true
title: Software Architecture for Essential & Accidental Uncertainty
author: Neil Harrison · with George Rudolph & Peter Aldous
paginate: true
footer: "HICSS-59 Jan 2026 — Software Architecture for Essential & Accidental Uncertainty — "

# Global default background (applies to all slides unless overridden)
backgroundImage: url('images/main-bg.jpg')
backgroundSize: cover
backgroundPosition: center
backgroundColor: #ffffff

style: |
  :root { --uvu-green: #004b23; --uvu-green-2: #2d6a4f; --uvu-accent: #40916c; --text: #1a1a1a; }
  section { color: var(--text); }
  h1, h2, h3 { color: var(--uvu-green); }
  h1 { font-weight: 800; }
  h2 { font-weight: 700; text-align: center !important; }
  h3 { font-weight: 600; }
  p, li { font-size: 28px; line-height: 1.35; }
  table { font-size: 22px; border-collapse: collapse; }
  th { background: #e8f2ea; color: var(--uvu-green); font-weight: 700; }
  td, th { padding: 12px 16px; border-bottom: 1px solid #e5e5e5; }
  footer { 
    color: #e8e8e8; 
    background: linear-gradient(to bottom, 
      rgba(255, 255, 255, 0) 0%,
      rgba(255, 255, 255, 0.15) 15%,
      rgba(255, 255, 255, 0.5) 50%,
      rgba(255, 255, 255, 0.5) 50%,
      rgba(255, 255, 255, 0.15) 85%,
      rgba(255, 255, 255, 0) 100%);
    padding: 12px 15px;
    backdrop-filter: blur(2px);
    text-shadow: 0 1px 2px rgba(255, 255, 255, 0.8);
  }
  section::after { position: absolute; bottom: 20px; right: 30px; color: var(--text); font-size: 24px; }
  .two-column { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; align-items: center; }
  .two-column[style*="align-items: start"] { align-items: start; align-content: start; }
  .two-column[style*="align-items: start"] > div:first-child { padding-top: 0 !important; margin-top: 0 !important; align-self: start; }
  .two-column[style*="align-items: start"] > div:last-child { align-self: start; }
  .two-column p, .two-column li { font-size: 24px; line-height: 1.3; }
  .two-column strong { font-size: 25px; }
  .text-red { color: #d32f2f !important; }
  .text-green { color: #2d6a4f !important; }
  span.text-red { color: #d32f2f !important; }
  span.text-green { color: #2d6a4f !important; }
  .small-text {
    font-size: 20px !important;
    line-height: 1.3 !important;
  }
  .small-text li, .small-text p {
    font-size: 20px !important;
    line-height: 1.3 !important;
    margin-bottom: 6px;
  }

---

<!-- class: lead -->
<!-- _backgroundImage: url('images/title-bg.jpg') -->
# Software Architecture for Essential & Accidental Uncertainty

**Neil Harrison**, **George Rudolph** (presenter), **Peter Aldous**  
Utah Valley University
Orem, Utah

---

## The Challenge: From Deterministic to Uncertain

<div class="two-column">

<div>

**Early computing** (ENIAC, 1945-1955): Precisely specified problems with deterministic outputs

**Today**: Computing expanded to business, communication, control systems, and AI
- Inputs, outputs, and processes became more varied and less precise
- Modeling non-mathematical problems via mathematical abstractions

We must now deal with <span class="text-red">uncertainty</span> — and understand how to <span class="text-green">approach</span> it in architecture and design.

</div>

<div>

![width:100%](images/eniac.png)

</div>

</div>

---

## Current State of the Art

- (2010) **David Garlan** called for uncertainty to be a first‑class concern in software design and development.
- Current research and practice focus on **fault tolerance** and related tactics.
- **This misses a large part of uncertainty** and motivates a deeper investigation.

---

## Essence vs. Accident (Brooks, 1986)

<div class = "two-column">

<div style="flex: 1;">

**Accidental complexity**: created by engineering choices, mitigated by better tools and abstractions.  
**Essential complexity**: inherent in the problem — cannot be removed.  

Likewise, there is <span class="text-red">essential</span> and <span class="text-green">accidental</span> <span class="text-purple">uncertainty</span>.

</div>

<div style="text-align: left;">

<img src="images/brooks-1986.png" width = "350px">

</div>

</div>

---

## Essential and Accidental Uncertainty

- **Accidental uncertainty**: can be separated from the problem; *a transformation exists* to remove it.
- **Essential uncertainty**: must be addressed as part of the problem; *no transformation* can remove it.

**Computing is the processing of data.** Consider uncertainty across:
- **Input** (can be essential or accidental)
- **Transformation** from input to output (can be essential or accidental)
- **Output** (often essential)

---

## Uncertainty in the Transformation (Algorithms)

The **algorithm or processing logic** that transforms input to output can *introduce* uncertainty

<div class="small-text">
<div class="two-column">

  <div>
    <ul>
      <li><strong>Accidental</strong> → can be fixed
        <ul>
          <li>Hardware glitches</li>
          <li>Compiler differences</li>
          <li>Implementation bugs</li>
        </ul>
      </li>
      <li><strong>Essential</strong>
        <ul>
          <li>No deterministic algorithm exists</li>
          <li>Example: Image recognition</li>
        </ul>
      </li>
    </ul>
  </div>

  <div>
    <ul>
      <li><strong>Essential (intractable)</strong>
        <ul>
          <li>Algorithm is computationally infeasible</li>
          <li>Approximations introduce uncertainty</li>
          <li>Examples: Game of Go, optimization problems</li>
        </ul>
      </li>
    </ul>
  </div>

</div>
</div>

**Critical insight**: Essential transformation uncertainty often reflects **uncertain output** — requires probabilistic or AI-based approaches

---

## Essential Output Uncertainties

| Output characteristics | Example |
|---|---|
| There is a known right answer | Mathematical computation |
| The right answer(s) can be known | Sales website (How well did a product sell?) |
| Right answer exists but is infeasible to compute directly | Game of Go (astronomical state space) |
| Unknown right answer; we can **guess** | Image recognition |
| Effect is unknown, but can be measured | Optimization problems |
| Effect is unknown; system is **chaotic** | Weather forecasting |
| No specific answer, but can observe "right" direction | Advertising; many simulation problems |
| No single right answer; the problem is **vague** | Automated prose writing |
| The problem itself is unknown | Grounded theory |

---

## Spectrum of Uncertainty

<center>

![width:800px](images/spectrum-uncertainty.png)

</center>

---

## Architectural Approaches

Different levels and characteristics of uncertainty suggest different architectural styles, patterns, and tactics

- **Virtually no uncertainty** → Batch processing
- **Accidental uncertainty** → Pipes & Filters; Layers; Broker
- **Greater essential uncertainty** → AI‑based approaches
  - Blackboard
  - Neural networks
  - Machine learning / deep learning

---

## Spectrum of Architectural Approaches

<center>

![width:800px](images/spectrum-architectures.png)

</center>

---

## An Architecture Process for Uncertainty

1. **Identify** uncertainties associated with the system.  
2. For each, determine if it is **essential** or **accidental**.  
3. **Study the source** of uncertainty (external is often accidental).  
4. Determine if a **transformation** can remove the uncertainty.  
5. If so, apply **fault‑tolerance** and related techniques. If not, use AI-based approaches.

**Key questions:**
- **Input**: Is it due to imprecise specification or data variability?
- **Output**: Is there a known correct output? Can it be deterministically derived?
- **Transformation**: Is the relationship deterministic? If so, is it tractable?

---

## Case Study: Helicopter Rotor Balancing

<div class="two-column">

<div>

**Problem**: Unbalanced rotor causes vibration, wear, loss of power, safety issues

**Uncertainty Analysis:**
- **Input**: Known measurements; unique wear patterns (essential)
- **Output**: Measurable (IPS); multiple solution sequences possible
- **Processing**: Initially appeared non-deterministic/chaotic

**Initial approach**: Neural network (treating as essential uncertainty)

</div>

<div>

![width:100%](images/helicopter-rotor.png)

</div>

</div>

---

## Case Study: Helicopter Rotor Balancing (continued)

**Further analysis revealed:**
- Each helicopter has a **unique wear profile**
- Initial NN trained on many helicopters → generic approximation
- **Adjustment/response history** reveals unique profiles
- **Key insight**: There exists a **deterministic, repeatable** sequence of adjustments with **feedback loops**

**What appeared essential was actually accidental**, solvable with the right approach.

**Results**: System balances rotors to **0.05 IPS** — *10× better* than the 0.5 IPS standard. Actively marketed to US Army.

---

## Case Study: Online Bookstore Evolution

**Initially**: Inputs/outputs well‑specified; numerous **accidental uncertainties** (e.g., unreliable networks). Straightforward architecture.

**Evolution 1 — Related Books**: Which books are related? An **essential uncertainty** — output cannot be known beforehand, no single right answer. Approaches become **probabilistic** (recommendation algorithms).

**Evolution 2 — Promotions**: Using browsing history introduces even more uncertainty. Requires **machine learning** approaches, mapping to different positions on the uncertainty spectrum.

---

## References

- Harrison, N.B., Rudolph, G., and Aldous, P. *Software Architecture for Essential and Accidental Uncertainty*. HICSS, 2026.  
- Harrison, N.B., Rudolph, G., and Aldous, P. *Is Artificial Intelligence the Answer to Everything?* Intermountain Conference on Engineering, Technology and Computing (IETC), 2025.

---

<!-- Last slide: remove background to be plain -->
<!-- _backgroundImage: none -->
# Thank you!

**Summary**: We've presented a framework for understanding essential versus accidental uncertainty in software architecture. This distinction is crucial for selecting appropriate architectural approaches. Essential uncertainty requires probabilistic and AI-based methods, while accidental uncertainty can be addressed with traditional fault-tolerance techniques.

Questions?
