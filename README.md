<<<<<<< HEAD
# ai201-project3-takemeter
=======
TakeMeter: Evaluating NBA Discussion Quality

Overview

TakeMeter is a text classification system designed to evaluate different styles of discourse within the r/nba Reddit community. The goal of the project is to distinguish between evidence-based discussion, unsupported opinionated claims, and emotional reactions commonly found in NBA discussions.

This project fine-tunes DistilBERT on a manually labeled dataset of NBA comments and compares its performance against a zero-shot baseline using Groq’s Llama 3.3 70B model.

⸻

Community Choice and Reasoning

I chose the r/nba community because it contains a large volume of active discussion with a wide range of discourse styles. NBA fans frequently post detailed basketball analysis, bold predictions, emotional reactions, jokes, and memes within the same discussion thread.

This makes r/nba a good classification task because the distinctions between thoughtful analysis and low-effort reactions are meaningful to community members and moderators.

⸻

Label Taxonomy

analysis

Definition:

A comment that provides evidence, reasoning, statistics, strategic discussion, or a detailed basketball argument.

Examples:

* “They went down five spots and got off $33 million in salary, which gives them a valuable trade exception.”
* “Claxton fits well because the Bulls needed a defensive center and had cap space available.”

⸻

hot_take

Definition:

A strong opinion, judgment, prediction, or claim with little supporting evidence.

Examples:

* “Randle really has negative value now.”
* “The Lakers only made this trade so Pelinka could say he did something.”

⸻

reaction

Definition:

An emotional reaction, joke, meme, surprise, excitement, disappointment, or short response with little reasoning.

Examples:

* “Bruh.”
* “Funniest trade of all time.”

⸻

Data Collection

Source

All data was collected manually from public Reddit discussions in r/nba.

Dataset Size

Total examples: 216


Label Distribution:

Label                   Count

analysis                 76

hot_take                 35

reaction                 105

Labeling Process

Each comment was manually reviewed and assigned exactly one label based on the definitions above. Ambiguous comments were evaluated using decision rules documented in planning.md.

⸻

Difficult Labeling Decisions

Example 1

Comment:

“Randle really got negative value now lol”

Possible labels:

* hot_take
* reaction

Decision:

hot_take because the comment makes a strong judgment about a player’s value.

⸻

Example 2

Comment:

“It’s not that funny. We just gave up some cash and swapped picks.”

Possible labels:

* analysis
* reaction

Decision:

analysis because it explains the trade using factual reasoning.

⸻

Example 3

Comment:

“Carr. They need athleticism imo.”

Possible labels:

* analysis
* hot_take

Decision:

analysis because it provides a basketball-related rationale rather than simply expressing an opinion.

⸻

Fine-Tuning Approach

Base Model

distilbert-base-uncased

Training Setup

* Epochs: 3
* Learning Rate: 2e-5
* Batch Size: 16

The default notebook hyperparameters were used because the dataset was relatively small and the training notebook was already optimized for this assignment.

⸻

Baseline Model

The baseline model used Groq’s llama-3.3-70b-versatile model in a zero-shot setting.

The prompt defined the three labels (analysis, hot_take, reaction), provided one example for each label, and instructed the model to return only the label name.

The baseline was evaluated on the same test set used for the fine-tuned model.

⸻

Evaluation Report

Accuracy Comparison:
Model                           Accuracy

Zero-shot Groq Baseline           0.636

Fine-Tuned DistilBERT             0.485

Fine-tuning resulted in a regression of 15.2 percentage points.

⸻

Baseline Metrics:
Label       Precision       Recall      F1

analysis      1.00           0.33       0.50

hot_take      0.50           0.20       0.29

reaction      0.59           1.00       0.74

Fine-Tuned Metrics:
Label       Precision       Recall      F1

analysis       0.50           0.08      0.14

hot_take       0.00           0.00      0.00

reaction       0.48           0.94      0.6

Confusion Matrix:
True \ Predicted    analysis    hot_take    reaction

analysis                1           0           11

hot_take                0           0            5

reaction                1           0            15


Failure Analysis

Failure 1

Comment:

“Randle really got negative value now lol”

True Label:

hot_take

Predicted:

reaction

Analysis:

The model focused on the emotional tone (“lol”) and ignored the judgment being made.

⸻

Failure 2

Comment:

“They went down five spots and got off $33 million in money.”

True Label:

analysis

Predicted:

reaction

Analysis:

The comment contains reasoning and evidence, but its conversational style may have made it look similar to reaction comments.

⸻

Failure 3

Comment:

“Minnesota’s getting Ja Morant.”

True Label:

hot_take

Predicted:

reaction

Analysis:

The model failed to recognize speculative predictions as a distinct category and grouped them into reaction.

⸻

Sample Classifications:
Comment                                                 Predicted Label

“Bruh”                                                       reaction

“Funniest trade of all time.”                                reaction

“They went down five spots and got off $33 million in salary.”                                                      analysis

“Randle really got negative value now lol.”                   reaction

“Minnesota’s getting Ja Morant.”                              reaction


The prediction for “Bruh” is reasonable because the comment is a short emotional response with no supporting reasoning.

⸻

Reflection

My goal was to distinguish between analysis, hot_take, and reaction comments. However, the model primarily learned to separate reaction comments from everything else.

The model completely failed to predict the hot_take class and misclassified most analysis comments as reaction. This suggests that it relied heavily on surface-level language patterns rather than deeper argumentative structure.

A likely cause is dataset imbalance. The dataset contained 105 reaction examples but only 35 hot_take examples. The model therefore learned the majority class much more effectively than the intended discourse distinctions.

⸻

Spec Reflection

How the Spec Helped

The requirement to define label boundaries before annotation forced me to think carefully about ambiguous cases and improve the consistency of my labels.

How Implementation Diverged

I originally expected the fine-tuned model to outperform the zero-shot baseline. Instead, the baseline achieved higher accuracy. This shifted the focus of the project from maximizing performance to understanding failure modes and class imbalance.

⸻

AI Usage

AI Usage #1

I used ChatGPT to stress-test my label definitions and generate boundary cases between analysis, hot_take, and reaction. Several examples revealed ambiguity in my original definitions, which I revised before annotation.

AI Usage #2

I used ChatGPT to help analyze the confusion matrix and identify systematic error patterns after evaluation. I independently verified those observations before including them in the report.
>>>>>>> c82e8bd (complete project 3)
