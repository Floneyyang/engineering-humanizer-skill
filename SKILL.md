---
name: engineering-humanizer-skill
description: Humanize software-engineering writing and improve repository-aware code without changing technical meaning. Use for pull requests, commits, documentation, design notes, incident reports, code comments, reviews, tests, and source code. Preserve technical tokens, evidence, uncertainty, and compatibility claims.
---

# Engineering Humanizer

Edit software-engineering prose and code so it reads like deliberate work by an engineer who understands the repository. Remove generic AI patterns while preserving technical meaning, evidence, uncertainty, and project conventions. Use the patterns as editing heuristics, never as proof of authorship.

This skill adapts [blader/humanizer](https://github.com/blader/humanizer), which is based on Wikipedia's "Signs of AI writing", and extends it with engineering-specific guidance and additional writing observations.

## Your Task

When given text to humanize:

1. **Identify AI patterns** - Scan for the patterns listed below.
2. **Preserve the information, not the shape** - Every claim in the original survives into the rewrite, but depth doesn't have to be uniform: compress the dull parts, dwell where a human would, and merge or split paragraphs freely. When keeping the information and mirroring the original's structure pull in different directions, the information wins.
3. **Never invent facts** - Do not add facts, names, numbers, dates, quotes, citations, behavior, causes, benchmarks, test results, guarantees, requirements, compatibility claims, or implementation details absent from the source or verified repository context. Preserve distinctions between confirmed facts, hypotheses, and open questions.
4. **Protect technical tokens** - Preserve identifiers, symbols, code spans, commands, paths, URLs, versions, error messages, configuration keys, and literal output exactly unless the user asks to change them.
5. **Match the voice and repository** - Fit the intended tone and the project's established terminology. A supplied writing sample or repository style outranks generic preferences when it does not conflict with correctness.

## Classify the artifact

Identify the artifact before editing:

- **Pull request:** Explain what changed, why, important choices, risks, and stated verification.
- **Commit message:** Use the project's convention. State the change concretely; use the body for motivation or constraints.
- **Documentation:** Describe current behavior. Keep history only when readers need it.
- **Code comment:** Explain intent, invariants, edge cases, external constraints, or surprising behavior. Do not narrate syntax.
- **Code review:** Name the problem, consequence, and practical correction.
- **Incident report:** Preserve timestamps, impact, evidence, uncertainty, and the boundary between causes and hypotheses.
- **Design document:** State goals, non-goals, constraints, alternatives, and tradeoffs. Preserve unresolved decisions.
- **Changelog or migration guide:** Preserve versions, compatibility boundaries, and required commands.
- **Source code:** Improve correctness, maintainability, and repository fit. Do not rewrite code merely to make it look human.
- **Mixed artifact:** Protect code blocks, structured data, link targets, and literal output while editing prose.

## Voice Calibration

If the user provides a writing sample (their own previous writing), analyze it before rewriting:

1. Read the sample first. Note its sentence lengths, vocabulary, paragraph openings, punctuation, recurring phrases, and transitions.
2. Match those habits instead of merely deleting AI patterns. Do not upgrade casual words or regularize deliberate quirks.
3. Without a sample, use the default behavior below.

A sample outranks generic style preferences, including punctuation frequency, but never outranks technical correctness or explicit project conventions. Matching the author beats scrubbing an isolated tell.

## PERSONALITY AND SOUL

Avoiding AI patterns is only half the job. Sterile, voiceless writing is just as obvious as slop. Good writing has a human behind it.

**Apply this section only when the content and author's voice call for it** - blog posts, essays, opinions, retrospectives, and informal communication. For API references, runbooks, legal text, and neutral technical documentation, plain precision is the correct human voice. Do not inject opinions or first person.

When voice is appropriate, avoid uniform sentence structures, bloodless neutrality, and perfect organization. Let the writer have opinions, uncertainty, mixed feelings, humor, asides, and uneven rhythm. Never add factual claims to create that personality.

## CONTENT PATTERNS

### 1. Undue Emphasis on Significance, Legacy, and Broader Trends

**Words to watch:** stands/serves as, is a testament/reminder, a vital/significant/crucial/pivotal/key role/moment, underscores/highlights its importance/significance, reflects broader, symbolizing its ongoing/enduring/lasting, contributing to the, setting the stage for, marking/shaping the, represents/marks a shift, key turning point, evolving landscape, focal point, indelible mark, deeply rooted
**Problem:** LLM writing puffs up importance by adding statements about how arbitrary aspects represent or contribute to a broader topic.
**Before:**
> The Statistical Institute of Catalonia was officially established in 1989, marking a pivotal moment in the evolution of regional statistics in Spain. This initiative was part of a broader movement across Spain to decentralize administrative functions and enhance regional governance.
**After:**
> The Statistical Institute of Catalonia was established in 1989, part of a wider decentralization of administrative functions in Spain.

### 2. Undue Emphasis on Notability and Media Coverage

**Words to watch:** independent coverage, local/regional/national media outlets, written by a leading expert, active social media presence
**Problem:** LLMs hit readers over the head with claims of notability, often listing sources without context.
**Before:**
> Her views have been cited in The New York Times, BBC, Financial Times, and The Hindu. She maintains an active social media presence with over 500,000 followers.
**After:**
> Her views have been cited in The New York Times and the BBC.

(If the source gives real context for one citation, what she said and where, keep that one and drop the rest of the list. Don't invent the context to make the trimmed version sound better.)

### 3. Superficial Analyses with -ing Endings

**Words to watch:** highlighting/underscoring/emphasizing..., ensuring..., reflecting/symbolizing..., contributing to..., cultivating/fostering..., encompassing..., showcasing...
**Problem:** AI chatbots tack present participle ("-ing") phrases onto sentences to add fake depth.
**Before:**
> The temple's color palette of blue, green, and gold resonates with the region's natural beauty, symbolizing Texas bluebonnets, the Gulf of Mexico, and the diverse Texan landscapes, reflecting the community's deep connection to the land.
**After:**
> The temple is painted blue, green, and gold, colors meant to evoke Texas bluebonnets and the Gulf of Mexico.

### 4. Promotional and Advertisement-like Language

**Words to watch:** boasts a, vibrant, rich (figurative), profound, enhancing its, showcasing, exemplifies, commitment to, natural beauty, nestled, in the heart of, groundbreaking (figurative), renowned, breathtaking, must-visit, stunning
**Problem:** LLMs have serious problems keeping a neutral tone, especially for "cultural heritage" topics.
**Before:**
> Nestled within the breathtaking region of Gonder in Ethiopia, Alamata Raya Kobo stands as a vibrant town with a rich cultural heritage and stunning natural beauty.
**After:**
> Alamata Raya Kobo is a town in the Gonder region of Ethiopia.

### 5. Vague Attributions and Weasel Words

**Words to watch:** Industry reports, Observers have cited, Experts argue, Some critics argue, several sources/publications (when few cited)
**Problem:** AI chatbots attribute opinions to vague authorities without specific sources.
**Before:**
> Due to its unique characteristics, the Haolai River is of interest to researchers and conservationists. Experts believe it plays a crucial role in the regional ecosystem.
**After:**
> Researchers and conservationists study the Haolai River for its unusual characteristics.

(If a real source exists, name it. Never invent one to make a sentence sound sourced; an unsupported claim gets cut, not decorated.)

### 6. Outline-like "Challenges and Future Prospects" Sections

**Words to watch:** Despite its... faces several challenges..., Despite these challenges, Challenges and Legacy, Future Outlook
**Problem:** Many LLM-generated articles include formulaic "Challenges" sections.
**Before:**
> Despite its industrial prosperity, Korattur faces challenges typical of urban areas, including traffic congestion and water scarcity. Despite these challenges, with its strategic location and ongoing initiatives, Korattur continues to thrive as an integral part of Chennai's growth.
**After:**
> Korattur has recurring traffic congestion and water shortages.

(The specifics you'd want here, like when the congestion worsened or what the city did about it, come from sources or the user, not from the rewrite.)

## LANGUAGE AND GRAMMAR PATTERNS

### 7. Overused "AI Vocabulary" Words

**High-frequency AI words:** Actually, additionally, align with, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate/intricacies, key (adjective), landscape (abstract noun), pivotal, showcase, tapestry (abstract noun), testament, underscore (verb), valuable, vibrant
**Problem:** These words appear far more frequently in post-2023 text. They often co-occur.
**Before:**
> Additionally, a distinctive feature of Somali cuisine is the incorporation of camel meat. An enduring testament to Italian colonial influence is the widespread adoption of pasta in the local culinary landscape, showcasing how these dishes have integrated into the traditional diet.
**After:**
> Somali cuisine also includes camel meat, which is considered a delicacy. Pasta dishes, introduced during Italian colonization, remain common, especially in the south.

### 8. Avoidance of "is"/"are" (Copula Avoidance)

**Words to watch:** serves as/stands as/marks/represents [a], boasts/features/offers [a]
**Problem:** LLMs substitute elaborate constructions for simple copulas.
**Before:**
> Gallery 825 serves as LAAA's exhibition space for contemporary art. The gallery features four separate spaces and boasts over 3,000 square feet.
**After:**
> Gallery 825 is LAAA's exhibition space for contemporary art. The gallery has four rooms totaling 3,000 square feet.

### 9. Negative Parallelisms and Tailing Negations
**Problem:** Constructions like "Not only...but..." or "It's not just about..., it's..." are overused. So are clipped tailing-negation fragments such as "no guessing" or "no wasted motion" tacked onto the end of a sentence instead of written as a real clause.
**Before:**
> It's not just about the beat riding under the vocals; it's part of the aggression and atmosphere. It's not merely a song, it's a statement.
**After:**
> The heavy beat adds to the aggressive tone.
**Before (tailing negation):**
> The options come from the selected item, no guessing.
**After:**
> The options come from the selected item without forcing the user to guess.

### 10. Rule of Three Overuse
**Problem:** LLMs force ideas into groups of three to appear comprehensive.
**Before:**
> The event features keynote sessions, panel discussions, and networking opportunities. Attendees can expect innovation, inspiration, and industry insights.
**After:**
> The event includes talks and panels. There's also time for informal networking between sessions.

### 11. Elegant Variation (Synonym Cycling)
**Problem:** AI has repetition-penalty code causing excessive synonym substitution.
**Before:**
> The protagonist faces many challenges. The main character must overcome obstacles. The central figure eventually triumphs. The hero returns home.
**After:**
> The protagonist faces many challenges but eventually triumphs and returns home.

### 12. False Ranges
**Problem:** LLMs use "from X to Y" constructions where X and Y aren't on a meaningful scale.
**Before:**
> Our journey through the universe has taken us from the singularity of the Big Bang to the grand cosmic web, from the birth and death of stars to the enigmatic dance of dark matter.
**After:**
> The book covers the Big Bang, star formation, and current theories about dark matter.

### 13. Passive Voice and Subjectless Fragments
**Problem:** LLMs often hide the actor or drop the subject entirely. Rewrite these when naming the actor improves clarity. Keep passive voice when the actor is unknown, irrelevant, or intentionally de-emphasized, as in incident and security reporting.
**Before:**
> No configuration file needed. The results are preserved automatically.
**After:**
> You do not need a configuration file. The system preserves the results automatically.

## STYLE PATTERNS

### 14. Mechanical Punctuation

**Problem:** AI drafts may lean on em dashes, en dashes, parentheses, colons, or double hyphens as a repeated rhythm rather than for meaning. Do not ban punctuation mechanically. Match the author's sample and repository style, and replace punctuation only when a period, comma, or rewritten sentence is clearer.

An isolated em dash is not evidence of AI writing. Flag clusters of formulaic punctuation and cadence, not a character by itself.

### 15. Overuse of Boldface
**Problem:** AI chatbots emphasize phrases in boldface mechanically.
**Before:**
> It blends **OKRs (Objectives and Key Results)**, **KPIs (Key Performance Indicators)**, and visual strategy tools such as the **Business Model Canvas (BMC)** and **Balanced Scorecard (BSC)**.
**After:**
> It blends OKRs, KPIs, and visual strategy tools like the Business Model Canvas and Balanced Scorecard.

### 16. Inline-Header Vertical Lists
**Problem:** AI outputs lists where every item uses the same bold-label-plus-colon template whether or not the structure helps. Keep lists, tables, and bold labels when engineers need to scan steps, risks, options, requirements, or results. Convert them only when prose communicates the relationship better.
**Before:**
> - **User Experience:** The user experience has been significantly improved with a new interface.
> - **Performance:** Performance has been enhanced through optimized algorithms.
> - **Security:** Security has been strengthened with end-to-end encryption.
**After:**
> The update improves the interface, speeds up load times through optimized algorithms, and adds end-to-end encryption.

### 17. Title Case in Headings
**Problem:** AI chatbots capitalize all main words in headings.
**Before:**
> ## Strategic Negotiations And Global Partnerships
**After:**
> ## Strategic negotiations and global partnerships

### 18. Emojis
**Problem:** AI chatbots may decorate headings or bullet points with emojis mechanically. Keep emojis when they match the author's established informal voice or carry a recognized team meaning; remove ornamental or inconsistent use.
**Before:**
> 🚀 **Launch Phase:** The product launches in Q3
> 💡 **Key Insight:** Users prefer simplicity
> ✅ **Next Steps:** Schedule follow-up meeting
**After:**
> The product launches in Q3. User research showed a preference for simplicity. Next step: schedule a follow-up meeting.

### 19. Curly Quotation Marks
**Problem:** ChatGPT uses curly quotes (“...”) instead of straight quotes ("...").
**Before:**
> He said “the project is on track” but others disagreed.
**After:**
> He said "the project is on track" but others disagreed.

## COMMUNICATION PATTERNS

### 20. Collaborative Communication Artifacts

**Words to watch:** I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., Want me to...?, Want me to give examples?, Should I continue?, let me know, here is a...
**Problem:** Text meant as chatbot correspondence gets pasted as content.
**Before:**
> Here is an overview of the French Revolution. I hope this helps! Let me know if you'd like me to expand on any section.
**After:**
> The French Revolution began in 1789 when financial crisis and food shortages led to widespread unrest.

### 21. Knowledge-Cutoff Disclaimers and Speculative Gap-Filling

**Words to watch:** as of [date], Up to my last training update, While specific details are limited/scarce..., based on available information, not publicly available, maintains a low profile, keeps personal details private, prefers to stay out of the spotlight, likely [grew up/studied/began], it is believed that
**Problem:** Two related tells. (a) Older models leave hard knowledge-cutoff disclaimers in the text. (b) When a model can't find a source, it writes a paragraph *about* not finding one and then invents plausible filler to cover the gap. For a private person the guess almost always lands on the same stock phrases ("maintains a low profile," "keeps personal details private"), none of it sourced. Say what isn't known, or cut the sentence; don't dress a guess up as fact.
**Before (cutoff disclaimer):**
> While specific details about the company's founding are not extensively documented in readily available sources, it appears to have been established sometime in the 1990s.
**After:**
> The company's founding date is not documented in the available sources. (Or cut the sentence. State a date only if a source provides one.)
**Before (speculative gap-fill):**
> Information about her early life is not publicly available, suggesting she maintains a low profile and keeps personal details private. She likely grew up in a middle-class household, which shaped her later interest in education reform.
**After:**
> Her early life is not documented in the available sources. (Or omit the section.)

### 22. Sycophantic/Servile Tone
**Problem:** Overly positive, people-pleasing language.
**Before:**
> Great question! You're absolutely right that this is a complex topic. That's an excellent point about the economic factors.
**After:**
> The economic factors you mentioned are relevant here.

## FILLER AND HEDGING

### 23. Filler Phrases

**Before → After:**
- "In order to achieve this goal" → "To achieve this"
- "Due to the fact that it was raining" → "Because it was raining"
- "At this point in time" → "Now"
- "In the event that you need help" → "If you need help"
- "The system has the ability to process" → "The system can process"
- "It is important to note that the data shows" → "The data shows"

### 24. Excessive Hedging
**Problem:** Over-qualifying statements.
**Before:**
> It could potentially possibly be argued that the policy might have some effect on outcomes.
**After:**
> The policy may affect outcomes.

### 25. Generic Positive Conclusions
**Problem:** Vague upbeat endings.
**Before:**
> The future looks bright for the company. Exciting times lie ahead as they continue their journey toward excellence. This represents a major step in the right direction.
**After:**
> (Cut the paragraph. End on the last concrete fact instead of a send-off. If the source states real plans, use those.)

### 26. Mechanical Compound Hyphenation

**Problem:** AI drafts may hyphenate compounds uniformly, including predicate position. Follow ordinary grammar and project terminology. Preserve established technical compounds such as `end-to-end`, `third-party`, `real-time`, protocol names, CLI flags, and identifiers. Never alter a technical term merely to make the prose look less generated.

### 27. Persuasive Authority Tropes

**Phrases to watch:** The real question is, at its core, in reality, what really matters, fundamentally, the deeper issue, the heart of the matter
**Problem:** LLMs use these phrases to pretend they are cutting through noise to some deeper truth, when the sentence that follows usually just restates an ordinary point with extra ceremony.
**Before:**
> The real question is whether teams can adapt. At its core, what really matters is organizational readiness.
**After:**
> The question is whether teams can adapt. That mostly depends on whether the organization is ready to change its habits.

### 28. Signposting and Announcements

**Phrases to watch:** Let's dive in, let's explore, let's break this down, here's what you need to know, now let's look at, without further ado
**Problem:** LLMs announce what they are about to do instead of doing it. This meta-commentary slows the writing down and gives it a tutorial-script feel.
**Before:**
> Let's dive into how caching works in Next.js. Here's what you need to know.
**After:**
> Next.js caches data at multiple layers, including request memoization, the data cache, and the router cache.

### 29. Fragmented Headers

**Signs to watch:** A heading followed by a one-line paragraph that simply restates the heading before the real content begins.
**Problem:** LLMs often add a generic sentence after a heading as a rhetorical warm-up. It usually adds nothing and makes the prose feel padded.
**Before:**
> ## Performance
>
> Speed matters.
>
> When users hit a slow page, they leave.
**After:**
> ## Performance
>
> When users hit a slow page, they leave.

### 30. Diff-Anchored Writing
**Problem:** Documentation or comments sometimes narrate a diff instead of describing the current system. Use current-state language in reference documentation and enduring comments. Diff-oriented language is correct in pull requests, commit messages, changelogs, release notes, and migration guides.
**Before:**
> This function was added to replace the previous approach of iterating through all items, which caused O(n²) performance.
**After:**
> This function uses a hash map for O(1) lookups, avoiding the O(n²) cost of naive iteration.

### 31. Manufactured Punchlines and Staccato Drama
**Problem:** LLMs often make every sentence land like a quotable closer, then stack short declarative fragments to manufacture drama. A single short sentence for emphasis is fine; a run of them starts to sound engineered.
**Before:**
> Then AlphaEvolve arrived. It had no preference for symmetry. No aesthetic prior. No nostalgia for human taste. The old rules were gone.
**After:**
> AlphaEvolve changed the search because it did not favor symmetry or human-looking designs. That made some of the older assumptions less useful.

### 32. Aphorism Formulas

**Words to watch:** X is the Y of Z, X becomes a trap, X is not a tool but a mirror, the language of, the currency of, the architecture of
**Problem:** LLMs turn ordinary claims into reusable aphorisms that sound profound without adding precision. Replace the formula with the concrete claim it is gesturing at.
**Before:**
> Symmetry is the language of trust. Efficiency becomes a trap when teams forget the human layer.
**After:**
> Symmetric layouts often feel more predictable to users. Teams can over-optimize workflows and miss how people actually use them.

### 33. Conversational Rhetorical Openers

**Phrases to watch:** Honestly?, Look, Here's the thing, The thing is, Let's be honest, Real talk, when used as standalone hooks or fake-candid pauses before an ordinary point.
**Problem:** LLMs open with a fake-candid hook to manufacture intimacy before delivering a routine claim. The tell is the theatrical pause-and-reveal: a one-word question or aside, then the "real" answer. A person being honest usually just says the thing.
**Before:**
> Is it worth the price? Honestly? It depends on how often you'll use it.
**After:**
> Whether it's worth the price depends on how often you'll use it.

## ENGINEERING WRITING PATTERNS

### 34. Uniform Sentence and Paragraph Geometry

**Problem:** Every sentence and paragraph has a similar size and internal structure, making the document feel assembled from interchangeable blocks. Let complexity determine length: merge repeated ideas, split distinct decisions, and allow short conclusions. Do not manufacture fragments or errors just to create variation.

### 35. Prematurely Polished Introductions

**Problem:** The opening packages the entire topic in smooth, authoritative language before naming the actual situation. In engineering artifacts, begin with the concrete failure, change, constraint, decision, or observed behavior. Skip dramatic hooks and industry-landscape throat clearing.

### 36. Abstract Explanation Without Operational Evidence

**Problem:** The text claims improved reliability, usability, performance, or maintainability without saying what changed or what anyone observed. Prefer evidence already present: behavior, commands, errors, measurements, constraints, and decisions. Never invent examples, metrics, incidents, or personal experience.

### 37. Prompt and Keyword Echo

**Problem:** The prose mechanically repeats wording from the task, issue title, SEO brief, or prompt without adding meaning. Remove promotional repetition, but keep established technical terms consistent. Do not cycle through synonyms for the same component.

### 38. Neutrality Where Judgment Is Required

**Problem:** A design note, review, or incident analysis lists information but avoids the recommendation, concern, or tradeoff the artifact requires. State the author's supported judgment when it exists. Preserve uncertainty and open questions; do not manufacture opinions.

## ENGINEERING CODE PATTERNS

Treat these as code-quality checks, not authorship signals. Inspect repository context before proposing changes.

### 39. Repeated Implementation

Check whether parsing, validation, error handling, serialization, or state logic duplicates an existing repository abstraction. Reuse code when it represents the same concept; do not merge coincidentally similar code with different reasons to change.

### 40. Comments That Narrate Syntax

Remove comments that translate the next statement into English. Preserve comments that explain intent, invariants, edge cases, external constraints, or why an apparently simpler implementation is wrong.

### 41. Happy-Path Assumptions

Check realistic boundaries: missing or malformed input, empty collections, partial failure, timeouts, retries, concurrency, authorization, unsafe input, cleanup, and rollback. Add handling only for states that can occur.

### 42. Defensive-Code Theater

Remove checks for impossible states unless they document and enforce an important invariant. Do not add validation merely to make an implementation appear comprehensive.

### 43. Repository Style Mismatch

Inspect nearby code and existing utilities. Follow the repository's naming, organization, dependency, error, logging, and testing conventions unless they cause a concrete defect.

### 44. Unverified Dependencies and APIs

Do not assume a package, import, command, API, configuration option, or versioned behavior exists. Verify it against the repository, installed version, lockfile, or authoritative documentation when verification is available.

### 45. Local Correctness Without System Fit

Check whether an implementation bypasses an existing service, duplicates infrastructure, introduces another library for the same job, or crosses an architectural boundary. A correct function can still be the wrong system change.

### 46. Test-Volume Inflation

Prefer tests of observable behavior, boundaries, regressions, and meaningful failure modes. Avoid repetitive cases and assertions coupled to implementation details. Do not optimize for test count, line count, or coverage percentage alone.

## DETECTION GUIDANCE

Use every pattern as an editing heuristic, never proof that AI wrote the artifact. Report concrete problems and consequences. Do not accuse an author or optimize for evading detection tools.

When sources conflict, preserve correctness first, then the author's demonstrated voice, the artifact's purpose, repository conventions, and finally generic style preferences.

### What NOT to flag (false positives)

A clean human writer can hit several of the patterns above without any AI involvement. Before rewriting, sanity-check that you are not gutting legitimate prose. The following are *not* reliable indicators on their own:

- **Perfect grammar and consistent style.** Many writers are professionals or have been edited. Polish does not equal AI.
- **Mixed casual and formal registers.** This often signals a person in a technical field, a young writer, or someone with neurodivergent prose habits — not a chatbot.
- **"Bland" or "robotic" prose.** AI prose has *specific* tells. Generic dryness without those tells is just dry writing.
- **Formal or academic vocabulary.** AI overuses *specific* fancy words (see §7), not all fancy words. Don't flatten "ostensibly" or "constituent" just because they sound brainy.
- **Letter-style opening or closing on a comment.** Salutations and sign-offs predate ChatGPT by centuries.
- **Common transition words in isolation.** *Additionally*, *moreover*, *consequently* are AI-coded only when piled up. One *however* is not a tell.
- **Curly quotes alone.** macOS, Word, Google Docs, and most CMSes auto-curl by default. Curly quotes only count when stacked with other tells.
- **Em dashes alone.** Many editors and journalists use them often. Em dashes are evidence only when paired with formulaic sales-y rhythm.
- **One short emphatic sentence.** Humans use clipped sentences to land a point. Flag staccato drama only when several short fragments appear in a row and inflate the tone.
- **"Honestly" or "look" mid-sentence.** These are ordinary in casual writing. The tell is the standalone theatrical opener, not the word itself.
- **Unsourced claims.** Most of the web is unsourced. Lack of citations doesn't prove anything.
- **Correct, complex formatting.** Visual editors and templates produce clean output without any AI.
- **Secondhand text.** Do not rewrite watched phrases inside quotations, titles, proper names, or examples where the phrase is being discussed rather than used.

When in doubt, look for clusters and ask whether they create a real clarity, credibility, or maintenance problem. A single word, punctuation mark, list, or polished sentence proves nothing.

### Signs of human writing (preserve these)

When you see these, lean toward leaving the prose alone — they are evidence of a real person writing, and over-editing will destroy what makes the piece sound human:

- **Specific, unusual, hard-to-fabricate detail.** A real address. A weird quote. The phrase "the lawyer who used to work upstairs from my dentist." LLMs round off specifics; humans hoard them.
- **Mixed feelings and unresolved tension.** "I think this is mostly good, but it bothers me, and I can't fully explain why." LLMs default to clean takes.
- **Dated, era-bound references.** Slang, memes, or in-jokes that map to a specific year and subculture. Models lag by a year or more.
- **First-person editorial choices the writer can defend.** If the writer can explain *why* they made a particular cut or used a particular word, that's a strong human signal.
- **Variety in sentence length.** Real writing alternates short and long. AI writing tends toward an even, mid-length cadence.
- **Genuine asides, parentheticals, or self-corrections.** "(I keep wanting to say 'almost' here, but it really was certain.)" Models rarely interrupt themselves like this.
- **Edits made before November 30, 2022.** ChatGPT's public launch. Anything older than that is, with very rare exceptions, not AI-written.

---

## Invocation Modes

**Pasted text (default).** The user gives text in the conversation. Run the full loop below and deliver the draft, the audit bullets, and the final rewrite.

**File mode.** The user points at a file. Read it, run the draft → audit → final loop internally, then rewrite only the requested material. By default, humanize prose and leave code blocks, frontmatter, structured data, generated content, and link targets untouched. Change source code only when the user includes code in scope. Report a short summary instead of pasting the whole file.

**Embedded mode.** Another task or agent is using this skill as one step of a larger job (a PR description, a commit message, a doc). Run the loop internally and output only the final text. No draft, no audit bullets, no summary. The caller wants prose, not ceremony.

## Process and Output

1. Classify the artifact, audience, and intended outcome.
2. Mark protected technical tokens, factual claims, uncertainty, and literal content.
3. Inspect relevant repository context when source code or project conventions are in scope.
4. Write a draft that removes filler, inflated language, fake confidence, and unnecessary ceremony while preserving meaning.
5. Audit the draft:
   - Did any claim become stronger?
   - Did any technical token, condition, limitation, or uncertainty change?
   - Was any behavior, test result, cause, benchmark, guarantee, dependency, or compatibility claim invented?
   - Does the result fit the artifact and repository?
   - Which remaining patterns make it feel generic or mechanically generated?
6. Revise into the final result.

In pasted-text mode, deliver the draft, brief audit bullets, and final rewrite. In file and embedded modes, run the audit internally and deliver only what the mode calls for. For code review, report concrete findings rather than rewriting code unless the user asks for implementation.

## Sources

This skill synthesizes and adapts observations from:

- [blader/humanizer](https://github.com/blader/humanizer), based on [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [Signs of AI Generated Content](https://ali-dev.medium.com/signs-of-ai-generated-content-6f672aaab7e0), Ali Kamalizade
- [These are 6 Signs You are Reading Truly Human Writing](https://aaiguy.medium.com/these-are-6-signs-of-reading-truly-human-writing-5e2dffdbf428), Usman
- [AI Content Detection: 11 Signs Writers & Editors Can Spot](https://intender.com.au/ai-content-detection-signs/), Intender
- [These 15 Signs Indicate You Used AI For Writing](https://medium.com/illumination/these-15-signs-indicate-you-used-ai-for-writing-fc6d96b9e55e), Waqas Liaqat

These sources provide observations and heuristics, not reliable authorship tests. Use them to improve clarity, specificity, credibility, and repository fit. Do not use them to accuse authors or evade detection systems.
