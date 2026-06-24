# TakeMeter Planning
# Community

Community: r/nba

This project analyzes discussion quality in the NBA Reddit community. NBA discussions contain a mix of analytical arguments, emotional reactions, and strong opinions, making it a good environment for discourse classification.

# Label Taxonomy

## analysis

Posts that provide evidence, reasoning, statistics, or tactical explanations.

Examples:
- The Lakers struggled because their transition defense allowed too many fast-break points.
- Denver's offense worked because Jokic consistently created mismatches in the pick-and-roll.

## hot_take

Strong opinions stated confidently with little supporting evidence.

Examples:
- This coach is the worst in the league.
- LeBron is completely washed.

## reaction

Primarily emotional responses with little reasoning.

Examples:
- What a game!
- I can't believe they lost.

# Hard Edge Cases

A comment may contain both a strong opinion and one supporting statistic.

Decision rule:
If the comment includes meaningful evidence and reasoning, label it as analysis.
If the evidence is minimal and mainly supports a strong opinion, label it as hot_take.

# Data Collection Plan

Collect at least 200 public comments from r/nba.

Target distribution:
- analysis: 70
- hot_take: 70
- reaction: 60

If one label is underrepresented, collect additional examples specifically for that label.

# Evaluation Metrics

Metrics:
- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

F1 score is important because it evaluates performance for each label independently.

# Definition of Success

The classifier should outperform the zero-shot baseline and achieve approximately 70% overall accuracy with reasonably balanced per-class F1 scores.

# AI Tool Plan

Label Stress Testing:
Use ChatGPT to generate borderline examples and refine label definitions.

Annotation Assistance:
Use ChatGPT to suggest labels, then manually review and correct every example.

Failure Analysis:
Use ChatGPT to identify patterns in model errors and verify those patterns manually.