# Technical Writing

Use these guidelines for prose that helps technical readers understand a system, make a decision or complete a task. Project and platform conventions take precedence, including spelling, punctuation and required document structure.

## Start With The Reader's Need

Determine what the reader already knows, what they need to learn and what they should be able to do afterwards. State the document's scope early and omit background that does not support that purpose.

Choose a shape that matches the content:

- **Concept or explanation:** Establish the idea, explain the mechanism, identify boundaries and ground it with an example.
- **Procedure:** State the outcome and prerequisites, then give ordered actions and observable results.
- **Reference:** Use consistent terminology and predictable structure so readers can retrieve details quickly.
- **Decision or design note:** State the decision or problem, then present constraints, trade-offs, alternatives and consequences.

Do not force one document to serve all four purposes when separation would help the reader.

## Make Sentences Precise

- Prefer active voice when the actor matters or passive voice would hide responsibility.
- Choose verbs that name the real action. Replace vague constructions such as `there is`, `occurs` or `happens` when a concrete subject and verb are available.
- Keep one main idea in a sentence. Split sentences when separate conditions, actions or consequences compete for attention.
- Define unfamiliar terms and acronyms before using them as shorthand.
- Keep terminology consistent. Do not vary technical nouns merely to avoid repetition.
- Place conditions before the instruction or claim they govern.
- Preserve modal meaning. `Must`, `should`, `can` and `might` are not interchangeable.
- Replace vague pronouns such as `it`, `this` or `that` when their referent is not immediate and unmistakable.

## Make Structure Visible

- Put critical information first in a section and usually in a paragraph.
- Give each paragraph one topic. Break up walls of text, but do not fragment one coherent idea into choppy one-sentence paragraphs.
- Use descriptive headings that tell readers what the section contains.
- Use numbered lists for sequences and bullets for unordered sets.
- Keep list items grammatically parallel. Begin procedural steps with imperative verbs.
- Use descriptive link text rather than generic phrases such as `here` or `this link`.
- Format commands, filenames, identifiers, literal values and code consistently with the target platform.

## Write Procedures That Can Be Followed

- Put prerequisites and safety constraints before the steps that depend on them.
- Give each step one primary action unless combining actions prevents confusion.
- Name the interface, file, command or control precisely.
- Include an expected result when readers need it to know whether the step succeeded.
- Explain optional branches where they occur instead of hiding them after the main procedure.
- Avoid describing work as easy, simple or quick. Those claims do not help a blocked reader.

## Use Examples As Evidence

Introduce an example by stating what it demonstrates. Keep it minimal enough to expose the relevant mechanism without removing constraints that make it correct.

Do not invent commands, output or behaviour. Preserve code exactly unless the task includes changing it, and distinguish illustrative placeholders from values readers can copy.

## Write For A Broad Technical Audience

Prefer plain, direct language without erasing necessary technical terms. Avoid idioms, culture-specific references and unexplained humour in documentation intended for a global audience. These restrictions need not flatten personal or editorial writing governed by a different genre guide.

## Sources

This reference paraphrases and operationalises guidance from Google's [developer documentation style guide](https://developers.google.com/style/) and [Technical Writing One](https://developers.google.com/tech-writing/one/summary). It does not adopt Google's US English conventions where active project or authorship guidance specifies another form of English.
