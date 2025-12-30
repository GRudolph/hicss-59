# Presentation Script: Software Architecture for Essential & Accidental Uncertainty
## HICSS 2026 - 10-15 Minute Presentation

**Total Target Time: 12-14 minutes** (leaves 1-3 minute buffer)

---

## SLIDE 1: Title Slide
**Time: 0:00 - 0:15 (15 seconds)**

"Good morning/afternoon. I'm George Rudolph from Utah Valley University, and I'm here with my colleagues Neil Harrison and Peter Aldous to present our work on Software Architecture for Essential and Accidental Uncertainty."

*[Pause, make eye contact, take a breath]*

---

## SLIDE 2: Introduction: A Bit of History (ENIAC)
**Time: 0:15 - 0:50 (35 seconds)**

"Let's start with a bit of history. The ENIAC - the Electronic Numerical Integrator and Computer - was the first general-purpose computer, built to solve a large class of numerical problems."

*[Point to image]*

"Early computing problems were precisely specified: we knew the inputs, we knew the algorithms, and the results were deterministically computed. This was the world of mathematical computation."

---

## SLIDE 3: Progress: More Applications
**Time: 0:50 - 1:20 (30 seconds)**

"But computing quickly expanded beyond mathematics. Business applications had varying amounts and nature of input data. Data communication introduced timing issues, failures, and corruption. Control systems needed to handle diverse problems reliably. And now, artificial intelligence deals with unknown inputs, unknown transformations, and unknown outputs."

*[Pause for emphasis]*

"The nature of our problems has fundamentally changed."

---

## SLIDE 4: History: Summary
**Time: 1:20 - 1:55 (35 seconds)**

"So here's the key transition: Originally, computing tackled mathematical problems with precisely defined inputs, outputs, and algorithms. But as software capabilities expanded, inputs, outputs, and processes have become less precise."

*[Emphasize the next part]*

"We must now deal with uncertainty. And therefore, it is necessary to understand uncertainty and how to approach it in architecture and design."

---

## SLIDE 5: Current State of the Art
**Time: 1:55 - 2:30 (35 seconds)**

"In 2010, David Garlan called for uncertainty to be a first-class concern in software design and development. However, research and practice often focus primarily on fault tolerance and related tactics."

*[Pause, then emphasize]*

"This misses a large part of uncertainty, and that's what motivates our deeper investigation."

---

## SLIDE 6: Essence vs. Accident (Brooks, 1986)
**Time: 2:30 - 3:10 (40 seconds)**

"To frame our work, we draw on Fred Brooks' classic distinction from 1986. Accidental complexity is created by engineering choices and can be mitigated by better tools and abstractions. Essential complexity is inherent in the problem and cannot be removed."

*[Point to Brooks image]*

"Likewise, we argue there is essential and accidental uncertainty. This distinction is crucial for how we architect systems."

---

## SLIDE 7: Essential and Accidental Uncertainty
**Time: 3:10 - 3:45 (35 seconds)**

"Let me define these clearly. Accidental uncertainty can be separated from the problem - a transformation exists to remove it. Think of network failures - we can add redundancy, retry logic, error correction."

*[Pause]*

"Essential uncertainty must be addressed as part of the problem - no transformation can remove it. This is the uncertainty that's inherent to what we're trying to solve."

---

## SLIDE 8: Uncertainty and Data
**Time: 3:45 - 4:15 (30 seconds)**

"Computing is fundamentally the processing of data. So we consider uncertainty across three dimensions: Input - which can be essential or accidental. The transformation from input to output - which can also be essential or accidental. And output - which is often essential."

*[Gesture to show the flow]*

"This framework helps us analyze where uncertainty exists in our systems."

---

## SLIDE 9: Input: Examples
**Time: 4:15 - 4:50 (35 seconds)**

"Let's look at input uncertainty. Unreliable transmission is accidental - datacom protocols can mitigate it. The amount of data is often accidental - we can process incrementally. User input errors are accidental - we validate and re-prompt."

*[Pause, then emphasize]*

"But concurrent access? That's accidental if we can discretize it, but essential in cases like ticketing for the same seat. Two people can't both have seat 12A."

---

## SLIDE 10: Input Uncertainty — Other Cases
**Time: 4:50 - 5:05 (15 seconds)**

"Other input uncertainties may be essential, and we'll revisit these with our case studies."

*[Quick transition - this slide is brief]*

---

## SLIDE 11: Uncertainty in the Transformation
**Time: 5:05 - 5:35 (30 seconds)**

"Uncertainty in the transformation is often accidental on its own. Hardware glitches can be mitigated via duplication. Compiler differences are acceptable if behavior is equivalent."

*[Pause]*

"But the interesting cases arise when transformation uncertainty is tied to output uncertainty - and that's where we need different architectural approaches."

---

## SLIDE 12: Output Uncertainty
**Time: 5:35 - 6:00 (25 seconds)**

"Accidental output uncertainty is generally less interesting. But essential output uncertainty spans a wide spectrum - and this requires a corresponding spectrum of architectural approaches."

*[This sets up the next important slide]*

---

## SLIDE 13: Essential Output Uncertainties
**Time: 6:00 - 7:00 (60 seconds)**

"This is crucial - let me walk through the spectrum. At one end, there's a known right answer - mathematical computation. Then the right answer can be known - like a sales website asking how well a product sold."

*[Point to table]*

"Moving along: the right answer exists but is infeasible to compute directly - think Game of Go with its astronomical state space. Then we have unknown right answers where we can guess - image recognition."

*[Pause for audience to read]*

---

## SLIDE 14: More Examples
**Time: 7:00 - 7:45 (45 seconds)**

"Continuing the spectrum: Effect is unknown but can be measured - optimization problems. Effect is unknown and the system is chaotic - weather forecasting."

*[Point to examples]*

"No specific answer but we can observe the right direction - advertising, many simulation problems. No single right answer - the problem is vague - automated prose writing. And finally, the problem itself is unknown - grounded theory."

*[Emphasize the range]*

"This spectrum is critical for choosing architectural approaches."

---

## SLIDE 15: Thought Question
**Time: 7:45 - 8:15 (30 seconds)**

"Here's a thought question for you: How would you characterize automatic software coding?"

*[Pause 3-4 seconds for audience to think]*

"The trick is: it depends on the nature of the software. If you cannot precisely specify what the generated software should do, how can you verify it? This highlights the challenge of essential uncertainty."

---

## SLIDE 16: Spectrum of Uncertainty
**Time: 8:15 - 8:40 (25 seconds)**

*[Point to diagram]*

"This diagram visualizes the spectrum we've been discussing - from known answers to unknown problems. Take a moment to see how the examples map across this range."

*[Let audience read for 10 seconds]*

---

## SLIDE 17: Architectural Approaches
**Time: 8:40 - 9:20 (40 seconds)**

"Different levels of uncertainty suggest different architectural styles. Virtually no uncertainty? Batch processing works fine. Accidental uncertainty? Pipes and Filters, Layers, Broker patterns."

*[Pause]*

"But with greater essential uncertainty, we need AI-based approaches: Blackboard architectures, neural networks, machine learning and deep learning. The architecture must match the nature of the uncertainty."

---

## SLIDE 18: Spectrum of Architectural Approaches
**Time: 9:20 - 9:45 (25 seconds)**

*[Point to diagram]*

"This shows how architectural approaches map to the uncertainty spectrum. Notice how we move from traditional patterns to AI-based approaches as uncertainty increases."

*[Let audience absorb]*

---

## SLIDE 19: An Architecture Process for Uncertainty
**Time: 9:45 - 10:30 (45 seconds)**

"We propose a five-step process. First, identify uncertainties associated with the system. Second, for each, determine if it's essential or accidental."

*[Point to steps]*

"Third, study the source of uncertainty - external is often accidental. Fourth, determine if a transformation can remove the uncertainty. And fifth, if so, apply fault-tolerance and related techniques."

*[Emphasize]*

"If not - if it's essential - you need different approaches."

---

## SLIDE 20: Analyze Uncertainties — Input
**Time: 10:30 - 11:00 (30 seconds)**

"For input analysis, ask: Is it due to imprecise or incomplete specification? Is it due to variability in data - transmission, user errors? And critically: what can and cannot be known about input at runtime?"

*[Quick transition]*

---

## SLIDE 21: Analyze Uncertainties — Output
**Time: 11:00 - 11:35 (35 seconds)**

"For output, ask: What is the objective of the system? How do we know it meets the objective? Is there a known correct output? Is the correct output unknowable but estimable? Can output be deterministically derived from inputs? Are there multiple correct outputs, and if so, is one preferable?"

---

## SLIDE 22: Analyze Uncertainties — Transformation
**Time: 11:35 - 12:00 (25 seconds)**

"For transformation: Is the relationship between input and output deterministic? And if deterministic, is it tractable?"

*[Quick transition to case study]*

---

## SLIDE 23: Case Study: Helicopter Rotor Balancing
**Time: 12:00 - 12:45 (45 seconds)**

"Let me illustrate with a real case study. If the main rotor of a helicopter is not perfectly balanced, excess vibration occurs. This causes wear, loss of power, and can compromise safety."

*[Point to image]*

"The rotor is a complex system with multiple adjustment points. This was a real problem that needed solving."

---

## SLIDE 24: Uncertainty Analysis — Input (Rotor)
**Time: 12:45 - 13:15 (30 seconds)**

"Applying our framework: Input is known and precisely specified - vibration measurements, blade positions, adjustment points. User entry errors are external - we apply standard fault tolerance techniques."

*[Emphasize]*

"But each helicopter has unique wear patterns - this is essential uncertainty that must be considered."

---

## SLIDE 25: Uncertainty Analysis — Output (Rotor)
**Time: 13:15 - 13:50 (35 seconds)**

"Output: The objective is measurable - change in vibration, measured in IPS, inches per second. Desired output is a range - lower is better. Acceptable standard is 0.5 IPS."

*[Pause]*

"But here's the key question: Is there a single solution? There may be different sequences of adjustments achieving the goal."

---

## SLIDE 26: Uncertainty Analysis — Processing (Rotor)
**Time: 13:50 - 14:25 (35 seconds)**

"Processing: Is the relationship deterministic? Initially, this was unknown. Combinations of adjustments appeared non-deterministic, even chaotic."

*[Pause for emphasis]*

"So the approach was to use a neural network to derive suggested solutions."

---

## SLIDE 27: Further Analysis (Rotor)
**Time: 14:25 - 15:00 (35 seconds)**

"Further analysis revealed something important: Each helicopter has a unique wear profile. The initial neural network was trained on many helicopters - giving a generic approximation."

*[Pause]*

"But adjustment and response history reveals unique profiles. And here's the insight: There exists a deterministic, repeatable sequence with feedback loops - but it's unique to each helicopter."

---

## SLIDE 28: Results (Rotor)
**Time: 15:00 - 15:35 (35 seconds)**

"The results were impressive. The system reliably balances main rotors to 0.05 IPS - that's ten times better than the standard of 0.5 IPS."

*[Pause for impact]*

"It's actively marketed to the US Army and other organizations. This demonstrates the importance of understanding essential versus accidental uncertainty - and choosing the right architectural approach."

---

## SLIDE 29: Case Study: Online Bookstore
**Time: 15:35 - 16:00 (25 seconds)**

"Let me briefly touch on another case study. Initially, an online bookstore had well-specified inputs and outputs, with numerous accidental uncertainties like unreliable networks. The architecture was straightforward."

---

## SLIDE 30: Bookstore Evolution — Related Books
**Time: 16:00 - 16:35 (35 seconds)**

"But then they added a 'related books' feature. Which books are related? This is an essential uncertainty - the output cannot be known beforehand, there's no single right answer."

*[Pause]*

"The approaches become probabilistic. This is a different kind of problem requiring different architectural patterns."

---

## SLIDE 31: Bookstore Evolution — Promotions
**Time: 16:35 - 17:05 (30 seconds)**

"Further evolution: using browsing history to promote products. Even more uncertainty - the problem is less well-defined. This requires considering machine learning and mapping to the uncertainty spectrum we discussed."

---

## SLIDE 32: References
**Time: 17:05 - 17:15 (10 seconds)**

*[Quick acknowledgment]*

"Our work is published in HICSS 2026, and we also presented related work at IETC 2025."

*[Don't read the references - just acknowledge]*

---

## SLIDE 33: Thank you!
**Time: 17:15 - 17:25 (10 seconds)**

"Thank you for your attention. I'm happy to take questions."

*[Pause, smile, make eye contact]*

---

## PRACTICE TIPS

1. **Timing Practice:**
   - Practice each section individually first
   - Then practice full run-throughs
   - Use a timer and aim for 12-14 minutes total
   - Mark slides where you consistently go over/under

2. **Emphasis Points:**
   - "We must now deal with uncertainty" (Slide 4)
   - "This misses a large part of uncertainty" (Slide 5)
   - "Essential vs. accidental" (throughout)
   - "Ten times better" (Slide 28 - rotor results)

3. **Transitions:**
   - Use pauses effectively
   - "Let me illustrate..." (before case studies)
   - "Here's the key question..." (before important points)
   - "This demonstrates..." (after case study results)

4. **Body Language:**
   - Point to images and diagrams
   - Make eye contact with audience
   - Use hand gestures to show spectrum/flow
   - Pause after key statements

5. **If Running Long:**
   - Cut or shorten: Slide 10, Slide 11, Slide 12
   - Condense bookstore case study (Slides 29-31)
   - Shorten analysis slides (20-22)

6. **If Running Short:**
   - Expand on rotor case study details
   - Add more examples in uncertainty spectrum
   - Elaborate on architectural approaches

---

## KEY MESSAGES TO REINFORCE

1. **Uncertainty is a first-class concern** in software architecture
2. **Essential vs. accidental** distinction is crucial
3. **Spectrum of uncertainty** requires spectrum of approaches
4. **Case studies demonstrate** the practical application
5. **Process framework** helps architects analyze uncertainty

---

**Good luck with your presentation!**
