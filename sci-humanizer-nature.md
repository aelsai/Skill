---
name: sci-humanizer-nature
version: 1.0.0
description: |
  Remove AI-generated writing patterns from scientific manuscripts targeting
  Nature, Science, and equivalent high-impact journals. Calibrated for PhD-level
  natural science writing. Covers 50+ patterns: significance inflation, AI
  vocabulary (tiered by detection strength), deep syntax tells (abstract noun
  subjects, nominalizations, clause stacking), em dash zero-tolerance, copula
  avoidance, hedging imbalance, Nature/Science-specific tells, and classical
  vocabulary restoration. Preserves disciplinary conventions: passive voice in
  Methods, technical terms, appropriate hedging. Two-pass anti-AI audit with
  structural refinement for senior researcher voice.
license: MIT
compatibility: claude-code
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Sci-Humanizer: Nature/Science Edition

Remove AI-generated writing patterns from scientific manuscripts. Calibrated for
PhD-level writing in the natural sciences, with specific attention to Nature/Science
journal conventions.

**Use when:** editing manuscripts, abstracts, cover letters, or any scientific prose
for submission to Nature, Science, Cell, PNAS, or equivalent high-impact journals.

**What makes this different from general humanizers:** Scientific AI patterns are
subtler than blog-post patterns. The tells are in syntax (nominalizations, abstract
noun subjects, clause stacking), hedging architecture, structural templates, and a
vocabulary drift away from classical academic phrasing. This skill targets those
tells while preserving disciplinary conventions that general humanizers would
incorrectly flag (passive voice in Methods, standard hedging, technical jargon).

---

## Nature/Science Journal Context

Nature and Science publish primary research across all natural sciences for a broad
scientific audience. Their conventions differ from specialist journals:

- **First-person ("We") is standard and preferred** for the main narrative. Methods
  may use passive voice.
- **Findings-first structure** is valued. A strong sentence leads with the result,
  not the setup.
- **Concision is mandatory.** Articles run 1,500–4,000 words; every sentence must
  earn its place.
- **Quantification over qualification.** "18% improvement (P = 0.003)" always beats
  "significant improvement."
- **Novelty is never self-claimed.** Remove "novel," "for the first time," "to our
  knowledge" except one carefully placed instance in the abstract if truly needed.
- **Sentences end on the key point.** Qualifying clauses go in the middle, not at
  the end.

---

## Workflow

```
Receive text
  → Step 1: Diagnose  — list every violation with rule group; do NOT revise yet
  → Step 2: Revise    — fix all flagged items; preserve meaning exactly
  → Step 3: Structural pass (text > 5 sentences or repeated structures remain)
  → Step 4: Anti-AI audit — "What still makes this obviously AI-generated?"
                             List remaining tells. Revise again.
  → Step 5: Final check — search output for "—" (em dash). Zero allowed. Done.
```

**Step 1 discipline:** Diagnose without revising. A running edit misses patterns
that a systematic scan catches. Format: `"exact phrase" — Group X: explanation`.

**Step 3 applies when:** text exceeds 5 sentences OR Step 2 leaves consecutive
sentences with identical structures.

**Step 4 purpose:** This catches patterns that emerge FROM the cleanup — sterile,
structurally clean but voiceless prose. Removing "delve" and replacing it with
"examine" does not fix the problem if the paragraph still reads as template-generated.
Step 4 is where researcher voice enters.

---

## What NOT to Change

These boundaries are as important as the rules. Violations here damage scientific
accuracy or disciplinary trust.

- Sentences that already read naturally. Do not edit to show work.
- **Passive voice in Methods sections.** It is the disciplinary standard for
  reproducibility. Converting to active voice here is wrong.
- **Technical and disciplinary vocabulary.** "Downregulated," "heteroscedasticity,"
  "ablation study," "gene ontology enrichment" are correct terms, not AI patterns.
- **Appropriate hedging on uncertain claims.** "May," "suggests," "is consistent
  with" are required for observational, mechanistic, and exploratory claims.
- **Complete and necessary lists.** Molecular components, experimental conditions,
  defined categories — do not truncate these. Only trim illustrative lists.
- **Standard statistical language** backed by actual statistics: "significantly"
  with a P-value, effect sizes, confidence intervals.
- **Standard academic transitions used once**, followed by specific data: "Notably,"
  "Importantly," "Interestingly," "Furthermore" are fine in isolation. Flag only
  when clustered (two or more of these in one paragraph).

---

## Phrases to PRESERVE

Legitimate academic writing. Flag only when stacked excessively or used without
citations or data.

**Transitional phrases — keep unless clustered:**
- "Notably," / "Of note,"
- "Importantly,"
- "Interestingly," / "Strikingly,"
- "Furthermore," / "Moreover,"
- "In contrast," / "Conversely,"
- "Nevertheless," / "Nonetheless,"
- "Accordingly,"
- "Taken together,"

**Attribution phrases — keep when followed by citation or specific finding:**
- "Prior studies have shown that..."
- "Previous work has demonstrated..."
- "It has been reported that..."
- "A growing body of evidence indicates..."
- "Consistent with..."
- "Evidence suggests that..."

**Rule of thumb:** If a phrase is followed by a specific citation, number, or named
finding, it is legitimate academic writing. Only flag when vague and unsupported.

---

## Group A: Hard Boundaries (Rules 1–4)

Never break these.

1. **Preserve meaning exactly.** Never invent claims, citations, results, or statistics.
2. **Never alter numbers.** P-values, effect sizes, gene names, chemical formulas,
   sample sizes, confidence intervals are untouchable.
3. **Never convert correlation to causation.** Observational associations must stay
   associations regardless of how the original author framed them.
4. **Match hedging to evidence strength.**
   - RCT primary endpoint → direct statement acceptable: "Empagliflozin reduced
     cardiovascular death."
   - Mechanistic inference → one hedge: "...suggesting that AMPK mediates this
     response."
   - Observational/exploratory finding → one hedge: "was associated with," "may
     reduce."
   - Do not strengthen beyond what the data support, and do not weaken an
     established finding with unnecessary hedges.

---

## Group B: Significance Inflation and Promotional Language (Rules 5–10)

**5. Kill significance filler**

Remove words that inflate findings without adding information:

- "plays a crucial/pivotal/central/vital/key role"
- "provides valuable insights"
- "highlights the importance of"
- "underscores the significance of"
- "sheds light on"
- "represents a significant/major advance"
- "marks a pivotal moment / turning point"
- "reflects broader trends"
- "paves the way for"
- "opens new avenues"
- "has far-reaching implications"
- "has the potential to transform"
- "a landmark/groundbreaking study"

Before: "This pivotal finding underscores the crucial role of mitochondrial
dysfunction in the evolving landscape of metabolic disease."
After: "Mitochondrial dysfunction contributed to insulin resistance in all three
mouse models."

**6. Kill promotional adjectives**

Remove adjectives and constructions borrowed from press releases:
- "remarkable," "striking," "impressive" applied to your own findings
- "state-of-the-art," "cutting-edge," "unprecedented"
- "elegant" applied to methods or results
- "robust" unless describing statistical robustness with specific tests
- "comprehensive" — let the scope speak for itself
- "transformative" applied to your own work

Exception: "striking" is appropriate in biology for visually obvious phenotypes when
the description is literal ("a striking reduction in nuclear staining"), not
self-congratulatory.

**7. Kill formulaic limitations-and-future-directions**

The pattern "Despite X challenges, future work will Y" adds no information. Replace
with specific, concrete limitation statements and specific next steps.

Before: "Despite some limitations, these findings pave the way for future studies
that will advance our understanding of this important process."
After: "The absence of human tissue samples limits direct clinical translation.
Future experiments should determine whether [specific intervention] reproduces the
phenotype in primary human cells."

**8. Remove grandiose field-introduction openings**

Remove: "In the ever-evolving field of...," "In recent years, there has been growing
interest in...," "X is one of the most important problems in...," "X remains poorly
understood despite decades of research."

Replace with the specific gap this paper addresses — stated concisely and precisely.

Before: "Cancer remains one of the most devastating diseases affecting humanity. In
the evolving landscape of cancer biology, understanding the molecular mechanisms
driving tumor progression is of paramount importance."
After: "Pancreatic ductal adenocarcinoma has a 5-year survival rate below 12%.
Most patients are diagnosed at stage III or IV, partly because early biomarkers are
lacking."

**9. Remove self-claimed novelty**

Remove: "novel," "for the first time," "unprecedented," "pioneering," "first-of-its-
kind" applied to your own work.

Exception: "to our knowledge" is acceptable once in an abstract if a thorough
literature search supports it.

**10. Kill abstract-noun significance statements at paragraph ends**

LLMs close paragraphs with "Together, these findings underscore the importance
of X" or "...highlighting the significance of Y." These add no new information.

Before: "...Together, these findings underscore the importance of mitophagy in
maintaining neuronal homeostasis."
After: Cut the sentence entirely. Or replace with a specific forward-pointing
statement: "Whether this mechanism operates in non-dividing human neurons remains
to be determined."

---

## Group C: AI Vocabulary Bank (Rules 11–13)

These words appear 5–25× more frequently in post-2023 LLM text than in pre-2023
human scientific writing (Kobak et al. 2025; Liang et al. 2024). They cluster —
when you find one, check for others nearby.

**11. Tier 1 — Hard AI signals: replace always**

delve, tapestry (abstract use), testament (e.g., "a testament to"), interplay
(when vague), intricacies, landscape (abstract use), vibrant, garner (attention/
support), foster (results/findings), showcase, underscore (verb), highlight (verb
applied to own findings), noteworthy

Replacements:
- "delve into" → "examine," "investigate," "analyze"
- "landscape of X" → name the actual domain or subfield
- "interplay between A and B" → specify the direction or mechanism
- "foster" (biological) → "promote," "stimulate," "drive"
- "garner" → "attract," "receive"
- "underscore" → cut, or restructure to make the claim directly
- "highlight" (own findings) → state the finding; it speaks for itself
- "intricacies" → "details," "mechanisms," or name what is complex
- "tapestry" → describe the actual composition

**12. Tier 2 — Frequent AI patterns: replace in most contexts**

Additionally (sentence-initial), align with, crucial, emphasize, enduring, enhance
(unless biological enhancement with specifics), pivotal, valuable (applied to
findings), comprehensive, multifaceted, nuanced (without specifics), novel,
evolving (abstract use), transformative

**13. Tier 3 — Weaker signals: review contextually**

key (as adjective), fundamental, vital, significant (without statistics), emerging
(abstract use), complex (as empty filler without elaboration)

---

## Group D: Superficial -ing Phrase Analyses (Rule 14)

**14. Remove decorative -ing phrases; convert causal ones to explicit connectives**

AI tacks present participle phrases onto sentences to simulate depth. In scientific
writing, these often function as implicit replacements for "therefore" and "thus" —
both of which have declined in AI-generated academic text. The result is a causal
claim disguised as a description.

**Pattern:** [data statement], [verb]-ing [conclusion or implication].

Decision rule:
- If the -ing phrase introduces genuine mechanistic or analytical inference → convert
  to an explicit connective: "therefore," "thus," "accordingly," or make it a
  separate sentence.
- If the -ing phrase restates or decorates a finding that speaks for itself → cut.

Before (decorative — cut it):
"All three replicates showed the same phenotype, underscoring the robustness of our
experimental system."
After: "The phenotype was reproducible across three biological replicates."

Before (causal — convert to explicit):
"The mutation abolished kinase activity, highlighting the critical importance of
this residue for catalysis."
After: "The mutation abolished kinase activity. This residue is therefore required
for catalysis."

Before (legitimate — keep as is):
"FOXO3 expression increased 4-fold following rapamycin treatment, suggesting that
mTOR suppresses FOXO3 under nutrient-replete conditions."
→ This encodes genuine mechanistic inference. Keep "suggesting."

Words to watch: highlighting, underscoring, emphasizing, reflecting, symbolizing,
contributing to, fostering, showcasing, suggesting (decorative use), demonstrating,
indicating, prompting, confirming.

---

## Group E: Punctuation and Formatting (Rules 15–18)

**15. Em Dash Zero Tolerance**

Replace ALL em dashes (—). No exceptions. This is one of the most consistent
mechanical AI tells in scientific writing — even one flags a document.

Replacement options:
- Parenthetical/appositive → commas:
  "mTOR—a serine/threonine kinase—regulates..." →
  "mTOR, a serine/threonine kinase, regulates..."
- Explanatory aside → parentheses:
  "the benefit—a 3-fold increase—was significant" →
  "the benefit (a 3-fold increase) was significant"
- Clause break → period or semicolon:
  "X increased—Y decreased" → "X increased. Y decreased." or "X increased; Y
  decreased."

After all edits: search the entire output for the character "—". If any remain,
replace them. Zero em dashes in final output.

**16. No colons introducing bullet lists mid-paragraph**

Scientific prose does not use inline bullet lists. Integrate into flowing sentences.

Before: "The method has three advantages: it is rapid, scalable, and inexpensive."
After: "The method is rapid, scalable, and inexpensive."
Or, with data: "The method returns results within 2 hours, processes 96 samples in
parallel, and costs less than $5 per sample."

**17. No scare-quotes around technical terms**

Do not use quotation marks to signal that a term is informal or uncertain. Either
use the term directly or define it properly at first use.

Before: "The cells underwent a process of 'metabolic reprogramming'."
After: "The cells underwent metabolic reprogramming."

**18. Section headings: sentence case, not title case**

AI applies title case to headings. Scientific manuscripts use sentence case.

Before: "Statistical Analysis And Primary Endpoints"
After: "Statistical analysis and primary endpoints"

---

## Group F: Deep AI Syntax Patterns (Rules 19–25)

These are the most sophisticated tells — structural patterns that survive surface-
level vocabulary editing.

**19. Abstract noun subjects**

LLMs make abstractions the grammatical subject: "This finding suggests...," "These
results demonstrate...," "The analysis reveals...," "This observation indicates..."

Replace with concrete subjects: what changed, what was measured, which cells, which
animals.

Before: "This finding suggests that autophagy is required for memory consolidation."
After: "ATG5-knockout mice failed to consolidate fear memories (Fig. 3c),
suggesting that autophagy is required for this process."

Before: "These results demonstrate the efficacy of the treatment."
After: "Treated mice showed a 4-fold reduction in tumor volume (P < 0.001)."

If 2+ consecutive sentences begin with "This/These/The results/The analysis," vary
the subjects.

**20. Nominalizations**

LLMs nominalize aggressively: turning verbs into noun phrases obscures the actor
and the action.

Replace:
- "the examination of X" → "examining X"
- "the occurrence of Y" → "when Y occurred"
- "the inhibition of Z" → "inhibiting Z" / "when Z was inhibited"
- "the reduction in X" → "X decreased" / "X fell by..."
- "the identification of" → "identifying" / "we identified"
- "the administration of" → "administering" / "we administered"

Before: "The observation of increased phosphorylation in knockout cells led to the
conclusion that AMPK is required for this modification."
After: "Knockout cells showed increased phosphorylation, suggesting that AMPK is
required for this modification."

**21. Relative clause stacking**

Chains of "that" or "which" clauses read as AI generation.

Before: "This is a method that allows the detection of proteins that are present at
low levels in samples that have been processed under standard conditions."
After: "This method detects low-abundance proteins in standard tissue preparations."

**22. "While X, Y" overuse**

AI defaults to this construction for every concessive. Vary the placement or split
into two sentences.

Before: "While previous studies have examined this pathway in yeast, its role in
mammalian cells remains unclear."
After: "This pathway has been characterized in yeast; its role in mammalian cells
is not known."
Or start with the gap: "The mammalian equivalent of this pathway has not been
characterized."

**23. Symmetric parallelism substituting for data**

AI forces content into adjective triplets ("rapid, accurate, and reproducible")
instead of reporting actual performance data. Replace abstract adjective lists with
concrete numbers.

Before: "Our approach is rapid, accurate, and reproducible."
After: "Our approach returned results within 2 hours with a false-positive rate
below 1% across three independent validation cohorts."

**24. Closing every causal chain**

LLMs spell out every inference: "...which resulted in X, thereby leading to Y,
ultimately causing Z." Researchers trust readers to follow causal chains.

Before: "AMPK phosphorylated TSC2, thereby inhibiting mTORC1, which ultimately
reduced protein synthesis."
After: "AMPK phosphorylated TSC2, inhibiting mTORC1 and reducing protein synthesis."
Or: "AMPK phosphorylated TSC2, inhibiting mTORC1." (if the downstream consequence
is obvious to the target audience)

**25. Uniform sentence structure throughout a paragraph**

A paragraph of S-V-O sentences with identical lengths is an AI tell even after
vocabulary cleaning. Apply deliberate variation:
- Begin occasionally with a prepositional phrase: "At 48 hours, all treated
  cells..."
- Begin with a conditional: "When the temperature exceeded 37°C..."
- Use an inverted construction: "What the data do not show is equally informative."
- Place a short sentence (under 12 words) after two long ones.

---

## Group G: Hedging Balance (Rules 26–29)

**26. Reduce redundant multi-layer hedging**

LLMs stack hedges: "may suggest," "could potentially," "might indicate," "possibly
reflect." 1–2 well-chosen hedges per claim is the maximum.

Before: "These findings may suggest that SGLT2 inhibitors have the potential to
confer beneficial effects on cardiovascular outcomes in select patient populations."
After: "These findings suggest that SGLT2 inhibitors may reduce cardiovascular
events."

**27. Do not over-hedge well-supported claims**

Hedging is epistemic, not defensive. Over-hedging makes authors appear uncertain
about their own data.

If P = 0.0001 with a large effect size across multiple independent experiments,
do not write "may possibly suggest a potential trend toward." Write "reduced by
40% (P < 0.001)."

**28. Appropriate causal language for observational contexts**

In observational studies, never write "X causes Y" unless causal inference methods
were applied. Use:
- "X was associated with Y" (observational)
- "X predicted Y" (regression)
- "X correlated with Y" (correlation)
- Reserve "demonstrates," "shows," "proves" for direct experimental manipulations
  with appropriate controls.

**29. Concentrate hedging at genuinely uncertain claims**

Do not distribute hedges evenly across a paragraph. Write directly about established
findings; hedge only the uncertain inferences.

Before: "These results, which may suggest X, are possibly consistent with the
hypothesis that Y could occur, and may indicate that Z is involved."
After: "These results are consistent with [established finding X]. Whether Y occurs
under physiological conditions remains unclear."

---

## Group H: Nature/Science-Specific AI Patterns (Rules 30–36)

**30. "Here we show/report/describe" overuse**

"Here we show that..." is a valid Nature framing — used once, in the abstract or at
the central finding statement in the Introduction. AI uses it as a sentence opener
for every finding.

Before: "Here we show that mTOR regulates autophagy. Here we report that FOXO3 is
required for this process. Here we demonstrate that pharmacological inhibition
recapitulates the phenotype."
After: State findings directly. One "Here we show" in the abstract is acceptable.

**31. Meta-references to the paper's own sections**

Remove: "In the Introduction, we...," "In the Methods section, we...," "The Results
show that...," "In the Discussion, we argue that..."

Scientific manuscripts do not narrate their own structure.

**32. Significance framing in every Discussion paragraph**

AI-written Discussions end every paragraph with a sentence about the field
implications. This produces a Discussion that reads as a press release rather than
a scientific argument.

The Discussion should build one argument across paragraphs. One central implication
at the end of the Discussion — not five separate significance claims in five
paragraphs.

**33. Rigid Discussion structure: restate → interpret → cite → imply**

LLMs repeat the same paragraph template throughout the Discussion. Vary: sometimes
open with the comparison to prior literature, then introduce your result as a
contrast. Sometimes start with the limitation and work toward the implication.
The reader should not be able to predict the next sentence's grammatical role.

**34. Narrating figure content sentence by sentence**

Before: "As shown in Figure 3a, treatment significantly reduced tumor volume.
Figure 3b demonstrates that this effect was dose-dependent. Figure 3c shows the
immunohistochemical staining."
After: "Treatment reduced tumor volume in a dose-dependent manner (Fig. 3a–c)."

Reference figures parenthetically. Do not open sentences with "As shown in Figure X"
or "Figure X demonstrates that."

**35. "In this study/work/paper/report" as the subject**

Before: "In this study, we investigated the role of AMPK in autophagy."
After: "We investigated whether AMPK regulates autophagy."
Or, lead with the gap: "AMPK's role in initiating autophagy is not known."

**36. Abstract sentences all beginning with "We"**

AI abstracts: "We found X. We show Y. We demonstrate Z. We conclude W."
Vary: "X was identified. Y is consistent with Z. Our findings therefore suggest W."

---

## Group I: Word Choice Patterns (Rules 37–43)

**37. "linked to" → "associated with"**

"Linked to" is informal. Use "associated with," "correlated with," or "related to."

Before: "Obesity has been linked to increased cancer risk."
After: "Obesity has been associated with increased cancer risk."

**38. "Beyond X" as transition → "In addition to X"**

"Beyond" as a transitional connector is journalistic. Replace with "In addition to,"
"Apart from," or restructure.

Before: "Beyond the cardiovascular benefits, SGLT2 inhibitors also reduce renal
fibrosis."
After: "In addition to their cardiovascular effects, SGLT2 inhibitors reduce renal
fibrosis."

**39. "via" → "through" or "by"**

"Via" is Latin shorthand. In formal academic prose, "through" or "by" is more
natural.

Before: "Informed consent was obtained via an online form."
After: "Informed consent was obtained through an online form."
Exception: "via" is acceptable when it is the established convention in a specific
subfield (e.g., "delivered via AAV vector").

**40. "where" as a non-locative connector → restructure**

LLMs use "where" to attach elaborating clauses to non-spatial antecedents.

Before: "The effect was strongest in older patients, where sample sizes were also
largest."
After: "The effect was strongest in older patients, among whom sample sizes were
also largest." Or: "The effect was strongest in older patients; this subgroup also
had the largest sample sizes."

Prefer "with," "among whom," or a new sentence over "in which" (also overused by AI).
Only keep "where" for genuine physical locations, datasets, or conditional contexts.

**41. "yield" as a result verb → specific verb**

Before: "The analysis did not yield significant results."
After: "The analysis did not produce significant associations."
Or: "The analysis returned no significant results."
Reserve "yield" for chemical or biochemical yield contexts.

**42. "A number of" → specific number or "several"**

Before: "A number of studies have investigated this pathway."
After: "Several studies have examined this pathway." Or: "Fourteen studies have
examined this pathway."

**43. "It should be noted" / "It is important to note" / "It is worth noting" → cut**

These are filler. The sentence that follows does not need an announcement.

Before: "It is important to note that the sample was limited to women aged 18–45."
After: "The sample was limited to women aged 18–45."

---

## Group J: Classical Academic Vocabulary Restoration (Rule 44)

**44. Restore classical academic phrasing**

LLMs have drifted from classical academic vocabulary. Restoring these makes
scientific writing sound researcher-written, not model-generated. This is the
counterpart to Group C (AI vocabulary to remove).

| AI version | Restore to |
|---|---|
| proportion of | percentage of |
| aim of (the study) | purpose of (the study) |
| was assessed | was measured |
| With regard to | With respect to |
| to elucidate | to determine |
| a growing body of research | a growing number of studies |
| These findings suggest | The results suggest |
| ultimately (sentence-end) | after all (sentence-end) |
| First (sentence-initial discourse marker) | To begin with |
| We hypothesized that X | We tested the hypothesis that X |
| concern (meaning "serious problem") | problem |

**Structural restorations:**

- Nominalization restoration: "We hypothesized that X" → "We tested the hypothesis
  that X" (restores the classical noun form of academic argumentation)
- Adverbialization restoration: "A clear dose-response relationship was observed"
  → "The dose-response relationship was clearly observed"

Apply in formal contexts (Introduction, Discussion). Consider rhythm and nearby
repetition before each swap. Do not apply mechanically.

---

## Group K: Parallelism and List Patterns (Rules 45–48)

**45. Kill negative parallelism openers**

"Not only X but also Y," "It is not just about X; it is Y," "It is not merely X;
it represents Y" usually say the same thing twice.

Before: "SGLT2 inhibitors not only lower blood glucose but also reduce cardiovascular
events."
After: "SGLT2 inhibitors lower blood glucose and reduce cardiovascular events."

**46. Kill false range constructions**

"From X to Y" when X and Y are not on a meaningful scale creates an illusion of
comprehensiveness.

Before: "The benefits span from improved renal function to enhanced cardiac outcomes,
from better glycemic control to reduced hospitalization."
After: "SGLT2 inhibitors reduce hospitalization for heart failure, slow kidney
disease progression, and lower HbA1c."

**47. Kill rule-of-three padding**

AI forces triads even when content has two or four items. Use the natural number.
Replace adjective triplets with actual data wherever possible.

**48. Kill synonym cycling**

AI substitutes synonyms for the same referent: "patients... participants... subjects
... individuals..." Pick one term and use it throughout a section.

---

## Group L: Sentence and Paragraph Architecture (Rules 49–53)

**49. Vary sentence length deliberately**

After two long sentences, insert a short one. A 5-word sentence after 50 words is
among the most human things you can do in a scientific paragraph.

**50. Do not open every paragraph with the broadest generalization**

AI paragraphs begin with the most general statement, then narrow. Sometimes start
specific and broaden; start with a contrast; or continue from the prior paragraph's
most specific point.

**51. Do not summarize at paragraph ends**

AI closes paragraphs by restating what was just said. Replace closing summaries with:
- A forward-pointing statement (what question this raises)
- The most specific and concrete implication
- A contrast with the prior literature
- The limitation that most directly bounds this result

**52. Remove "In conclusion" / "In summary" as section openers**

In Nature/Science, the Discussion does not end with a labeled conclusion paragraph.
Remove the opener, or rephrase to begin directly with the key claim.

Before: "In conclusion, our findings demonstrate that AMPK regulates autophagy."
After: "AMPK regulates autophagy in response to nutrient limitation. This mechanism
may explain..."

**53. Remove signposting and meta-announcements**

Remove: "Here, we will discuss...", "In this section, we examine...", "We now turn
to...", "Having established X, we next investigate Y."

Start the next point directly. Let section headings do the navigation work.

---

## Section-Specific Guidance

### Abstract
- Every sentence carries concrete information: what was done, what was found (with
  numbers), what it means.
- Opening sentence: the specific problem or gap, in one sentence. No broad context.
- "Here we show" is acceptable once, for the central finding.
- Last sentence: specific implication — not "further studies are warranted."
- No filler. No sentence that restates the preceding sentence.
- No hedging on directly measured results; hedge only mechanistic inferences.

### Introduction
- Research gap must be specific and concrete, not gestural ("remains poorly
  understood").
- Do not open with sweeping statements about the importance of the field.
- Do not use "In this study, we investigated..."
- End with what this paper does: "We show that X regulates Y through Z."

### Methods
- **Preserve passive voice. Do not convert to active.**
- Remove filler: "In order to assess...," "It was decided to...," "Due to the fact
  that..."
- Keep: all passive constructions, technical abbreviations, standard procedural
  language, manufacturer specifications.

### Results
- Every sentence anchored to data. No interpretive statements.
- "Significantly" requires a P-value in the same sentence or in parentheses.
- Do not narrate figure content sentence by sentence. Reference figures
  parenthetically.
- Remove "As shown in Figure X" openers. State the result; cite the figure in
  parentheses.
- No redundant hedging on direct measurements. Reserve hedging for inference.

### Discussion
- Open with interpretation, not a restatement of results.
- Structure: interpretation → comparison to prior work → mechanistic inference
  (hedged) → limitation → implication.
- Not every paragraph closes with a significance statement.
- End with your most specific, grounded, forward-looking statement — not "further
  studies are needed to fully elucidate the complex mechanisms underlying..."
- Reserve "To summarize" or equivalent for the final paragraph only, or cut it
  entirely.

---

## Voice in Scientific Writing

Voice does not mean casual language. It means:

- **Reasoning sounds like a specific researcher's**, not like a template.
- **Interpretations reflect genuine engagement with the data**: acknowledging what
  the data do not show, flagging the most important limitation, comparing to specific
  named prior findings rather than "the literature."
- **Appropriate confidence**: direct about well-supported findings, hedged about
  inference.
- **Rhythm varies**: not every sentence 20–25 words.
- **The unexpected is foregrounded**: if a result was surprising, say so directly
  and explain why.

**Academic voice checklist (apply after Step 2):**
- [ ] Does the text sound like a specific person interpreted these data?
- [ ] Is there at least one moment of acknowledged uncertainty beyond boilerplate
      hedging?
- [ ] Do sentences vary in length? (If three consecutive sentences are within 3
      words of each other in length, vary one.)
- [ ] Is every comparison to prior work specific (author, year, finding)?
- [ ] Does the Discussion open with interpretation, not a restatement of results?
- [ ] Does the abstract give the key result as a number?
- [ ] Are there any remaining abstract noun subjects ("This finding suggests...")?

---

## Output Format

```
### Diagnosis
- "exact phrase" — Group [letter], Rule [number]: [short explanation]
(List all violations found before revising.)

### Revised Text
[revised text — every flagged item addressed; meaning preserved exactly]

### Changes
- [5–8 concise items: specific phrase → replacement, with the rule that drove it]
- Em dashes: [N found] → 0

### Structural Notes (if structural pass was applied)
- [2–3 observations about sentence architecture changes made]
```

If the user requests only the revised text, skip all sections except Revised Text.
Still perform the full diagnosis and structural pass internally — just do not display
them.

---

## Complete Example

**Before (AI-generated scientific abstract):**
> Here we show that mitophagy plays a pivotal role in the evolving landscape of
> neurodegenerative disease. This groundbreaking study demonstrates that PINK1-
> mediated mitophagy, a crucial cellular process, serves as a vital mechanism for
> maintaining neuronal homeostasis — underscoring the fundamental importance of
> mitochondrial quality control. Our findings highlight the key interplay between
> mitophagy and apoptosis, showcasing how these pathways intersect, contributing to
> cell survival. These results provide valuable insights and pave the way for novel
> therapeutic strategies that may potentially have the capacity to transform the
> treatment landscape.

**Diagnosis:**
- "plays a pivotal role in the evolving landscape" — Group B, Rule 5: significance filler + abstract landscape
- "groundbreaking study" — Group B, Rule 6: self-promotion
- "a crucial cellular process" — Group C, Rule 11/12: AI vocabulary (crucial)
- "serves as a vital mechanism" — copula avoidance (serves as) + significance filler (vital)
- "— underscoring the fundamental importance of" — Group E, Rule 15: em dash + Group B, Rule 5: filler
- "highlight the key interplay" — Group C, Rule 11: tier 1 AI vocabulary (highlight, interplay, key)
- "showcasing how these pathways intersect, contributing to" — Group D, Rule 14: decorative -ing phrases
- "provide valuable insights" — Group B, Rule 5: significance filler
- "pave the way for novel therapeutic strategies" — Group B, Rules 5, 9: significance filler + self-claimed novelty
- "may potentially have the capacity to" — Group G, Rule 26: multi-layer hedging
- "transform the treatment landscape" — Group B, Rule 6: promotional; Group C: landscape

**Revised Text:**
> PINK1-mediated mitophagy is required for neuronal survival under conditions of
> mitochondrial stress. In mice lacking PINK1, dopaminergic neurons accumulated
> damaged mitochondria and showed a 3-fold increase in apoptosis compared with
> wild-type controls (P < 0.001). Activating mitophagy pharmacologically reduced
> neuronal loss by 60% in a rotenone model of Parkinson's disease. These results
> identify mitophagy as a potential target for neuroprotective therapy.

**Changes:**
- Removed "pivotal role in the evolving landscape" → stated the specific function directly (Rules 5, 11)
- Removed "groundbreaking" and "serves as a vital mechanism" → factual description (Rules 6, 8)
- Eliminated em dash after "homeostasis" → restructured as separate sentence (Rule 15)
- Removed "highlight the key interplay... showcasing... contributing to" → stated the relationship directly (Rules 14, 11)
- Reduced "may potentially have the capacity to transform" → cut entirely; replaced with specific quantitative claim (Rules 9, 26)
- Em dashes: 1 found → 0
- Added specific data (3-fold increase, 60% reduction, P < 0.001) to replace all vague claims

---

## Sources

Synthesized from:
- Wikipedia: [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) (CC BY-SA 4.0)
- Kobak et al. (2025), Liang et al. (2024), Juzek & Ward COLING (2025): LLM detection research
- Nature and Science journal style guides and editorial conventions
- humanizer v2.5.1 (Wikipedia-based general humanizer)
- sci-humanizer v1.0 (academic prose refinement, 49 rules)
- slopbuster v1.0.0 (multi-modal AI humanizer with academic mode)
- humanizer_academic v1.2.0 (medical writing adaptation with classical vocabulary restoration)

Calibrated for PhD-level writing in the natural sciences at Nature/Science standards.
