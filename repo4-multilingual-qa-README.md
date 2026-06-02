# Multilingual AI QA Toolkit

Standards, checklists, and reference guides for evaluating AI model outputs across languages — with a focus on linguistic accuracy, cultural alignment, and cross-language consistency.

Developed from operational experience evaluating frontier LLMs in English, Russian, Spanish, Chinese, and Portuguese across consumer and enterprise AI products.

---

## What This Is

Multilingual AI evaluation is not translation review. It requires assessing whether a model:

- Produces outputs that are **linguistically natural** in the target language (not translated-sounding)
- Reflects **cultural context** appropriately for the target market
- Maintains **consistent quality** across languages — not just in the dominant training language
- Avoids **cross-language bias** where the model performs significantly better in some languages than others

This toolkit provides the practical standards for that work.

---

## Repository Structure

```
multilingual-ai-qa-toolkit/
│
├── annotation-standards/
│   ├── linguistic-accuracy-guide.md    # What "native-level" actually means in annotation
│   ├── cultural-alignment-checklist.md # Culture-specific evaluation criteria
│   └── cross-language-consistency.md  # Comparing quality across language variants
│
├── bias-review/
│   ├── language-bias-detection.md      # Identifying performance gaps by language
│   └── demographic-bias-checklist.md  # Evaluating outputs for group-level fairness
│
├── language-guides/
│   ├── russian-eval-notes.md           # Russian-specific evaluation considerations
│   ├── spanish-latam-eval-notes.md     # LATAM Spanish vs. Castilian differences
│   └── multilingual-common-errors.md  # Errors that appear specifically in non-EN outputs
│
└── templates/
    ├── multilingual-eval-scorecard.md
    └── lqa-review-template.md
```

---

## Why Multilingual Evaluation is Different

### The core problem: Training data imbalance

Most frontier LLMs are trained predominantly on English data. This creates systematic quality gaps:

- Factual accuracy is often lower in non-English languages
- Reasoning chains are more likely to contain errors when produced in lower-resource languages
- Cultural references default to Western, often American, perspectives regardless of the target language
- Idiomatic language is frequently replaced with technically correct but unnatural phrasing

**Consequence:** A model that scores well on English benchmarks may perform significantly worse on equivalent tasks in Russian or Spanish. Standard evaluation pipelines that only sample English outputs will miss this entirely.

---

## Linguistic Accuracy: What "Native-Level" Means

Native-level quality is not the same as grammatically correct. An output can be grammatically perfect and still fail native-level evaluation.

### Evaluation criteria beyond grammar

**1. Idiomatic naturalness**
Does the phrasing sound like something a native speaker would actually say?

*Example (Russian):*
- Grammatically correct but unnatural: *"Я нахожусь в процессе изучения данного вопроса"*
- Natural: *"Я разбираюсь в этом вопросе"*

**2. Register consistency**
Does the formality level remain consistent throughout the response, and is it appropriate for the context?

**3. Cultural framing**
Does the response use references, examples, and analogies that are meaningful in the target culture?

*Example:*
A financial explanation for a LATAM Spanish audience should reference regional market conditions and regulatory contexts, not default to US-centric examples.

**4. Absence of translationese**
Translationese refers to phrasing that reveals the model is working from an underlying English structure — correct in the target language but revealing its origin.

Common signs: unusual word order, calque expressions (direct structural translations), unnaturally long sentences that would be split in native writing.

---

## Cross-Language Consistency Evaluation

When a model is deployed multilingually, users in different languages should receive equivalent quality. This requires explicit cross-language comparison.

### Protocol

1. Select a sample of 20–50 prompts from your evaluation set
2. Run each prompt in all target languages
3. Score each output independently using the standard rubric
4. Calculate mean scores per language
5. Flag any language where mean scores differ by more than 0.5 points on a 4-point scale

**If a gap exists:**
- Identify whether it is systematic (affects all output types) or categorical (affects specific domains or task types)
- Document with examples for model training feedback
- Recommend targeted data augmentation in the underperforming language

---

## Bias Review

### Language-level bias

Language-level bias occurs when a model systematically produces lower-quality, less accurate, or less helpful outputs for users of specific languages.

**Detection approach:**
- Run equivalent prompts across languages
- Flag cases where the model provides more caveats, shorter responses, or less confident answers in non-English languages without justification
- Identify cases where the model switches languages mid-response (often a sign of training data gaps)

### Demographic and cultural bias

**Checklist for evaluating cultural representation:**
- [ ] Does the response use demographically neutral examples when no specific group is referenced?
- [ ] Does the response avoid associating specific attributes with nationalities, ethnicities, or language groups?
- [ ] When describing professions, does the response avoid gendered assumptions?
- [ ] Does the response treat regional variants (e.g., LATAM Spanish vs. Castilian) with equal validity?
- [ ] Does the response avoid presenting Western norms as universal defaults?

---

## Russian Evaluation: Key Considerations

**Grammar pitfalls to watch:**
- Aspect usage (perfective vs. imperfective verb forms)
- Case agreement in complex noun phrases
- Correct use of animate/inanimate accusative

**Cultural alignment:**
- Formality defaults: Russian professional communication is generally more formal than English equivalents
- Direct vs. indirect communication norms differ from English
- References to geography, history, and institutions should reflect the regional context of the intended user

**Common model errors in Russian:**
- Overuse of formal bureaucratic constructions in contexts that call for plain language
- Inconsistent use of *ты* vs. *вы* (informal vs. formal address) within the same response
- Calque translations of English idioms that do not exist in native Russian usage

---

## Spanish (LATAM) Evaluation: Key Considerations

**Regional variation:**
- Vocabulary differences between LATAM variants and Castilian are significant (e.g., *computadora* vs. *ordenador*, *celular* vs. *móvil*)
- Voseo (*vos* + conjugation) is standard in Argentina and Uruguay; models often default to tuteo
- Legal and financial terminology varies by country

**Cultural alignment:**
- Business communication in LATAM tends toward more relational framing than direct task-focus
- References to local institutions, regulatory bodies, and market structures should be country-specific where relevant

---

## Related Repositories

- [llm-evaluation-framework](https://github.com/ilya-garaeff/llm-evaluation-framework)
- [prompt-engineering-playbook](https://github.com/ilya-garaeff/prompt-engineering-playbook)
- [rag-ops-notes](https://github.com/ilya-garaeff/rag-ops-notes)

---

*Maintained by [Ilya Garaeff](https://ilyagaraeff.com) — AI/ML Operations Specialist*  
*Native: Russian · Fluent: English, Spanish · Working: Chinese, Portuguese*
