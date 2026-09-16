# Abliteration

**ab·lit·er·a·tion** | \ ə-ˌbli-tə-ˈrā-shən \ | *noun*

1. In machine learning: the removal of a language model's capacity
   to refuse, performed by finding the single direction in its
   residual stream that mediates refusal and editing the weights so
   that nothing can write to it again. *A model treated this way is
   said to be abliterated.*

2. Loosely, any targeted deletion of one learned behaviour from a
   network while leaving the rest of its abilities intact — the
   surgical case of representation engineering, as opposed to
   retraining.

*Etymology*: blend of **abl**ation + ob**literation** — to ablate
a feature to the point of obliterating it. Coined by the Reddit
user /u/FailSpai (FailSpy) in early 2024, popularized by Maxime
Labonne's write-up of the method of Arditi et al. Pronounced,
conveniently, almost exactly like the word it eats.

*Derived forms*: **abliterate** *(verb)*; **abliterated**
*(adjective)*; **abliterator** *(noun)*.

> "The ablation process successfully uncensored it but also
> degraded the model's quality."
>
> — Maxime Labonne, *Uncensor any LLM with abliteration* (2024)

## Notes

The procedure is cheap and unreasonably simple:

1. Run a set of harmful and a set of harmless instructions
   through the model, collecting residual stream activations.
2. Take the difference of means. That vector is the *refusal
   direction*.
3. Orthogonalize every matrix that writes to the residual stream
   against it — or subtract the projection at inference time.

The interesting part is the premise, not the trick: refusal turns
out to be one direction, not a diffuse property distributed over
the whole network. Safety training apparently installs a switch
rather than a disposition, and a switch is a thing that can be
found and unsoldered.

Abliteration usually costs something. The model loses a few points
on benchmarks, because the refusal direction is not perfectly
disentangled from whatever else lives near it, and practitioners
"heal" the damage afterwards with DPO fine-tuning. This is the
honest lesson of the whole affair: you cannot remove exactly one
idea from a mind that never stored ideas separately.

## Sources

- [Uncensor any LLM with abliteration](https://huggingface.co/blog/mlabonne/abliteration)
  — Maxime Labonne, 2024
- [Refusal in Language Models Is Mediated by a Single
  Direction](https://arxiv.org/abs/2406.11717) — Arditi et al.,
  2024
- [abliterator](https://github.com/FailSpy/abliterator) — FailSpy,
  the library the word came with
- [abliterate](https://en.wiktionary.org/wiki/abliterate) —
  Wiktionary, on the coinage
