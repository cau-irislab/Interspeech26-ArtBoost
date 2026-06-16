# ArtBoost: Synthetic Articulatory Data Augmentation for Acoustic-to-Articulatory Inversion

> 🎉 **Accepted at Interspeech 2026!**

[Hyung Kyu Kim](https://github.com/kimhyungkyu-1208)<sup>1</sup>, Byungchan Hwang<sup>2</sup>, Hak Gu Kim<sup>2</sup>

<sup>1</sup> Department of Imaging Science and Arts, Chung-Ang University, South Korea
<sup>2</sup> Department of Metaverse Convergence, Chung-Ang University, South Korea

📄 [Project Page](https://cau-irislab.github.io/Interspeech26-ArtBoost/) | 📝 [Paper](https://arxiv.org/abs/2606.16327) | 💻 Code (coming soon)

## Overview

**ArtBoost** is a data augmentation strategy for **acoustic-to-articulatory inversion (AAI)** that repurposes large-scale **speech–mesh datasets** — originally built for speech-driven 3D facial animation — as a source of pseudo articulatory supervision, alleviating the scarcity of electromagnetic articulography (EMA) data.

## Method

ArtBoost converts abundant speech–mesh recordings into pseudo articulatory training data in three steps:

1. **ASR-guided Utterance Segmentation** — Long, continuous speech–mesh recordings are segmented into utterance-level clips using word-level ASR timestamps, matching the utterance-level organization of EMA corpora.
2. **Pseudo Articulatory Trajectory Extraction** — Visible facial anchors corresponding to articulators — upper lip (UL), lower lip (LL), and lower incisor (LI) — are tracked on audio-aligned 3D meshes. Protrusion (z) and mouth-opening (y) components are assembled into a 12-channel EMA-style target and resampled to the articulatory frame rate.
3. **Pre-training then Fine-tuning** — The AAI model is first pre-trained on the pseudo trajectories with a *channel-masked* loss supervising only the visible UL/LL/LI channels, then fine-tuned on real EMA data with full-channel supervision.

## Results

Under leave-one-speaker-out (unseen-speaker) evaluation, ArtBoost consistently improves PCC (↑) and RMSE (↓) across two AAI architectures and two benchmarks:

| Model | Dataset | PCC w/o | PCC w/ ArtBoost | RMSE w/o | RMSE w/ ArtBoost |
|---|---|---|---|---|---|
| SSL-AAI | HPRC | 0.678 | **0.698** | 0.736 | **0.717** |
| SSL-AAI | USC-TIMIT | 0.351 | **0.510** | 0.864 | **0.792** |
| SI-AAI | HPRC | 0.717 | **0.732** | 0.706 | **0.689** |
| SI-AAI | USC-TIMIT | 0.488 | **0.593** | 0.917 | **0.817** |

Gains are most pronounced on USC-TIMIT, where ground-truth EMA data is scarcest — indicating that ArtBoost is especially effective under limited supervision. Trajectory analyses further confirm that the mesh-derived pseudo signals encode physically meaningful, visible articulatory dynamics.

## Citation

```bibtex
@inproceedings{kim2026artboost,
  author    = {Kim, Hyung Kyu and Hwang, Byungchan and Kim, Hak Gu},
  title     = {ArtBoost: Synthetic Articulatory Data Augmentation for Acoustic-to-Articulatory Inversion},
  booktitle = {Proc. Interspeech},
  year      = {2026}
}
```
