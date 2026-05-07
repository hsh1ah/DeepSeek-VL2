<!-- markdownlint-disable first-line-h1 -->
<!-- markdownlint-disable html -->
<!-- markdownlint-disable no-duplicate-header -->

<div align="center">
  <img src="images/logo.svg" width="60%" alt="DeepSeek AI" />
</div>
<hr>
<div align="center">

  <a href="https://www.deepseek.com/" target="_blank">
    <img alt="Homepage" src="images/badge.svg" />
  </a>
  <a href="https://huggingface.co/spaces/deepseek-ai/deepseek-vl2-small" target="_blank">
    <img alt="Chat" src="https://img.shields.io/badge/🤖%20Chat-DeepSeek%20VL-536af5?color=536af5&logoColor=white" />
  </a>
  <a href="https://huggingface.co/deepseek-ai" target="_blank">
    <img alt="Hugging Face" src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-DeepSeek%20AI-ffc107?color=ffc107&logoColor=white" />
  </a>

</div>


<div align="center">

  <a href="https://discord.gg/Tc7c45Zzu5" target="_blank">
    <img alt="Discord" src="https://img.shields.io/badge/Discord-DeepSeek%20AI-7289da?logo=discord&logoColor=white&color=7289da" />
  </a>
  <a href="images/qr.jpeg" target="_blank">
    <img alt="Wechat" src="https://img.shields.io/badge/WeChat-DeepSeek%20AI-brightgreen?logo=wechat&logoColor=white" />
  </a>
  <a href="https://twitter.com/deepseek_ai" target="_blank">
    <img alt="Twitter Follow" src="https://img.shields.io/badge/Twitter-deepseek_ai-white?logo=x&logoColor=white" />
  </a>

</div>

<div align="center">

  <a href="LICENSE-CODE">
    <img alt="Code License" src="https://img.shields.io/badge/Code_License-MIT-f5de53?&color=f5de53">
  </a>
  <a href="LICENSE-MODEL">
    <img alt="Model License" src="https://img.shields.io/badge/Model_License-Model_Agreement-f5de53?&color=f5de53">
  </a>
</div>


<p align="center">
  <a href="https://github.com/deepseek-ai/DeepSeek-VL2/tree/main?tab=readme-ov-file#3-model-download"><b>📥 Model Download</b></a> |
  <a href="https://github.com/deepseek-ai/DeepSeek-VL2/tree/main?tab=readme-ov-file#4-quick-start"><b>⚡ Quick Start</b></a> |
  <a href="https://github.com/deepseek-ai/DeepSeek-VL2/tree/main?tab=readme-ov-file#5-license"><b>📜 License</b></a> |
  <a href="https://github.com/deepseek-ai/DeepSeek-VL2/tree/main?tab=readme-ov-file#6-citation"><b>📖 Citation</b></a> <br>
  <a href="./DeepSeek_VL2_paper.pdf"><b>📄 Paper Link</b></a> |
  <a href="https://arxiv.org/abs/2412.10302"><b>📄 Arxiv Paper Link</b></a> |
  <a href="https://huggingface.co/spaces/deepseek-ai/deepseek-vl2-small"><b>👁️ Demo</b></a>
</p>

## 1. Introduction

Introducing DeepSeek-VL2, an advanced series of large Mixture-of-Experts (MoE) Vision-Language Models that significantly improves upon its predecessor, DeepSeek-VL. DeepSeek-VL2 demonstrates superior capabilities across various tasks, including but not limited to visual question answering, optical character recognition,  document/table/chart understanding, and visual grounding. Our model series is composed of three variants: DeepSeek-VL2-Tiny, DeepSeek-VL2-Small and DeepSeek-VL2, with 1.0B, 2.8B and 4.5B activated parameters respectively.
DeepSeek-VL2 achieves competitive or state-of-the-art performance with similar or fewer activated parameters compared to existing open-source dense and MoE-based models.


[DeepSeek-VL2: Mixture-of-Experts Vision-Language Models for Advanced Multimodal Understanding]()

Zhiyu Wu*, Xiaokang Chen*, Zizheng Pan*, Xingchao Liu*, Wen Liu**, Damai Dai, Huazuo Gao, Yiyang Ma, Chengyue Wu, Bingxuan Wang, Zhenda Xie, Yu Wu, Kai Hu, Jiawei Wang, Yaofeng Sun, Yukun Li, Yishi Piao, Kang Guan, Aixin Liu, Xin Xie, Yuxiang You, Kai Dong, Xingkai Yu, Haowei Zhang, Liang Zhao, Yisong Wang, Chong Ruan*** (* Equal Contribution, ** Project Lead, *** Corresponding Author)


## 2. Release

### Model Zoo

| Model | #Total Params | #Activated Params | HuggingFace |
|-------|--------------|-------------------|-------------|
| DeepSeek-VL2-Tiny | 3.37B | 1.0B | [🤗 Link](https://huggingface.co/deepseek-ai/deepseek-vl2-tiny) |
| DeepSeek-VL2-Small | 16.1B | 2.8B | [🤗 Link](https://huggingface.co/deepseek-ai/deepseek-vl2-small) |
| DeepSeek-VL2 | 27.5B | 4.5B | [🤗 Link](https://huggingface.co/deepseek-ai/deepseek-vl2) |


## 3. Model Download

You can download the models from 🤗 HuggingFace:

```shell
# DeepSeek-VL2-Tiny (3.37B total, 1.0B activated)
huggingface-cli download deepseek-ai/deepseek-vl2-tiny --local-dir deepseek-vl2-tiny

# DeepSeek-VL2-Small (16.1B total, 2.8B activated)
huggingface-cli download deepseek-ai/deepseek-vl2-small --local-dir deepseek-vl2-small

# DeepSeek-VL2 (27.5B total, 4.5B activated)
huggingface-cli download deepseek-ai/deepseek-vl2 --local-dir deepseek-vl2
```

## 4. Quick Start

### Installation

```shell
git clone https://github.com/deepseek-ai/DeepSeek-VL2.git
cd DeepSeek-VL2
pip install -e .
```

### Inference with Transformers

```python
import torch
from transformers import AutoModelForCausalLM

from deepseek_vl2.models import DeepseekVLV2Processor, DeepseekVLV2ForCausalLM
from deepseek_vl2.utils.io import load_pil_images

# specify the path to the model
model_path = "deepseek-ai/deepseek-vl2-small"
vl_chat_processor: DeepseekVLV2Processor = DeepseekVLV2Processor.from_pretrained(model_path)
tokenizer = vl_chat_processor.tokenizer

vl_gpt: DeepseekVLV2ForCausalLM = AutoModelForCausalLM.from_pretrained(
    model_path,
    trust_remote_code=True,
    torch_dtype=torch.bfloat16
).cuda().eval()

# single image conversation
conversation = [
    {
        "role": "User",
        "content": "<image>\nDescribe the image.",
        "images": ["./images/training_pipelines.png"],
    },
    {
        "role": "Assistant",
        "content": ""
    }
]

# load images and prepare for inputs
pil_images = load_pil_images(conversation)
prepare_inputs = vl_chat_processor(
    conversations=conversation,
    images=pil_images,
    force_batchify=True
).to(vl_gpt.device)

# run image encoder to get the image embeddings
inputs_embeds = vl_gpt.prepare_inputs_embeds(**prepare_inputs)

# run the model to get the response
outputs = vl_gpt.language_model.generate(
    inputs_embeds=inputs_embeds,
    attention_mask=prepare_inputs.attention_mask,
    pad_token_id=tokenizer.eos_token_id,
    bos_token_id=tokenizer.bos_token_id,
    eos_token_id=tokenizer.eos_token_id,
    max_new_tokens=512,
    do_sample=False,
    use_cache=True
)

answer = tokenizer.decode(outputs[0].cpu().tolist(), skip_special_tokens=True)
print(f"{prepare_inputs['sft_format'][0]}", answer)
```

### Multi-image Conversation

```python
# multi-image conversation
conversation = [
    {
        "role": "User",
        "content": "This is image_1: <image>\nThis is image_2: <image>\nThis is image_3: <image>\nCan you tell me what are in the images?",
        "images": [
            "https://raw.githubusercontent.com/deepseek-ai/DeepSeek-VL2/main/images/image_1.jpg",
            "https://raw.githubusercontent.com/deepseek-ai/DeepSeek-VL2/main/images/image_2.jpg",
            "https://raw.githubusercontent.com/deepseek-ai/DeepSeek-VL2/main/images/image_3.jpg"
        ],
    },
    {
        "role": "Assistant",
        "content": ""
    }
]

# load images and prepare for inputs
pil_images = load_pil_images(conversation)
prepare_inputs = vl_chat_processor(
    conversations=conversation,
    images=pil_images,
    force_batchify=True
).to(vl_gpt.device)

# run image encoder to get the image embeddings
inputs_embeds = vl_gpt.prepare_inputs_embeds(**prepare_inputs)

# run the model to get the response
outputs = vl_gpt.language_model.generate(
    inputs_embeds=inputs_embeds,
    attention_mask=prepare_inputs.attention_mask,
    pad_token_id=tokenizer.eos_token_id,
    bos_token_id=tokenizer.bos_token_id,
    eos_token_id=tokenizer.eos_token_id,
    max_new_tokens=512,
    do_sample=False,
    use_cache=True
)

answer = tokenizer.decode(outputs[0].cpu().tolist(), skip_special_tokens=True)
print(f"{prepare_inputs['sft_format'][0]}", answer)
```

### Grounding

```python
conversation = [
    {
        "role": "User",
        "content": "<image>\n<|ref|>Describe the image.<|/ref|>",
        "images": ["./images/training_pipelines.png"],
    },
    {
        "role": "Assistant",
        "content": ""
    }
]

# load images and prepare for inputs
pil_images = load_pil_images(conversation)
prepare_inputs = vl_chat_processor(
    conversations=conversation,
    images=pil_images,
    force_batchify=True
).to(vl_gpt.device)

# run image encoder to get the image embeddings
inputs_embeds = vl_gpt.prepare_inputs_embeds(**prepare_inputs)

# run the model to get the response
outputs = vl_gpt.language_model.generate(
    inputs_embeds=inputs_embeds,
    attention_mask=prepare_inputs.attention_mask,
    pad_token_id=tokenizer.eos_token_id,
    bos_token_id=tokenizer.bos_token_id,
    eos_token_id=tokenizer.eos_token_id,
    max_new_tokens=512,
    do_sample=False,
    use_cache=True
)

answer = tokenizer.decode(outputs[0].cpu().tolist(), skip_special_tokens=True)
print(f"{prepare_inputs['sft_format'][0]}", answer)
```

And the output is something like:
```
<|User|>: This is image_1: <image>
This is image_2: <image>
This is image_3: <image>
 Can you tell me what are in the images?

<|Assistant|>: The first image contains carrots. The second image contains corn. The third image contains meat.<｜end▁of▁sentence｜>
```

Parse the bounding box coordinates, please refer to [parse_ref_bbox](https://github.com/deepseek-ai/DeepSeek-VL2/blob/main/deepseek_vl2/serve/app_modules/utils.py#L270-L298).


### Full Inference Example
```shell
# without incremental prefilling
CUDA_VISIBLE_DEVICES=0 python inference.py --model_path "deepseek-ai/deepseek-vl2"

# with incremental prefilling, when using 40G GPU for vl2-small
CUDA_VISIBLE_DEVICES=0 python inference.py --model_path "deepseek-ai/deepseek-vl2-small" --chunk_size 512

```


### Gradio Demo

* Install the necessary dependencies:
```shell
pip install -e .[gradio]
```

* then run the following command:

```shell
# vl2-tiny, 3.37B-MoE in total, activated 1B, can be run on a single GPU < 40GB
CUDA_VISIBLE_DEVICES=2 python web_demo.py \
--model_name "deepseek-ai/deepseek-vl2-tiny"  \
--port 37914


# vl2-small, 16.1B-MoE in total, activated 2.4B
# If run on A100 40GB GPU, you need to set the `--chunk_size 512` for incremental prefilling for saving memory and it might be slow.
# If run on > 40GB GPU, you can ignore the `--chunk_size 512` for faster response.
CUDA_VISIBLE_DEVICES=2 python web_demo.py \
--model_name "deepseek-ai/deepseek-vl2-small"  \
--port 37914 \
--chunk_size 512

# # vl27.5-MoE in total, activated 4.2B
CUDA_VISIBLE_DEVICES=2 python web_demo.py \
--model_name "deepseek-ai/deepseek-vl2"  \
--port 37914
```

* **Important**: This is a basic and native demo implementation without any deployment optimizations, which may result in slower performance. For production environments, consider using optimized deployment solutions, such as vllm, sglang, lmdeploy, etc. These optimizations will help achieve faster response times and better cost efficiency.

## 5. License

This code repository is licensed under [MIT License](./LICENSE-CODE). The use of DeepSeek-VL2 models is subject to [DeepSeek Model License](./LICENSE-MODEL). DeepSeek-VL2 series supports commercial use.

## 6. Citation

```
@misc{wu2024deepseekvl2mixtureofexpertsvisionlanguagemodels,
      title={DeepSeek-VL2: Mixture-of-Experts Vision-Language Models for Advanced Multimodal Understanding},
      author={Zhiyu Wu and Xiaokang Chen and Zizheng Pan and Xingchao Liu and Wen Liu and Damai Dai and Huazuo Gao and Yiyang Ma and Chengyue Wu and Bingxuan Wang and Zhenda Xie and Yu Wu and Kai Hu and Jiawei Wang and Yaofeng Sun and Yukun Li and Yishi Piao and Kang Guan and Aixin Liu and Xin Xie and Yuxiang You and Kai Dong and Xingkai Yu and Haowei Zhang and Liang Zhao and Yisong Wang and Chong Ruan},
      year={2024},
      eprint={2412.10302},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2412.10302},
}
```

## 7. Contact

If you have any questions, please raise an issue or contact us at [service@deepseek.com](mailto:service@deepseek.com).

## 8. Related Project

Related project: [Qwen2.5-VL](https://github.com/QwenLM/Qwen2.5-VL)
