# DeepL Glossary Generation Prompt

Use this prompt with an AI assistant to generate a DeepL glossary TSV file for a new target language. Replace `[LANGUAGE]` and `[CODE]` with the target language (e.g., "Spanish", "es").

---

## The Prompt

```
I need you to create a DeepL glossary (TSV format) for translating English → [LANGUAGE] in the context of a Christian missions website focused on prayer for unreached people groups.

## Context

This glossary is for Doxa.Life, a website by the World Assemblies of God Fellowship (WAGF) that mobilizes daily prayer for unengaged unreached people groups (UUPGs). DeepL translates both:
- **Prayer content**: daily devotional/prayer material about specific people groups
- **Marketing website**: the public-facing site explaining the mission, vision, and how to participate

The glossary must work naturally in both narrative prose and UI/marketing copy.

## Output format

Plain TSV (tab-separated), one entry per line: `english_term[TAB]target_term`. No headers. Save as `[CODE].tsv`.

## Key decisions already made (apply to all languages)

1. **"People group" = technical term.** Translate as the equivalent of "ethnic group" in the target language — NOT as a generic "group of people." This is the most important term on the site. It refers to a specific ethnolinguistic unit, and using a generic translation undermines every statistic and the entire mission.

2. **Compound terms (unreached, unengaged, sub-, self-, etc.) must follow the target language's standard conventions** for prefixes and compound modifiers (e.g., hyphenation in French, no hyphen for "sub-" in Spanish). Be consistent throughout — apply the same pattern to all similar terms.

3. **Biblical phrases must use a single, consistent conjugation style** across the entire glossary. For languages with formal/informal or regional verb forms (e.g., Spanish vosotros vs ustedes), pick the most accessible form for a global audience and use it everywhere. Look up established phrasing from a widely used Bible translation, but prioritize missiological precision and ease of understanding over strict alignment with any one version. Prefer modern, accessible vocabulary over archaic terms.

4. **Verbs should be in infinitive form** so DeepL can conjugate based on context. Exception: biblical imperative quotes that are fixed phrases (e.g., "pray without ceasing" is always imperative).

5. **The five "selfs" need adjective forms**, not noun forms. They describe a church: "a self-propagating church," "a self-governing church," etc.

6. **"Heart language" means "mother tongue"** — the language a person thinks and feels in most deeply. Use the natural target-language term for mother tongue, not a literal translation of "heart language."

7. **"Adopt" is used in a missions context** — a church committing to pray for, fund, and send workers to a people group. Be aware of family-law adoption connotations in the target language.

8. **Proper nouns stay untranslated:** DOXA, WAGF, WAGF Missions Commission.

9. **"Culturally appropriate" needs an adjective form** that works in any sentence position (not a prepositional phrase).

10. **Same-word entries** (where the English and target language are identical, like "disciple" in French) — include them only if there's a real risk of DeepL choosing a wrong synonym.

11. **Capitalize "the Gospel"** according to the target language's convention for referring to the Christian message. Some languages capitalize it (French "l'Évangile", Spanish "el Evangelio"), others may not. Follow what is standard in Christian publishing for the target language.

12. **Distinguish similar terms.** Several English terms are close in meaning (e.g., "self-supporting" vs "self-sustaining", "engagement" vs "fruitful engagement"). Ensure each gets a clearly distinct translation — do not let two different source terms collapse into the same or nearly identical target term.

## Source terms

Extract all English source terms from these two reference files:

1. **`i18n/glossary-candidates-ai.md`** — the master glossary with definitions, site examples, and translation guidance for every term. Generate a translation for every term listed in this document.
2. **`i18n/glossaries/fr.tsv`** — the French reference implementation. Use this as a structural template: your output should cover the same terms in the same TSV format.

## Validation checklist

Before finalizing, verify each entry against these checks:

1. **"People group" test**: Does your translation clearly mean "ethnic group," not "group of people"?
2. **Context test**: Read each translation in the example sentence from the glossary source document. Does it sound natural?
3. **Adjective test**: Do the five selfs and "culturally appropriate" work as adjectives modifying a noun?
4. **Bible conjugation test**: Do ALL biblical imperative phrases use the same verb form (e.g., all ustedes, or all vous)? No mixing.
5. **Modern vocabulary test**: Would a young adult in the target language understand every word without a dictionary? Replace archaic terms.
6. **Verb form test**: Are standalone verbs in infinitive form (not conjugated)?
7. **Prefix/compound test**: Are all prefixes (non-, sub-, auto-, self-) handled consistently following the target language's conventions?
8. **Uniqueness test**: Scan for any two entries that have the same or nearly identical target translation. Each English term must map to a distinct target term.
9. **Capitalization test**: Is "the Gospel" capitalized? Does it match the French reference?
10. **Connotation test**: Does "adopt" avoid family-law connotations? Does "indigenous" avoid political connotations where problematic? Does "frontier" avoid military connotations?

## Reference

The full glossary source with definitions, site examples, and translation guidance is in `i18n/glossary-candidates-ai.md`. The French glossary (`i18n/glossaries/fr.tsv`) serves as a reference implementation.
```

---

## Usage notes

- For each new language, also specify which Bible translation to align with (check `config/languages.ts` for the `bibleId` field)
- After generating, have a native speaker in missions review the people-group terminology specifically
- The French glossary (`fr.tsv`) is the reference implementation — share it alongside this prompt for additional context
