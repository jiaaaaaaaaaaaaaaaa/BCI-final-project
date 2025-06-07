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
Participants are chosen if they have the top 5 of the highest and lowest error rates based on the behavioral data
High error group(error rate): 6(0.56%),21(0.29%),23(0.32%),26(0.57%),27(0.54%)
Low error group:8(0.013%),10(0.012%),12(0.034%),16(0.030%),17(0.029%)

<img width="415" alt="image" src="https://github.com/user-attachments/assets/823a7396-b9de-400e-8137-75f30f37b0ba" />


#Statistical Analysis:

Independent-sample t-tests to compare EEG features across groups

#validation

Robust artifact removal verified via ICA component inspection
Statistical comparisons between groups with correction for multiple comparisons
Visual inspection of ERP and spectral topographies

#reference

Cavanagh, J. F., & Frank, M. J. (2014). Frontal theta as a mechanism for cognitive control. Trends in cognitive sciences, 18(8), 414-421.https://doi.org/10.1016/j.tics.2014.04.012

Esterman, M., Noonan, S. K., Rosenberg, M., & DeGutis, J. (2013). In the zone or zoning out? Tracking behavioral and neural fluctuations during sustained attention. Cerebral cortex, 23(11), 2712-2723. https://doi.org/10.1093/cercor/bhs261

Foxe, J. J., & Snyder, A. C. (2011). The role of alpha-band brain oscillations as a sensory suppression mechanism during selective attention. Frontiers in Psychology, 2, 154. https://doi.org/10.3389/fpsyg.2011.00154

Van Diepen, R. M., Foxe, J. J., & Mazaheri, A. (2019). The functional role of alpha-band activity in attentional processing: the current zeitgeist and future outlook.Current Opinion in Psychology, 29, 229-238.https://doi.org/10.1016/j.copsyc.2019.03.015.

Weber, J., Solbakk, A. K., Blenkmann, A. O., Llorens, A., Funderud, I., Leske, S., ... & Helfrich, R. F. (2024). Ramping dynamics and theta oscillations reflect dissociable signatures during rule-guided human behavior. Nature Communications, 15(1),637. https://doi.org/10.1038/s41467-023-44571-7

Zhang, W., Zhang, Y., Zhang, Q., & Xu, J. (2022). Sustained attention states recognition with EEG and eye-tracking in the GradCPT. International Conference on Human-Computer Interaction, 213-221.https://doi.org/10.1007/978-3-031-05457-0_18


