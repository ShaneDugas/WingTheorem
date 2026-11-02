# Wing Theorem

Wing Theorem is an evolving framework for identifying and classifying a
"proper Wing meme": a meme that produces a productive cascade of questions,
references, and interpretations without collapsing into either obviousness or
inaccessible noise.

This repository begins with the theory and annotation format. The scoring
model, dataset, and classifier will evolve as examples expose weaknesses in the
definition.

## Current Hypothesis

A meme's Wingness cannot be determined by question count alone. A useful model
must also account for:

- how independent the generated questions are;
- how quickly another layer resolves each question;
- how recognizable each cultural reference is to a particular audience;
- how image and text layers ground, amplify, or contradict one another;
- whether the resulting ambiguity produces a payoff rather than confusion.

Obscurity is therefore audience-conditioned and layer-dependent. It should be
recorded as evidence first and converted into a score only after annotation.

## Repository Layout

- `docs/wing-theory.md`: working theory and development ideas.
- `schema/wing-annotation.schema.json`: machine-readable annotation format.
- `examples/bilbo-microsoft-date.json`: first annotated example.
- `assets/`: source images used by local examples.

## Development Principles

1. Preserve raw observations separately from derived scores.
2. Treat the audience as part of the classification context.
3. Count independent interpretive branches, not paraphrased questions.
4. Record interactions between layers explicitly.
5. Keep borderline and failed examples; they are evidence, not clutter.
6. Version changes to the definition alongside changes to the classifier.

## Next Research Step

Build a small seed dataset with approximately:

- 10 likely Wing memes;
- 10 borderline memes;
- 10 clear non-Wing memes.

For selected examples, compare full meme, image-only, text-only, and
unfamiliar-image variants. Collect recognition, questions, response time, and
audience metadata. This will help distinguish raw question generation from
effective interpretive branching.

## Status

Early working notes. Terms, features, and formulas are expected to change.
