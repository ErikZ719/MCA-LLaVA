# MCA-LLaVA: Manhattan Causal Attention for Reducing Hallucination in Large Vision-Language Models 
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

## 🤗 Model
coming soon
- [mca-llava-1.5-7b](https://huggingface.co/)

## Citation
```bibtex
@article{zhaoMCA,
  title={MCA-LLaVA: Manhattan Causal Attention for Reducing Hallucination in Large Vision-Language Models},
  author={Zhao, Qiyan and  Zhang, Xiaofeng and Li, yiheng and Xing, Yun and Yuan Xiaosong and Tang, Feilong and Fan, Sinan and Chen, Xuhang and Zhang, Xuyao and Wang, Dahan},
  journal={The 33rd ACM International Conference on Multimedia},
  year={2025},
  url={https://doi.org/10.1145/3746027.3755271}, 
}
```
## Acknowledgement

This repo is built on [LLaVA](https://github.com/haotian-liu/LLaVA) (models) and [CCA-LLaVA]([https://github.com/pkunlp-icler/FastV](https://github.com/xing0047/cca-llava)) . Many thanks for their efforts. The use of our code should also follow the original licenses.
