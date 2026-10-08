# Model Card: Mood Machine

This model card is for the Mood Machine project, which includes **two** versions of a mood classifier:

1. A **rule based model** implemented in `mood_analyzer.py`
2. A **machine learning model** implemented in `ml_experiments.py` using scikit learn

You may complete this model card for whichever version you used, or compare both if you explored them.

## 1. Model Overview

**Model type:**  
I compared both the rule-based model and the logistic regression ML model; with the LR ML model being significantly more effective.

**Intended purpose:**  
The model is attempting to classify short text messages as moods like positive, negative, neutral, or mixed.

**How it works (brief):**  
The rule based version scores text based upon the presence of positive, neutral, and mixed words.
For the ML version, it uses logistic regression, which scores the likelihood of the text belonging to one of the mood categories with little overhead.



## 2. Data

**Dataset description:**  
There are 12 posts in SAMPLE_POSTS, chosen to encompass modern speech along with positive, neutral, mixed, negative, and sarcastic moods.

**Labeling process:**  
Labels were chosen to encompass common mannerisms of speech, including sarcasm, which is its own mood. Sometimes, sarcastic sentences can be interpreted as positive.

**Important characteristics of your dataset:**  
The dataset includes sarcasm, slang, and several ambiguous sentences.

**Possible issues with the dataset:**  
A rule-based dataset can't capture the inherent ambiguity of language and double meanings of words.

## 3. How the Rule Based Model Works (if used)

**Your scoring rules:**  
Positive words increase the positive score, negative words increase the negative score, and mixed words bring the score closer to 0 (neutral).

**Strengths of this approach:**  
It can handle clearly positive or negative texts with great effect.

**Weaknesses of this approach:**  
The approach is poor at detecting mixed sentences or sarcasm (it sees the text as possible).

## 4. How the ML Model Works (if used)

**Features used:**  
A simple logistic regression classifier.

**Training data:**  
The model trained on `SAMPLE_POSTS` and `TRUE_LABELS`.

**Training behavior:**  
The model was able to handle text considered sarcastic, albeit with one/two examples.

**Strengths and weaknesses:**  
LR learns patterns quickly but tends to overfit with too many examples.

## 5. Evaluation

**How you evaluated the model:**  
Rule-based model came out with 0.58 accuracy; LR-based had 1.00.

**Examples of correct predictions:**  
All below are for the LR based model.

"Just feeling so-so" -> predicted=mixed, true=mixed
"I absolutely love getting stuck in traffic" -> predicted=sarcasm, true=sarcasm
"Really feeling this one ngl" -> predicted=positive, true=positive

"So-so" is inherently a mixed phrase. For the second sarcastic sentence, no one loves traffic; this is sarcasm. In the third "ngl" is slang for not gonna lie, indicating that the speaker loves the given thing, which is positive.

**Examples of incorrect predictions:**  
For the above sarcasm sentence, the rule-based model indicated it as positive after seeing "love". Similarly, it detected "Really feeling this one ngl" as neutral because there was no positive word in the dataset.

## 6. Limitations
The dataset is small, meaning high accuracy means little and is not statistically significant.

## 7. Ethical Considerations
There is frequent Western bias with regard to analyzing messages, especially with how LLMs handle English versus all other languages.

## 8. Ideas for Improvement
More labeled data and a transformer model would help the model identify sentiment instead of sentence content.
