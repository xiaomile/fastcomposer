# FastComposer: Tuning-Free Multi-Subject Image Generation with Localized Attention [[website](https://fastcomposer.mit.edu/)] [[demo](https://fastcomposer.hanlab.ai)][[replicate api](https://replicate.com/cjwbw/fastcomposer)]

![resize_multi-subject](https://github.com/xiaomile/fastcomposer/assets/14927720/8a25789c-8d30-40cb-8ac5-e3bd3b617aac)


## Abstract

Diffusion models excel at text-to-image generation, especially in subject-driven generation for personalized images. However, existing methods are inefficient due to the subject-specific fine-tuning, which is computationally intensive and hampers efficient deployment. Moreover, existing methods struggle with multi-subject generation as they often blend features among subjects. We present FastComposer which enables efficient, personalized, multi-subject text-to-image generation without fine-tuning. FastComposer uses subject embeddings extracted by an image encoder to augment the generic text conditioning in diffusion models, enabling personalized image generation based on subject images and textual instructions with only forward passes. To address the identity blending problem in the multi-subject generation, FastComposer proposes cross-attention localization supervision during training, enforcing the attention of reference subjects localized to the correct regions in the target images. Naively conditioning on subject embeddings results in subject overfitting. FastComposer proposes delayed subject conditioning in the denoising step to maintain both identity and editability in subject-driven image generation. FastComposer generates images of multiple unseen individuals with different styles, actions, and contexts. It achieves 300x-2500x speedup compared to fine-tuning-based methods and requires zero extra storage for new subjects. FastComposer paves the way for efficient, personalized, and high-quality multi-subject image creation.


## Usage

### Environment Setup

```bash
conda create -n fastcomposer python
conda activate fastcomposer
pip install torch torchvision torchaudio
pip install transformers==4.25.1 accelerate datasets evaluate diffusers==0.16.1 xformers triton scipy clip gradio

python setup.py install
```

### Download the Pre-trained Models

```bash
mkdir -p model/fastcomposer ; cd model/fastcomposer
wget https://huggingface.co/mit-han-lab/fastcomposer/resolve/main/pytorch_model.bin
```

### Gradio Demo

We host a demo [here](https://fastcomposer.hanlab.ai/). You can also run the demo locally by 

```bash   
python demo/run_gradio.py --finetuned_model_path model/fastcomposer/pytorch_model.bin  --mixed_precision "fp16"
```

### Inference

```bash
bash scripts/run_inference.sh
```

### Training

Prepare the FFHQ training data:
  
```bash 
cd data
wget https://huggingface.co/datasets/mit-han-lab/ffhq-fastcomposer/resolve/main/ffhq_fastcomposer.tgz
tar -xvzf ffhq_fastcomposer.tgz
```

Run training:

```bash
bash scripts/run_training.sh
```

## test images
<table align="center">
<thead>
  <tr>
    <td>
<div align="center">
  <img src="https://user-images.githubusercontent.com/14927720/265911400-91635451-54b6-4dc6-92a7-c1d02f88b62e.jpeg" width="400"/>
  <br/>
  <b>'einstein.png'</b>
</div></td>
    <td>
<div align="center">
  <img src="https://user-images.githubusercontent.com/14927720/265911502-66b67f53-dff0-4d25-a9af-3330e446aa48.jpeg" width="400"/>
  <br/>
  <b>'newton.png'</b>
</div></td>
    <td>
</thead>
</table>


## output
![output_0](https://github.com/xiaomile/fastcomposer/assets/14927720/4975d6e2-c5fc-4324-80c9-a7a512953218)


## TODOs

- [x] Release inference code
- [x] Release pre-trained models
- [x] Release demo
- [x] Release training code and data
- [ ] Release evaluation code and data

## Citation

If you find FastComposer useful or relevant to your research, please kindly cite our paper:

```bibtex
@article{xiao2023fastcomposer,
            title={FastComposer: Tuning-Free Multi-Subject Image Generation with Localized Attention},
            author={Xiao, Guangxuan and Yin, Tianwei and Freeman, William T. and Durand, Frédo and Han, Song},
            journal={arXiv},
            year={2023}
          }
```
