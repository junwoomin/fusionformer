# FusionFormer

[한국어](README_ko.md)

**Status: research concept and architecture sketch.** Development stopped at the idea stage because of time and competing research work. This archive contains the design, not a trained model or an implementation.

FusionFormer explores whether neighboring vehicles can supply BEV features for regions that the ego vehicle cannot observe. Each vehicle produces BEV features, the features are aligned using vehicle location information, and a transformer fuses the aligned representations.

![Original FusionFormer architecture sketch](assets/fusionformer-concept.png)

## Proposed architecture

| Stage | Intended operation |
| --- | --- |
| Per-vehicle perception | Encode ego and neighboring camera observations into BEV features. The sketch labels the BEV encoders as sharing weights. |
| Vehicle context | Inject neighboring vehicle status and vehicle location information. |
| Alignment | Express neighboring features in the ego coordinate frame before fusion. |
| FusionFormer | Fuse ego and neighboring BEV features into a representation with broader coverage. |
| Downstream output | Support perception of occluded or otherwise unobserved regions. The task head remains unspecified. |

## Research questions

- How much improvement comes from genuinely complementary viewpoints?
- How sensitive is fusion to pose error, time misalignment, and communication delay?
- Which spatial regions and channels should be transmitted under a bandwidth limit?
- How should stale or unreliable neighbors be masked?

These are open evaluation questions. No accuracy, latency, or communication result is claimed.

## Suggested evaluation when implementation resumes

Compare ego-only perception, aligned feature fusion without attention, and transformer fusion on the same scenes. Separate occluded-region quality from overall perception quality. Report localization perturbations, delay, neighbor count, and bytes transmitted per frame alongside task metrics.
