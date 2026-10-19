# Typing Speed: A 2×2 Factorial Experiment in R

**Experimental Design | Statistical Analysis | R | ANOVA | Data Visualization**

## Project Overview

Does the keyboard we use—or the noise around us—change how quickly we type? This project investigates how **keyboard type** (laptop internal vs. external) and **environment** (quiet vs. noisy) relate to **net typing speed**, measured in words per minute (WPM).

We conducted a controlled **2×2 factorial experiment** with **6 participants and 24 typing trials**, then used a **participant-blocked ANOVA** in R to estimate main effects and the keyboard-by-environment interaction. The goal was to translate a practical workplace question into a testable experimental design and an evidence-based interpretation.

## Research Questions

1. Does average net typing speed differ between internal and external keyboards?
2. Does average net typing speed differ between quiet and noisy environments?
3. Does the effect of keyboard type depend on the environment (an interaction)?

All hypothesis tests used **α = 0.05**.

## Experimental Design

| Design element | Specification |
| --- | --- |
| Design | 2×2 factorial, within-participant conditions |
| Participants | 6 |
| Total observations | 24 (6 participants × 4 conditions) |
| Response | Net words per minute (Net WPM) |
| Factor A | Keyboard: External / Internal |
| Factor B | Environment: Quiet / Noisy |
| Trial duration | 3 minutes per condition |
| Replication | One observation per participant per condition; six participants per treatment combination |
| Order | Four conditions randomized separately for each participant |
| Blocking | Participant included to account for baseline typing-speed differences |

The noisy condition used heavy metal music at a consistent volume, as described in the team presentation. Participants corrected typing errors during the test; the recorded response was net WPM, with no further error adjustment applied during analysis.

**Important design distinction:** These are 24 measurements from **6 people**, not 24 independent participants. Each person completed every condition once; there were no within-person repeats of the same condition.

## Tools and Analytical Approach

- **R / R Markdown:** data import, preprocessing, reproducible analysis, and HTML reporting.
- **Descriptive statistics:** mean net WPM by keyboard, environment, and treatment combination.
- **Participant-blocked ANOVA:** `Net_WPM ~ Participant + Keyboard * Environment`.
- **F-tests:** assessment of the two main effects and their interaction.
- **Visualizations:** treatment means, interaction plot, and model diagnostic plots.
- **Model diagnostics:** residuals-versus-fitted, normal Q–Q plot, and Shapiro–Wilk normality test.

The model accounts for additive participant-level baseline differences. Its interpretation still depends on assumptions about the residuals and on the scope of the small experimental sample.

## Key Findings

### 1. Keyboard type was statistically significant

| Comparison | Mean Net WPM |
| --- | ---: |
| Internal (laptop) keyboard | 42.67 |
| External keyboard | 37.83 |
| **Observed difference (Internal − External)** | **+4.83** |

After accounting for participant differences, the keyboard effect was significant: **F(1, 15) = 13.307, p = 0.00238**. In this experiment, participants typed faster on the internal keyboard on average. This is a finding for the tested participants, keyboards, and conditions—not evidence that all internal keyboards are universally faster.

### 2. No statistically significant noise effect was detected

The environment main effect was not statistically significant: **F(1, 15) = 0.016, p = 0.90157**. The study did not find sufficient evidence of a difference between the quiet and noisy conditions. This does **not** prove that noise never affects typing performance.

### 3. No statistically significant interaction was detected

The keyboard × environment interaction was not significant: **F(1, 15) = 0.016, p = 0.90157**. The interaction plot showed nearly parallel trends: the internal keyboard had a higher observed mean WPM in both environments.

### 4. Individual differences mattered

The team presentation also reported a statistically significant participant/block effect (**F = 51.08, p < 0.001**), highlighting substantial differences in baseline typing speed. Including participant as a block helped make the treatment comparisons more informative.

## Model Diagnostics

Residual-versus-fitted and normal Q–Q plots were examined. The R Markdown analysis reports a **Shapiro–Wilk W = 0.96589, p = 0.5674**, providing insufficient evidence to reject residual normality at α = 0.05. The diagnostic plots did not indicate a strong funnel pattern, although the small sample limits the ability to detect assumption violations. These checks do not establish independence of errors.

## Practical Interpretation

For this small sample, **keyboard selection appeared more relevant to typing speed than the tested background-noise condition**. A practical follow-up for workplace productivity would be to test whether keyboard familiarity, ergonomic fit, and different noise types explain performance differences across a larger and more diverse sample.

These findings should inform further testing rather than be treated as a universal recommendation about equipment or office environments.

## Limitations and Next Steps

- **Small sample:** six participants limit statistical precision and generalizability.
- **Single trial per condition per participant:** trial-to-trial variability within a condition was not directly estimated.
- **Keyboard familiarity:** prior experience with each keyboard was not recorded.
- **Noise specificity:** one controlled music/noise condition cannot represent all real-world environments.
- **Model assumptions:** participant blocking adjusts for baseline differences but does not capture every possible participant-specific treatment response.

Future work would recruit more participants, repeat each treatment combination within participants, measure keyboard familiarity, record actual condition order, and standardize typing passages, noise levels, and rest intervals.


## Project Files

| File | Description |
|---|---|
| [Dataset](Typing_speed.csv) | Original experimental dataset containing 24 observations |
| [R Markdown Source](typing_analysis_6participants.Rmd) | R code, statistical analysis, and model diagnostics |
| [HTML Analysis Report](typing_analysis_6participants.html) | Complete statistical analysis and visualizations |
| [Final Presentation](Typing_Speed_FINAL_Presentation.pdf) | Final presentation summarizing experimental design, findings, and conclusions |

### How to Explore This Project

1. Start with the Final Presentation for a quick overview.
2. Review the HTML Analysis Report for detailed statistical results.
3. Explore the R Markdown Source to understand the analytical workflow.
4. Download the Dataset to reproduce the analysis.


## Reproduce the Analysis

1. Download the repository, including the original `Typing_speed.csv` file.
2. Open `typing_analysis_6participants copy.Rmd` in RStudio.
3. Set the working/knitting directory so that `Typing_speed.csv` is accessible using the relative path in `read.csv()`.
4. Click **Knit** to regenerate the HTML report.

The analysis uses base R functions for importing data, fitting the ANOVA, and creating the displayed diagnostics, together with R Markdown / knitr for rendering.

## Skills Demonstrated

**Design of experiments · Data preparation · Hypothesis testing · Factorial ANOVA · Blocking · Interaction interpretation · Statistical diagnostics · Reproducible reporting · Analytical communication**

---

*Academic team project — STAT 5604, Design of Experiments (October 2026). Team presentation credits: Abey John, Adnan Shaikh, Jason Kuang, and Sara Su.*
