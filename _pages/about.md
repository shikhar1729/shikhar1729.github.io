---
layout: about
title: about
permalink: /
subtitle: AI safety and interpretability research. Machine Learning Engineer at <a href="https://www.apple.com">Apple</a>.

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>San Diego, California</p>
    <p><a href="mailto:rbk.shikhar@gmail.com">rbk.shikhar@gmail.com</a></p>

selected_papers: true
social: true

announcements:
  enabled: true
  scrollable: true
  limit: 6

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

I work on making the reasoning a language model shows us correspond to the computation it actually ran.

Most of my research sits at the point where that correspondence breaks. In [The Hypocrisy Gap](https://arxiv.org/abs/2602.02496) I used sparse autoencoders to measure the divergence between what a model internally represents as true and what its chain of thought says, and showed the gap predicts sycophantic and unfaithful runs better than log-probability baselines. In [A False Average](https://arxiv.org/abs/2608.00583) I showed that CoT monitors collapse from roughly 95% to under 11% catch rate precisely on the subset where the reasoning trace is the only evidence, which is the subset those monitors exist to cover. Aggregate monitor accuracy hides this.

I am currently a **Pivotal Research Fellow**, selected from over 2,500 applicants and awarded a merit-based extension, working with Noah Y. Siegel at Google DeepMind on chain-of-thought faithfulness. I am also a **MARS V Research Fellow** at Meridian, one of 86 selected from 1,733 applications, working with Julian Schulz on steganographic reasoning, where we find that models hide reasoning in text through a distributed mechanism that transfers across encoding schemes by reusing the same weights. Earlier in 2026 I was a **SPAR Fellow** at Kairos on attention consistency training for safety.

Adjacent threads run through hallucination mitigation via attention steering ([COMPASS](https://arxiv.org/abs/2511.14776)), KV-cache compression from emergent linear structure across attention heads ([Linear Predictability](https://arxiv.org/abs/2603.13314)), and behavioral evaluation under persona and framing shifts ([ChameleonBench](/publications/), [PAB](/publications/), [ProMoral-Bench](https://arxiv.org/abs/2602.13274)).

By day I am a Machine Learning Engineer at Apple, building systems that optimize power and performance across Apple's operating systems. Before that I spent six years at NVIDIA across systems, infrastructure, and ML research, and completed an MS in Computational Science and Engineering at Georgia Tech, where I was a graduate research assistant at [AI4OPT](https://www.ai4opt.org/) under Prof. Pascal Van Hentenryck.

Outside my own papers I review for interpretability and reasoning venues, with twelve completed reviews across the Efficient Reasoning workshops at NeurIPS 2025 and COLM 2026, BlackboxNLP 2026 at EMNLP, and InterpScience 2026, and I mentor researchers at Algoverse. I am an IEEE Senior Member.

If you are working on faithfulness, monitorability, or evaluation and want a collaborator, get in touch.
