# Working Theory of Wing Meme Classification

## Originating Problem

An early heuristic proposed that a proper Wing meme generates at least three
questions. That is useful, but incomplete.

A meme may generate several immediate questions while its base image answers or
weakens those same questions. A familiar image can provide rapid cultural
grounding, turning apparent complexity into a short double entendre that ends
in "meh" or a shrug. Conversely, an unfamiliar base image can impose a large
interpretive cost before the reader reaches the intended joke.

Question yield is evidence of Wingness, not proof of it.

## Separate Observation From Scoring

Annotators should record observable features without seeing a final Wingness
score. Derived values should be calculated in a later stage.

This separation reduces anchoring and circular labeling. Hiding or salting
intermediate numbers is not sufficient if a model ultimately receives those
numbers together during training.

The system should retain:

- the original observations;
- the audience definition;
- the scoring-model version;
- the resulting derived scores;
- annotator uncertainty and disagreement.

## Audience-Conditioned Obscurity

Obscurity is not an intrinsic property of a reference. It depends on the
probability that a specified audience recognizes it.

One possible starting point is:

```text
raw_obscurity(audience) =
    sum(reference_salience * -log(P(reference_recognized | audience)))
```

Age belongs inside the recognition estimate rather than as a universal
multiplier applied afterward:

```text
P(recognition | age, cohort, domain, culture, reference_age, reference_type)
```

A seven-year age gap may strongly affect recognition of a brief internet trend
while barely affecting recognition of Tolkien. Other relevant audience
variables may include technical background, geography, language, occupation,
fandom, and platform history.

The first implementation should estimate these values coarsely and preserve the
inputs. False precision would be worse than an honest ordinal scale.

## Layer Interactions

Image, caption, format, typography, and source context should be annotated as
separate layers. Their interactions may:

- **ground**: make another layer easier to interpret;
- **resolve**: answer a question raised elsewhere;
- **amplify**: increase the force or reach of another layer;
- **contradict**: create tension between interpretations;
- **gate**: require recognition of one layer before another becomes available;
- **distract**: add complexity without contributing to the payoff.

A familiar base image can lower effective obscurity even when the added caption
is domain-specific. An unfamiliar "photo of your shoe" or fried egg on a beach
starts without a shared memetic frame and may create a high grounding cost.

## Questions And Interpretive Branches

Questions should not be counted equally. Three paraphrases of one uncertainty
are not three independent interpretive branches.

A possible formulation is:

```text
effective_question_yield =
    sum(novelty * independence * latency_weight * (1 - resolution))
```

Useful distinctions include:

- immediate versus latent questions;
- independent versus derivative questions;
- open versus resolved questions;
- productive versus merely confusing questions;
- questions about the source image versus the added text;
- questions necessary for the payoff versus incidental questions.

## Productive Ambiguity

The working hypothesis is that Wingness has an inverted-U relationship with
effective obscurity:

- too little obscurity produces an obvious, inert meme;
- moderate obscurity produces productive ambiguity;
- too much obscurity produces inaccessible noise.

The useful region will vary by audience. This means the classifier may need to
return a distribution or an audience-specific score rather than one universal
label.

## Proposed Feature Vector

Keep the feature vector visible and inspectable:

```text
[
  raw_question_yield,
  effective_question_yield,
  reference_obscurity,
  base_recognizability,
  interpretive_branching,
  layer_interaction_strength,
  resolution_pressure,
  payoff_strength,
  audience_stability
]
```

Do not collapse these features prematurely. A rule-based baseline should come
before a learned classifier so disagreements with the framework remain easy to
inspect.

## Bilbo / Microsoft Example

The source image uses Bilbo Baggins asking, "After all... why not?" The added
caption attributes to Microsoft the decision to store a date as an integer in
`yyMMddHHmm` format.

Initial observations:

- The Tolkien image is a highly recognizable cultural anchor for many
  audiences.
- The date-storage reference is comparatively domain-specific.
- Bilbo's expression and quoted question personify an arbitrary design choice.
- The image partially answers the implied question, "Why would Microsoft do
  that?"
- Several initial questions therefore collapse into one interpretive branch.

The example demonstrates high raw question production but only moderate
effective branching. It is useful as a borderline or mediocre example because
the familiar image grounds the reader quickly and the resolution arrives with
little remaining interpretive tension.

## Experimental Program

### Seed Dataset

Begin with likely Wings, borderline examples, and clear non-Wings. Preserve the
reason each example was selected before annotation.

### Ablation Study

For the same underlying meme, test:

1. full image and text;
2. image only;
3. text only;
4. original text on an unfamiliar image.

Collect:

- references recognized;
- questions generated;
- time to first interpretation;
- time to perceived payoff;
- confidence;
- age cohort and relevant domain familiarity.

### Annotation Reliability

Use multiple annotators and compare agreement separately for observations and
final labels. Low agreement on a feature may indicate that its definition
needs work, not that an annotator is wrong.

### Negative Evidence

Record why an example fails:

- too obvious;
- too obscure;
- no interaction between layers;
- questions resolve immediately;
- references are decorative rather than functional;
- ambiguity lacks payoff.

Negative evidence will be central to refining the boundary of a proper Wing.
