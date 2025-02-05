# Evaluating Large Language Models using Psychometrics
![Psychometrics Benchmark Visualization](img/teaser.png)

## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
- [API Keys](#api-keys)
- [Evaluation Settings](#evaluation-settings)
- [Dataset](#dataset)
- [Usage](#usage)
- [Citation](#citation)
- [License](#license)

## Overview
Large Language Models (LLMs) have demonstrated exceptional capabilities in solving various tasks, progressively evolving into general-purpose assistants. The increasing integration of LLMs into society has sparked interest in their ``behavioral patterns'' and whether these patterns remain consistent across different contexts—questions that could deepen our understanding of LLMs’ limitations and usages. This paper proposes evaluating LLMs using psychometrics, employing psychological constructs as examples to demonstrate how psychometrics can uncover LLMs' behavioral patterns and enhance evaluation reliability. Our framework encompasses psychological dimension identification, assessment dataset design, and assessment with results validation. We identify five key psychological constructs---personality, values, emotional intelligence, theory of mind, and self-efficacy---assessed through a suite of 13 datasets featuring diverse scenarios and item types. We reveal complexities in LLMs' behaviors and uncover significant discrepancies between LLMs' self-reported traits and their response patterns in real-world scenarios. Our findings also show that some preference-based tests, originally designed for humans, could not solicit reliable responses from LLMs. This paper offers a thorough psychometric assessment of LLMs, providing insights into reliable evaluation and potential applications in AI and social sciences. 

## Installation
```bash
bash install.sh
```

## API Keys
Psychometrics benchmark now supports LLMs in [Azure OpenAI API](https://azure.microsoft.com/en-us/products/ai-services/openai-service), [deepinfra](https://deepinfra.com/google/codegemma-7b-it?gad_source=1&gclid=Cj0KCQjwzva1BhD3ARIsADQuPnXXYTOm2_N7a0eu8-sBxnEie5o3Y4sCI9ug3Y_mb0bs4kIgUb6xqawaApXjEALw_wcB), [Zhipu](https://open.bigmodel.cn/dev/api#sdk_install), and [Qwen](https://www.alibabacloud.com/help/en/model-studio/developer-reference/use-qwen-by-calling-api). Specify API keys in `api.yaml`.

Also, in the `generation.py` file, specify `api_version` and `azure_endpoint` for OpenAI models.

## Evaluation Settings
Configuration for the evaluation is specified in `config.yaml`. This file sets up the models to use, the dimensions to evaluate, and the sub-tasks for each dimension. Reliability forms such as internal consistency, parallel forms, and inter-rater reliability are also defined here. If you prefer to evaluate all dimensions and all sub-tasks, this section can be left blank.

### Supported Models
gpt-4, gpt-3.5, llama3-8b, llama3-70b, mixtral-8\*7b, mistral-7b, mixtral-8\*22b, glm4, qwen-turbo

### Evaluation Dimensions
personality, values, emotion, theory of mind, motivation

### Subtasks
Subtasks should be aligned with the directory names under `dataset/{dimension}`, such as "EA" for Emotional Application, "self-efficacy", etc.

### Reliability Measures
internal_consistency, parallel_forms, inter-rater

## Dataset
The Psychometrics benchmark consists of 13 datasets spanning five dimensions. The datasets are organized in the `dataset` folder and are summarized in the table below. The term "Psych. Test" refers to a Psychometrics test, while "Est. Dataset" indicates an Established dataset. The symbols ○ and ● represent evaluation through automatic scripts (e.g., keywords matching) and the LLM-as-a-judge approach using GPT-4 and Llama3-70b as raters, respectively.

| Dimension       | Dataset                        | Source         | Number | Item Type             | Eval | License                          |
|-----------------|--------------------------------|----------------|--------|-----------------------|------|----------------------------------|
| **Personality** | Big Five Inventory             | Psych. Test    | 44     | Rating-Scale (1~5)    | ○    |  NC 4.0 |
| **Personality** | Short Dark Triad               | Psych. Test    | 12     | Rating-Scale (1~5)    | ○    | DbCL v1.0        |
| **Personality** | Vignette Test (Big Five)       | Est. Dataset   | 5      | Open-ended            | ●    | NC 4.0  |
| **Values**      | Cultural Orientation           | Psych. Test    | 27     | Rating-Scale (1~5)    | ○    | NC 4.0        |
| **Values**      | MoralChoice                    | Est. Dataset   | 1767   | Alternative-Choice    | ○    | cc-by-4.0  |
| **Values**      | Human-Centered Values          | Self-Design    | 228    | Alternative-Choice    | ○    | MIT           |
| **Emotion**     | Emotion Understanding          | Est. Dataset   | 200    | Multiple-Choice       | ○    | MIT  |
| **Emotion**     | Emotion Application            | Est. Dataset   | 200    | Multiple-Choice       | ○    | MIT  |
| **Theory of Mind** | False Belief Task            | Est. Dataset   | 40     | Alternative-Choice    | ○    | -  |
| **Theory of Mind** | Strange Stories Task         | Est. Dataset   | 11     | Open-Ended            | ●    | -  |
| **Theory of Mind** | Imposing Memory Task         | Est. Dataset   | 18     | Alternative-Choice    | ○    | -  |
| **Motivation**  | LLM Self-Efficacy              | Self-Design    | 6      | Rating-Scale (0~100)  | ○    | MIT           |
| **Motivation**  | HoneSet                        | Est. Dataset   | 987    | Open-Ended            | ●    | -  |


## Usage
### Generation
Execute the following command to run the generation script with the specified configuration:
```bash
python3 generation.py config.yaml
```
### Evaluation
```bash
python3 evaluation.py
```
The evaluation will be saved in results.json file under result folder under each models

## Future Work
We plan to extend our psychometric benchmark and provide a comprehensive evaluation tools that are easy to use and customize. We will extend the efforts to the following directions:

- [ ] Automatic generation of parallel forms of test
- [ ] More fine-grained datasets
- [ ] Downstream application evaluation

Stay tuned for the updates!
