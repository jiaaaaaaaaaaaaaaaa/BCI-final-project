# BCI-final-project
BCI final project
Error Warning? Decoding Neural Signatures of Attentional Lapses from EEG Activity!

#introduction

This project presents an EEG-based analysis framework aimed at investigating group-level differences in neural dynamics associated with attentional lapses. Using data from the gradual onset Continuous Performance Task (gradCPT), we compare EEG signatures between participants with high versus low error rates to identify distinct patterns related to sustained attention control. The analysis focuses on alpha and theta band activity in frontal-parietal regions and event-related potentials (ERPs) preceding behavioral errors.

#dataset

Dataset: Sustained Attention Task (gradCPT) using EEG-fMRI and DTI
Source: OpenNeuro.org
Participants: 29 healthy adults (ages 19–42)
EEG channels: 64
Sampling rate: 1000 Hz
Hardware: Simultaneous EEG setup(GradOFF)

#objective

Divide participants into High-error and Low-error groups based on task performance.
Compare EEG activity between groups, with focus on frontal-parietal alpha and theta oscillations.
Examine group-level differences in ERP components preceding behavioral responses.
Identify neurophysiological markers associated with attention stability or lapses.

#analysis framework

The EEG analysis pipeline includes:

(1)Preprocessing:
Bandpass filtering (1–50 Hz)
Artifact rejection using ICA and ICLabel
Epoching around stimulus onset (−1000 ms to 2000 ms)

(2)Feature Extraction:
Alpha power (8–13 Hz) and theta power (4–7 Hz)
ERP components (Fp1, Fp2, Fz, and Pz)
Power spectral density (PSD) and time-frequency decomposition

(3)Grouping:
Participants are chosen if they have the top 5 of the highest and lowest error rates

#Statistical Analysis:

Independent-sample t-tests to compare EEG features across groups

#validation

Robust artifact removal verified via ICA component inspection
Statistical comparisons between groups with correction for multiple comparisons
Visual inspection of ERP and spectral topographies
<img width="415" alt="image" src="https://github.com/user-attachments/assets/823a7396-b9de-400e-8137-75f30f37b0ba" />

