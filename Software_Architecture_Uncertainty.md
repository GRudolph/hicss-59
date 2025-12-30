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
  h2 { font-weight: 700; }
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
    font-size: 18px !important;
    line-height: 1.2 !important;
  }
  .small-text li, .small-text p {
    font-size: 20px !important;
    line-height: 1.2 !important;
    margin-bottom: 4px;
  }
  .smaller-text {
    font-size: 16px !important;
    line-height: 1.15 !important;
  }
  .slide9-content {
    font-size: 18px !important;
    line-height: 1.2 !important;
  }
  .slide9-content li {
    font-size: 18px !important;
    line-height: 1.2 !important;
    margin-bottom: 4px;
  }
  .slide9-content p {
    font-size: 18px !important;
    line-height: 1.2 !important;
    margin-bottom: 6px;
  }
  
  /* Slide 9 nested-list markers (stronger specificity + !important) */
  section.slide9 ul ul { list-style-type: circle !important; }
  section.slide9 ul ul ul { list-style-type: square !important; }
  section.slide9 ul { list-style-type: disc !important; list-style-position: outside; padding-left: 1.2em; }

  /* Slide 9: force hollow circle for second level and a square for third level via ::marker */
  section.slide9 ul ul li::marker { content: "◦ "; }   /* U+25E6 White Bullet */
  section.slide9 ul ul ul li::marker { content: "▪ "; } /* U+25AA Black Small Square */

  /* Optional: keep top-level as solid disc and tidy spacing */
  section.slide9 ul li::marker { content: "• "; }       /* solid at first level */
  section.slide9 ul { list-style-position: outside; padding-left: 1.2em; }
  section.slide9 ul ul { padding-left: 1.1em; }


---

<!-- class: lead -->
<!-- _backgroundImage: url('images/title-bg.jpg') -->
# Software Architecture for Essential & Accidental Uncertainty

**Neil Harrison**, **George Rudolph** (presenter), **Peter Aldous**  
Utah Valley University
Orem, Utah

---

## &nbsp; Introduction: A Bit of History

<div class="two-column">

<div>

**ENIAC** — Electronic Numerical Integrator and Computer  
First general-purpose computer built to solve *a large class of numerical problems*.  1945-1955

 -  Fisrt computer to run at electronic speed
 - Killed by lightning strik in 1955
 - Early problems were **precisely specified**: inputs, algorithms, outputs, ...
 - Results were deterministically computed

</div>

<div>

![width:100%](images/eniac.png)

</div>

</div>

---

## Progress

- Original computing tackled precisely-defined **mathematical problems**
- Over time, capabilities expanded to **business applications, data communication, control systems, and AI**
    - inputs, outputs, and processes became more varied, less precise.
    - an artifact of modeling non-mathematical problems via mathematical abstractions
- We must now deal with <span class="text-red">uncertainty</span> — and understand how to <span class="text-green">approach</span> it in architecture and design.

---

## Current State of the Art

- (2010) **David Garlan** called for uncertainty to be a first‑class concern in software design and development.
- Current research and practice focus on **fault tolerance** and related tactics.
- **This misses a large part of uncertainty** and motivates a deeper investigation.

---

## &nbsp; Essence vs. Accident (Brooks, 1986)

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

---

## Uncertainty and Data

Computing is the **processing of data**. Consider uncertainty across:

- **Input** (can be essential or accidental)
- **Transformation** from input to output (can be essential or accidental)
- **Output** (often essential)

---

## Input: Uncertainty Examples

- **Unreliable data transmission** — Accidental; datacomm protocols implement transformations to remove uncertainty
- **Amount of data** — Often accidental; handle in subsets
- **User input errors** — Accidental; parse for correctness and re-prompt
- **Multiple concurrent access** — Accidental if handled discretely; **Essential** if not (e.g., venue ticket website, requests for the *same* seat)

---

<!-- _class: slide9 -->
## &nbsp; Uncertainty in the Transformation (Algorithms)

The **algorithm or processing logic** that transforms input to output can *introduce* uncertainty

<div class="small-text">
<div class="two-column">

  <div>
    <ul>
      <li><strong>Accidental</strong> → can be fixed
        <ul>
          <li>Hardware glitches</li>
          <li>compiler differences</li>
          <li>implementation bugs</li>
        </ul>
      </li>
      <li><strong>Essential</strong>
        <ul>
          <li>No deterministic algorithm exists to compute correct output</li>
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
          <li>approximations introduce uncertainty in accuracy/precision</li>
          <li>Examples: Game of Go, optimization problems</li>
        </ul>
      </li>
    </ul>
  </div>

</div>
</div>

**Critical insight**: Essential transformation uncertainty often reflects **uncertain output** — requires probabilistic or AI-based approaches

---

## Output Uncertainty

- *Accidental* output uncertainty is generally less architecurally interesting.
- **Essential output uncertainty** spans a wide spectrum — requires a corresponding spectrum of architectural approaches.

---

## &nbsp; Essential Output Uncertainties

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

## Thought Question

How would you characterize **automatic software coding**?

> Trick: It depends on the nature of the software.  
> If you cannot precisely specify what the generated software should do, **how can you verify it?**

> Generative AI makes good answers at once more vital and more complex

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

</center

---

## An Architecture Process for Uncertainty

1. **Identify** uncertainties associated with the system.  
2. For each, determine if it is **essential** or **accidental**.  
3. **Study the source** of uncertainty (external is often accidental).  
4. Determine if a **transformation** can remove the uncertainty.  
5. If so, apply **fault‑tolerance** and related techniques.

---

## Analyze Uncertainties — Input 

- Is it due to **imprecise/incomplete specification**?  
- Is it due to **variability in data** (transmission, user errors, ...)?  
- What can and cannot be known about input **at runtime**?

---

## Analyze Uncertainties — Output

- What is the **objective** of the system? How do we know it meets the objective?
- Is there a **known correct output**?
- Is the correct output **unknowable** (but estimable)?
- Can output be **deterministically** derived from inputs?  
- Are there **multiple correct outputs**? If so, is one **preferable**?

---

## Analyze Uncertainties — Transformation

- Is the relationship between input and output **deterministic**?  
- If deterministic, is it **tractable**?

---

## Case Study: Helicopter Rotor Balancing

<div class="two-column">

<div>

- If the main rotor is not perfectly balanced, excess **vibration** occurs.  
- Vibration causes **wear**, **loss of power**, and can compromise **safety**.  
- The rotor is a complex system with multiple **adjustment points**.

</div>

<div>

![width:100%](images/helicopter-rotor.png)

</div>

</div>

---

## Uncertainty Analysis — Input (Rotor)

- Input is **known and precisely measured**: vibration measurements; blade positions; adjustment points.  
- **User entry errors** → external; apply standard Fault Tolerance techniques (to correct accidental uncertainty)
- Each helicopter has **<span class="text-red">unique</span>**  wear patterns → *essential*; must be considered.

---

## Uncertainty Analysis — Output (Rotor)

- Objective measurable: **change in vibration** (IPS — inches per second).  
- Desired output is a **range** (lower is better).  
- Acceptable standard: **0.5 IPS**.  
- Single solution? There may be **different sequences** of adjustments achieving the goal.

---

## Uncertainty Analysis — Processing (Rotor)

- Is the relationship between input and output **deterministic**? Initially **unknown**.  
- Combinations of adjustments appeared **non‑deterministic** / **chaotic**.  
- *Initial* Approach: use a **neural network** to derive suggested solutions.

---

## Further Analysis (Rotor)

- **Unique wear profile** for each helicopter.  
- Initial NN trained on **many helicopters** → a **generic** approximation.  
- **Adjustment/response history** of testing reveals unique profiles.  
- **Intermediate Result**: There exists a **deterministic, repeatable** sequence of adjustments with **feedback loops**.
  - details are proprietary

---

## Relevant Results

- System reliably balances main rotors to **0.05 IPS** — *10× better* than the standard.  
- Actively marketed to **US Army** and other organizations.  
- Demonstrates the importance of understanding **essential vs. accidental** uncertainty.
  - to choose the right architectural approach

---

## Case Study: Online Bookstore

- **Initially**: Inputs/outputs well‑specified; numerous **accidental uncertainties** (e.g., unreliable networks).  
- Straightforward architecture.

---

## Bookstore Evolution — Related Books

- Add **“related books”** feature.  
- Which books are **related**? An **essential uncertainty** — output cannot be known beforehand, no single right answer.  
- Approaches become **probabilistic**.

---

## Bookstore Evolution — Promotions

- Use **browsing history** to promote products.  
- Even **more uncertainty**; the problem is less well‑defined.  
- Consider **machine learning**; map to the uncertainty **spectrum**.
- recommendation engines are a popular, common solution.

---

## References

- Harrison, N.B., Rudolph, G., and Aldous, P. *Software Architecture for Essential and Accidental Uncertainty*. HICSS, 2026.  
- Harrison, N.B., Rudolph, G., and Aldous, P. *Is Artificial Intelligence the Answer to Everything?* Intermountain Conference on Engineering, Technology and Computing (IETC), 2025.

---

<!-- Last slide: remove background to be plain -->
<!-- _backgroundImage: none -->
# Thank you!

Questions?

