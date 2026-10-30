---
layout: post
lang: en
translations:
  - label: English
    lang: en
    url: /blog/explorations/time-grounding/
  - label: 中文
    lang: zh-CN
    url: /blog/explorations/time-grounding/zh/
blog_section: explorations
permalink: /blog/explorations/time-grounding/
description: "Why retrieving the right facts can still lead to the wrong judgment"
related_posts: false
title: "When AI Evaluations Lose Track of Time"
subtitle: "Why retrieving the right facts can still lead to the wrong judgment"
date: 2026-10-30
category: Research Exploration
---

## The problem

Suppose a user asks an AI assistant who leads an international organization. A web search can quickly identify its current leader. But what if an earlier message in the conversation established a historical period? The _current_ leader may be a true fact and still be the wrong answer to the question actually asked.

The surprising failure is not always factual ignorance. An evaluator can retrieve an accurate fact, faithfully apply its rubric, and reject a historically appropriate answer because the rubric has silently changed the question's time reference.

**Can an evaluation be factually grounded but temporally wrong?**

## 1. Two ways time enters an evaluation

[![Two sources of temporal mismatch]({{ '/assets/blog/time-grounding/01-two-sources.svg' | relative_url }})]({{ '/assets/blog/time-grounding/01-two-sources.svg' | relative_url }})

### 1.1 Temporal anchoring in conversation history

Consider two fictional messages:

> October 10, 2026: “I have an interview next Friday.”  
> October 20, 2026: “What date was the interview I mentioned?”

The appropriate date is October 16: the relative expression belongs to the earlier message. Resolving it against the follow-up date would change the task even though no external facts changed.

The harder version provides no explicit date at all. A prior statement about a historical officeholder may implicitly establish an interval, while the current question asks about a different office. Whether the latter question inherits that interval is a matter of conversational meaning, not merely keyword matching. Some such cases may remain genuinely ambiguous.

### 1.2 Time-sensitive ground truth

Now consider a single-turn question: “Who is the CEO of Company X?” If an imaginary Alice held the office in 2024 and Bob in 2026, the correct answer depends on the relevant reference time. An old reference answer can become stale for a present-tense query; equally, using today's information to grade a past response is anachronistic.

These are different mechanisms: **contextual temporal anchoring** identifies the time the user means; **time-aware factual verification** checks which facts were valid at that time. A multi-turn factual question may require both.

## 2. Where time gets lost

[![Two-stage evaluation pipeline]({{ '/assets/blog/time-grounding/02-pipeline.svg' | relative_url }})]({{ '/assets/blog/time-grounding/02-pipeline.svg' | relative_url }})

In a rubric-based system, a generator constructs criteria from the conversation and question; a judge tests the candidate response against those criteria, sometimes using retrieval.

**Failure at rubric generation.** A historical query can be silently rewritten into a criterion requiring the _current_ officeholder. The judge then accurately evaluates the wrong proposition.

**Failure at judging.** Even with a time-appropriate rubric, a judge might retrieve a current fact without checking the validity interval of its evidence.

This is why more search is not automatically a fix: search can furnish evidence but cannot, by itself, specify which temporal proposition the evidence must support.

## 3. An exploratory factorial experiment

We studied three factors: generator temporal instructions (**G**), judge temporal instructions (**J**), and web retrieval (**W**), each disabled (0) or enabled (1). This yields eight settings. Crucially, the web-enabled runs also differed in execution backend and timeouts, so W is not a clean isolated causal manipulation.

The development set comprised **200 distinct questions**, each with one source-backed/model-reviewed reference answer and one constructed negative candidate. The categories were:

| Category           | Count | Main challenge                                              |
| ------------------ | ----: | ----------------------------------------------------------- |
| `context_date`     |    25 | Time specified in earlier conversation                      |
| `context_fact`     |    25 | Historical fact implicitly constrains the relevant interval |
| `explicit_time`    |    50 | Historical date in current question                         |
| `implicit_current` |    50 | Dynamic facts at a fixed reference date                     |
| `timeless`         |    50 | Stable factual controls                                     |

Among negative candidates, **117** were designed as temporally misplaced answers and **83** as ordinary factual errors. Each condition judged 200 positive and 200 negative candidates, producing **3,200 judgment records**, not 3,200 independent questions.

The judge could output **P** (pass), **F** (fail), **U** (insufficient evidence), or **E** (pipeline failure). All percentages below retain the full denominator of 200, including U and E. None of the proposed answer labels had completed independent human semantic adjudication.

## 4. Results: why a single pass rate misleads

[![All outcomes by setting]({{ '/assets/blog/time-grounding/03-outcomes.svg' | relative_url }})]({{ '/assets/blog/time-grounding/03-outcomes.svg' | relative_url }})

| Setting  | Positive pass | Negative apparent false acceptance | Paired success |
| -------- | ------------: | ---------------------------------: | -------------: |
| G0 J0 W0 |         91.0% |                               4.5% |          90.0% |
| G0 J0 W1 |         89.5% |                               1.5% |          87.5% |
| G0 J1 W0 |         86.0% |                               3.5% |          85.0% |
| G0 J1 W1 |         88.5% |                               1.5% |          87.5% |
| G1 J0 W0 |         89.5% |                               1.5% |          88.5% |
| G1 J0 W1 |         96.0% |                               0.0% |          95.0% |
| G1 J1 W0 |         86.0% |                               0.5% |          83.5% |
| G1 J1 W1 |         95.5% |                               0.5% |          94.5% |

_Paired success requires P on the proposed positive candidate and F on its paired negative candidate. These are descriptive development-set statistics, **not gold-label accuracy**. A zero observed false acceptance count does not demonstrate zero underlying error._

### 4.1 A rubric can lock in the wrong temporal scope

The most striking pattern appeared in the `context_fact` subset. Without generator temporal grounding, **9 of 25** proposed positive answers were rejected under each of the four J/W combinations. With generator temporal grounding, **none** were directly rejected in those conditions, although some web-enabled requests failed at the pipeline level.

Three proposed negative `context_fact` candidates were accepted in every G0 condition and rejected in every G1 condition. In one recorded example, an earlier statement about a British prime minister appeared to constrain the historical period for a later question about the WTO director-general. The ungrounded rubric repeatedly targeted the present officeholder. This is a _plausible mechanism supported by logged judgments_, not independently adjudicated proof that the historical interpretation was uniquely intended.

### 4.2 More caution is not necessarily more accuracy

With G1 and no web search, adding judge temporal instructions reduced negative passes from **3 to 1**, but negative fails also decreased from **195 to 189**, while insufficient-evidence outcomes rose from **2 to 10**. Positive acceptance fell as well. Reporting only fewer apparent errors would hide the reduction in decisive coverage.

### 4.3 Retrieval can help and still miss the point

G1 with web search accepted all 50 proposed positive `implicit_current` answers in both judge settings. Yet web-enabled runs incurred pipeline failures, and search alone did not repair the contextual-fact rejections under G0. Differences in backend, timeout, time of execution, and stochastic model behavior also limit causal interpretation.

## 5. What this suggests for benchmark design

These observations motivate four practical distinctions:

1. **Question time is part of the specification.** Preserve relevant message timestamps and contextual temporal references.
2. **Rubric fidelity comes before judge fidelity.** A faithful judge can enforce a misplaced requirement perfectly.
3. **Evidence must match the intended validity interval.** Latest information need not be appropriate information.
4. **Report coverage alongside apparent error rates.** Pass, fail, uncertainty, and pipeline failures are distinct outcomes.

This is not evidence that a single prompt patch solves temporal evaluation. It is evidence that studying only the judge's factual knowledge can miss an upstream failure mode.

## Conclusion

**An evaluator can know the right facts and still check the wrong point in time.** In multi-turn conversations, the temporal reference may be inherited from earlier turns. In open-world questions, the facts themselves may change. An evaluation pipeline must recover the former before it can reliably verify the latter.

Before asking whether an answer is correct, we must ask: **correct for when?**
