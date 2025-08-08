# MCA-LLaVA: Manhattan Causal Attention for Reducing Hallucination in Large Vision-Language Models 

[![arXiv](https://img.shields.io/badge/Arxiv-2410.15926-b31b1b.svg?logo=arXiv)](https://arxiv.org/abs/2507.09184) <a href="https://huggingface.co/papers/2410.15926"></a> <a href='https://huggingface.co'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Model-blue'></a> 


> **[MCA-LLaVA: Manhattan Causal Attention for Reducing Hallucination in Large Vision-Language Models](https://doi.org/10.1145/3746027.3755271)**<br>
> ACM MM 2025<br>
> Qiyan Zhao*, Xiaofeng Zhang*, Yiheng Li, Yun Xing, Xiaosong Yuan, Feilong Tang, Sinan Fan, Xuhang Chen, Xu-Yao Zhang, Da-Han Wang†<br>

The information flow of MCA-LLaVA is follows:
![image](https://github.com/ErikZ719/MCA-LLaVA/blob/main/information-flow.png)


The difference of MCA-LLaVA with CCA-LLaVA and LLaVA is follows:

![image](https://github.com/ErikZ719/MCA-LLaVA/blob/main/Manhattan-Causal-Masking.png)

## 🛠️ Install
```
conda create -n mca python=3.10 -y
conda activate mca
pip install --upgrade pip  # enable PEP 660 support
pip install torch==2.1.1 torchvision==0.16.1 torchaudio==2.1.1 --index-url https://download.pytorch.org/whl/cu118
pip install -e .
pip install -e ".[train]"
pip install triton==2.1.0 pynvml==11.5.0 --upgrade
pip install flash-attn==2.5.8 --no-build-isolation --no-cache-dir
```
## Data
Please refer to [Data.md](https://github.com/ErikZ719/MCA-LLaVA/blob/main/docs/Data.md) for preparation of training data.

## Train
MCA-LLaVA training pipeline follows [LLaVA-1.5](https://github.com/haotian-liu/LLaVA). The training consists of two stages:
- **Step 1, pretraining**. Train a projector on a CC3M subset of ∼558K image-text pairs to connect a frozen pretrained vision encoder and a frozen LLM.
  ```
  bash scripts/v1_5/pretrain.mca-llava-1.5-7b.sh
  ```
- **Step 2, instruction tuning**. Fine-tune projector and LLM with ~665k multimodal instruction data.
  ```
  bash scripts/v1_5/finetune.mca-llava-1.5-7b.sh
  ```
  
## Model
coming soon
- [mca-llava-1.5-7b](https://huggingface.co/)

## Eval
coming soon

## Usage
To replace default causal scheme with our proposed mca, you can prepend following code to either training or evaluation code, subject to your own use case.
```
import transformers
from llava.mca_utils.mca import llamaforcausallm_forward, mca_forward 
transformers.models.llama.LlamaForCausalLM.forward = llamaforcausallm_forward
transformers.models.llama.LlamaModel.forward = mca_forward
```
We encourage trying a training-free implementation of MCA-LLaVA — it might yield surprising results.

## Citation
```bibtex
@article{zhaoMCA,
  title={MCA-LLaVA: Manhattan Causal Attention for Reducing Hallucination in Large Vision-Language Models},
  author={Zhao, Qiyan and  Zhang, Xiaofeng and Li, Yiheng and Xing, Yun and Yuan, Xiaosong and Tang, Feilong and Fan, Sinan and Chen, Xuhang and Zhang, Xu-Yao and Wang, Da-Han},
  journal={The 33rd ACM International Conference on Multimedia},
  year={2025},
  url={https://doi.org/10.1145/3746027.3755271}, 
}

@article{xing2024mitigating,
  title={Mitigating Object Hallucination via Concentric Causal Attention},
  author={Xing, Yun and Li, Yiheng and Laptev, Ivan and Lu, Shijian},
  journal={arXiv preprint arXiv:2410.15926},
  year={2024}
}
```
## Acknowledgement

This repo is built on [LLaVA](https://github.com/haotian-liu/LLaVA) (models) and [CCA-LLaVA]([https://github.com/pkunlp-icler/FastV](https://github.com/xing0047/cca-llava)) . Many thanks for their efforts. The use of our code should also follow the original licenses.
