<p align="center">
  <img src="figures/granite-4_0-language-models-3x-v1.png" />
</p>

<p align="center">
  :books: <a href="https://github.com/ibm-granite/granite-4.0-language-models">Paper (comming soon)</a>&nbsp | :hugs: <a href="https://huggingface.co/collections/ibm-granite/granite-40-language-models-6811a18b820ef362d9e5a82c">HuggingFace Collection</a>&nbsp | 
  :speech_balloon: <a href="https://github.com/orgs/ibm-granite/discussions">Discussions Page</a>&nbsp | 📘 <a href="https://www.ibm.com/granite/docs/">IBM Granite Docs</a>
<br>

---
## Introduction to Granite 4.0 Language Models
Granite 4.0 language models are lightweight, state-of-the-art, open foundation models that natively support multilinguality, coding, reasoning, RAG tasks, and tool usage, including the potential to be run on constrained compute resources. All the models are publicly released under an Apache 2.0 license for both research and commercial use. The models' data curation and training procedure were designed for enterprise usage and customization, with a process that evaluates datasets for governance, risk and compliance (GRC) criteria, in addition to IBM's standard data clearance process and document quality checks.

Granite 4.0 models retain the context length and key capabilities of earlier versions, such as response length control and response originality. Granite 4.0 also supports fill-in-the-middle (FIM) code completion and reasoning.

Granite 4.0 models are available in four different sizes and are built on a dense, dense-hybrid, and MoE with hybrid architectures. We release base model — checkpoints of models after pretraining, as well as instruct checkpoints — models finetuned for dialogue, instruction-following, helpfulness, and safety.

<!-- TO DO: Mention an evaluation highlight -->
<!-- Evaluation results show that Granite-3.3-8B-Instruct outperforms models of similar parameter sizes in [Hugging Face's OpenLLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard#/) (see Figure 1). 

<figure>
  <img src="https://github.com/ibm-granite/granite-3.1-language-models/blob/main/figures/granite-3_1-8b-instruct.png"
  alt=" Granite-3.1-8B-Instruct">
  <figcaption>
  Figure 1. Evaluation results from Granite-3.1-8B-Instruct in Hugging Face's OpenLLM Leaderboard.</figcaption>
</figure>
</br> -->
Comprehensive evaluation results for all model variants, as well as other relevant information will be available in Granite 4.0 Language Models technical report.

## How to Use our Models?
To use any of our models, pick an appropriate `model_path` from:
1. `iibm-granite/granite-4.0-micro-base`
2. `ibm-granite/granite-4.0-micro`
3. `ibm-granite/granite-4.0-h-micro-base`
4. `ibm-granite/granite-4.0-h-micro`
5. `ibm-granite/granite-4.0-h-tiny-base`
6. `ibm-granite/granite-4.0-h-tiny`
7. `ibm-granite/granite-4.0-h-small-base`
8. `ibm-granite/granite-4.0-h-small`

### Inference
This is a simple example of how to use Granite-3.1-1B-A400M-Instruct model.

```python
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

device = "auto"
model_path = "ibm-granite/granite-4.0-h-small"
tokenizer = AutoTokenizer.from_pretrained(model_path)
# drop device_map if running on CPU
model = AutoModelForCausalLM.from_pretrained(model_path, device_map=device)
model.eval()
# change input text as desired
chat = [
    { "role": "user", "content": "What is the largest ocean on Earth?"},
]

chat = tokenizer.apply_chat_template(chat, tokenize=False, add_generation_prompt=True)

# tokenize the text
input_tokens = tokenizer(chat, return_tensors="pt").to(device)
# generate output tokens
output = model.generate(**input_tokens, 
                        max_new_tokens=150)
# decode output tokens into text
output = tokenizer.batch_decode(output)
# print output
print(output)
```
## How to Download our Models?
The model of choice (`ibm-granite/granite-4.0-h-small` in this example) can be cloned using:
```shell
git clone https://https://huggingface.co/ibm-granite/granite-4.0-h-small
```

## How to Contribute to this Project?
Plese check our [Guidelines](/CONTRIBUTING.md) and [Code of Conduct](/CODE_OF_CONDUCT.md) to contribute to our project.

## Model Cards
The model cards for each model variant are available in their respective HuggingFace repository. Please visit our collection [here](https://huggingface.co/collections/ibm-granite/granite-40-language-models-6811a18b820ef362d9e5a82c).

## License 
All Granite 4.0 Language Models are distributed under [Apache 2.0](./LICENSE) license.

## Would you like to provide feedback?
Please let us know your comments about our family of language models by visiting our [collection](https://huggingface.co/collections/ibm-granite/granite-40-language-models-6811a18b820ef362d9e5a82c). Select the repository of the model you would like to provide feedback about. Then, go to *Community* tab, and click on *New discussion*. Alternatively, you can also post any questions/comments on our [github discussions page](https://github.com/orgs/ibm-granite/discussions).

<!-- ## Citation
If you find granite models useful, please cite:

```
@misc{granite2024granite,
  title={Granite 4.0 Language Models},
  url={},
  author={Granite Team, IBM},
  month={October},
  year={2024}
}
``` -->