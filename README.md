# GPT-4-ENEM

**\*\*\* Most of the code in this repository has been adapted from [Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness). \*\*\***

## Introduction

This repository contains code and data used in the following papers:

- [Evaluating GPT-4's Vision Capabilities on Brazilian University Admission Exams](https://arxiv.org/abs/2311.14169). 
- [Evaluating GPT-3.5 and GPT-4 Models on Brazilian University Admission Exams](https://arxiv.org/abs/2303.17003).

This most recent study presents a comprehensive framework to evaluate language models on entrance exams, which incorporates both textual and visual elements. We evaluate the three most recent editions of *[Exame Nacional do Ensino Médio (ENEM)](https://www.gov.br/inep/pt-br/areas-de-atuacao/avaliacao-e-exames-educacionais/enem)*, the main standardized entrance examination adopted by Brazilian universities.

<!-- Our study not only reaffirms the capabilities of GPT-4 as the state of the art for handling complex multidisciplinary questions, but also pioneers in offering a realistic assessment of multimodal language models on Portuguese examinations. -->

One of the highlights is that text captions transcribing visual content outperform the direct use of images, suggesting that the vision model has room for improvement. Yet, despite improvements afforded by images or captions, mathematical questions remain a challenge for these state-of-the-art models.

Significant improvements are noticeable when incorporating either textual or visual representations of images, with the difference nearing 10 points, particularly when utilizing captions.

<table>
  <tr>
    <th rowspan="2">Area</th>
    <th colspan="3" style="text-align: center;">GPT-4o</th>
    <th colspan="3" style="text-align: center;">Sabiá-3</th>
  </tr>
  <tr>
    <th>without images</th>
    <th>with captions</th>
    <th>with CoT + captions</th>
    <th>without images</th>
    <th>with captions</th>
    <th>with CoT + captions</th>
  </tr>
  <tr>
    <td>Languages and Codes</td>
    <td>88.89</td>
    <td>91.11</td>
    <td>91.11</td>
    <td>86.67</td>
    <td>91.11</td>
    <td>93.33</td>
  </tr>
  <tr>
    <td>Human Sciences</td>
    <td>100.00</td>
    <td>100.00</td>
    <td>100.00</td>
    <td>100.00</td>
    <td>100.00</td>
    <td>100.00</td>
  </tr>
  <tr>
    <td>Natural Sciences</td>
    <td>68.18</td>
    <td>84.09</td>
    <td>93.18</td>
    <td>72.73</td>
    <td>81.82</td>
    <td>86.36</td>
  </tr>
  <tr>
    <td>Mathematics</td>
    <td>60.00</td>
    <td>66.67</td>
    <td>91.11</td>
    <td>60.00</td>
    <td>75.56</td>
    <td>82.22</td>
  </tr>
  <tr>
    <td style="font-weight: bold;">Total</td>
    <td style="font-weight: bold;">79.33</td>
    <td style="font-weight: bold;">85.47</td>
    <td style="font-weight: bold;">93.85</td>
    <td style="font-weight: bold;">79.89</td>
    <td style="font-weight: bold;">87.15</td>
    <td style="font-weight: bold;">90.50</td>
  </tr>
</table>

<p style="text-align: center;">Results of GPT-4o and Sabiá-3 on ENEM 2024, using 3-shot prompts.</p>

## Data

We made available the [ENEM 2022](data/enem/2022.jsonl), [ENEM 2023](data/enem/2023.jsonl), and [ENEM 2024](data/enem/2024.jsonl) datasets. These datasets encompass all multiple-choice questions from the last three editions. The datasets have been created to allow the evaluation of both textual-only and textual-visual language models. To evaluate textual-only models, we incorporated into the datasets the textual descriptions of the images that appear in the questions' statements from the orange ENEM exam booklet, a particular booklet that offers accessibility to people with visual impairments.

The datasets can also be accessed via the 🤗 Datasets library: https://huggingface.co/datasets/maritaca-ai/enem

The deprecated ENEM 2022 dataset can be found [here](data/enem/2022.json).

> [!Warning]
> We do not recommend using the deprecated dataset, since it does not include the image placeholders, image paths, and textual descriptions. Also, the tables are not well-formatted.

## Tasks

We have implemented a set of 22 tasks, described below:

<table>
  <thead>
    <tr>
      <th>Task</th>
      <th>Enem edition</th>
      <th>Experiment</th>
      <th>CoT</th>
      <th>Use all the questions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>enem_2022_blind</td>
      <td>ENEM 2022</td>
      <td>without images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2022_blind</td>
      <td>ENEM 2022</td>
      <td>without images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2022_images</td>
      <td>ENEM 2022</td>
      <td>with images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2022_images</td>
      <td>ENEM 2022</td>
      <td>with images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2022_captions</td>
      <td>ENEM 2022</td>
      <td>with captions</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2022_captions</td>
      <td>ENEM 2022</td>
      <td>with captions</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2023_blind</td>
      <td>ENEM 2023</td>
      <td>without images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2023_blind</td>
      <td>ENEM 2023</td>
      <td>without images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2023_images</td>
      <td>ENEM 2023</td>
      <td>with images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2023_images</td>
      <td>ENEM 2023</td>
      <td>with images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2023_captions</td>
      <td>ENEM 2023</td>
      <td>with captions</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2023_captions</td>
      <td>ENEM 2023</td>
      <td>with captions</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2024_blind</td>
      <td>ENEM 2024</td>
      <td>without images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2024_blind</td>
      <td>ENEM 2024</td>
      <td>without images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2024_images</td>
      <td>ENEM 2024</td>
      <td>with images</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2024_images</td>
      <td>ENEM 2024</td>
      <td>with images</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_2024_captions</td>
      <td>ENEM 2024</td>
      <td>with captions</td>
      <td>No</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem_cot_2024_captions</td>
      <td>ENEM 2024</td>
      <td>with captions</td>
      <td>Yes</td>
      <td>:heavy_check_mark:</td>
    </tr>
    <tr>
      <td>enem</td>
      <td>Enem Challenge (2009-2017)</td>
      <td>-</td>
      <td>No</td>
      <td>:x:</td>
    </tr>
    <tr>
      <td>enem_cot</td>
      <td>Enem Challenge (2009-2017)</td>
      <td>-</td>
      <td>Yes</td>
      <td>:x:</td>
    </tr>
    <tr>
      <td>enem_2022_deprecated</td>
      <td>ENEM 2022</td>
      <td>-</td>
      <td>No</td>
      <td>:x:</td>
    </tr>
    <tr>
      <td>enem_cot_2022_deprecated</td>
      <td>ENEM 2022</td>
      <td>-</td>
      <td>Yes</td>
      <td>:x:</td>
    </tr>
  </tbody>
</table>


<!-- 1. **enem_2022_blind**: ENEM 2022 without images and without CoT prompting.
2. **enem_cot_2022_blind**: ENEM 2022 without images and with CoT prompting.
3. **enem_2022_images**: ENEM 2022 with images and without CoT prompting.
4. **enem_cot_2022_images**: ENEM 2022 with images and with CoT prompting.
5. **enem_2022_captions**: ENEM 2022 with captions and without CoT prompting.
6. **enem_cot_2022_captions**: ENEM 2022 with captions and with CoT prompting.
7. **enem_2023_blind**: ENEM 2023 without images and without CoT prompting.
8. **enem_cot_2023_blind**: ENEM 2023 without images and with CoT prompting.
9. **enem_2023_images**: ENEM 2023 with images and without CoT prompting.
10. **enem_cot_2023_images**: ENEM 2023 with images and with CoT prompting.
11. **enem_2023_captions**: ENEM 2023 with captions and without CoT prompting.
12. **enem_cot_2023_captions**: ENEM 2023 with captions and with CoT prompting.
13. **enem**: Enem Challenge (2009-2017) without CoT prompting (deprecated).
14. **enem_cot**: Enem Challenge (2009-2017) with CoT prompting (deprecated).
15. **enem_2022_deprecated**: Enem 2022 without CoT prompting (deprecated).
16. **enem_cot_2022_deprecated**: Enem 2022 with CoT prompting (deprecated). -->

## Reproducing the results
To reproduce the experiments described in the paper, please follow the steps below:

### 1. Clone the repository:
```bash
git clone https://github.com/piresramon/gpt-4-enem.git
```

### 2. Install the required packages:
```bash
pip install -e .
```
### 3. Set the API keys:
Visit [openai](https://platform.openai.com/api-keys) to retrieve OpenAI API keys and [maritalk](https://plataforma.maritaca.ai/chaves-de-api) to retrieve MariTalk API keys. Insert them into your env variables.
```bash
OPENAI_API_SECRET_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
MARITALK_API_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
### 4. Run the experiments:

To reproduce the results of the Table 1, run the following commands:

```bash
# running 3-shot with CoT for Sabiá-3 on ENEM 2024
python main.py \
    --model maritalk \
    --model_args engine=sabia-3 \
    --tasks enem_cot_2024_blind,enem_cot_2024_captions \
    --description_dict_path description.json \
    --num_fewshot 3 \
    --conversation_template chatgpt

# running 3-shot with CoT for GPT-4o on ENEM 2024
python main.py \
    --model chatgpt \
    --model_args engine=gpt-4o \
    --tasks enem_cot_2024_blind,enem_cot_2024_images,enem_cot_2024_captions \
    --description_dict_path description.json \
    --num_fewshot 3 \
    --conversation_template chatgpt
```
To experiment other Maritaca AI or OpenAI models, just change the engine. The tasks `enem_cot_*_images` are not supported by text-based models.
<!-- python main.py --model chatgpt --model_args engine=gpt-4-1106-preview --tasks enem_cot_2023 --description_dict_path description.json --num_fewshot 3 --conversation_template chatgpt -->
It is possible to use a different number of few-shot examples (maximum 3).

> [!Tip]
> You can experiment any other model available in the 🤗 Transformers library. Just change the `model` and `model_args` parameters. It is necessary to disable the parameter `conversation_template`.

## Citation
If you use this code or data in your research, please cite the following papers:

```bibtex
@misc{pires2023evaluating,
      title={Evaluating GPT-4's Vision Capabilities on Brazilian University Admission Exams}, 
      author={Ramon Pires and Thales Sales Almeida and Hugo Abonizio and Rodrigo Nogueira},
      year={2023},
      eprint={2311.14169},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

```bibtex
@misc{nunes2023evaluating,
      title={Evaluating GPT-3.5 and GPT-4 Models on Brazilian University Admission Exams}, 
      author={Desnes Nunes and Ricardo Primi and Ramon Pires and Roberto Lotufo and Rodrigo Nogueira},
      year={2023},
      eprint={2303.17003},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

<!-- ## Contact
If you have any questions or comments, please feel free to contact us at pires.ramon@gmail.com. -->